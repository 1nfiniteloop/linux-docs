# toolset: gpg

## Tools

* `gpg` - OpenPGP encryption and signing tool.
* `gpg2` - Extended implementation of gpg but fully compatible with gpg. Mainly
  targeted for desktop environments.
* `paperkey` - Backup and restore gpg keys in paper format.

## Files

* `~/.gnupg` - gpg config and keyring.

## Usage

For easier copy-paste of steps below, set identity with:
`gpg_uid="user@example.com"`

### Overview

Command           | Description
------------------|-------------------------------------------
Encrypt           | `gpg --encrypt --recipient <email> <file>`
Decrypt           | `gpg --decrypt <file>.gpg`
Sign              | `gpg --sign <file>`
Verify            | `gpg --verify <file>.gpg`
List public keys  | `gpg --list-keys`
List private keys | `gpg --list-secret-keys`
Change password   | `gpg --passwd ${gpg_uid}`

### Create new keys

The root key shall only be used for issue sub-keys and should be kept stored in
a secure place offline. Thus, set a temporary gpg workdir for key generation
which can be removed later when finshed:

    export GNUPGHOME=${HOME}/.tmp/gnupg-genkey

Create root key, preferably choose Elliptic Curve (ECC) and curve 25519 when
prompted. The chosen password will be used for both root key and subkeys. Set
capability to "Certify" only with no expiry.

    gpg --expert --full-generate-key

Create 3 separate sub-keys for signing, encryption and authentication. The root
key id can be seen from command above or with `gpg --list-keys`. The shortened
key id is just the last part of the complete key id. Recommend to choose
1 year expire.

    $ gpg --expert --edit-key ${key_id}
    gpg> addkey
    ...
    gpg> save

Create revocation certificate which makes it posslbe to revoke the pgp identity.
The certificate file should be stored in a secondary place that allows retrieval
in case the key backup fails.

    gpg --gen-revoke --output ${gpg_uid}.revoke-cert.gpg ${key_id}

Export keys by running all steps under section "Export keys".

Remove workdir:

    gpg --delete-secret-and-public-keys --yes ${gpg_uid}
    rm -r ${GNUPGHOME}

### Export keys

Export private root key and subkeys for secure offline storage:

    gpg --export-secret-keys --armor --output ${gpg_uid}.key.gpg ${key_id}

Export private subkeys without root-key included, for importing to user's home
gpg keyring after root key generation:

    gpg --export-secret-subkeys --armor --output ${gpg_uid}.subkey.gpg ${key_id}

Export public keys for distribution:

    gpg --export --armor --output ${gpg_uid}.gpg ${key_id}

Optionally publish public key to key servers:

    gpg --send-key ${key_id}

### Backup keys

Backup private root key to paperkey:

    gpg --export-secret-key ${key_id} \
      |paperkey --output ${gpg_uid}.paperkey

Backup private root key to paperkey as QR code:

    gpg --export-secret-key ${key_id} \
      |paperkey --output-type raw \
      |qrencode --8bit --output ${gpg_uid}.paperkey.png

Export public key to QR code (in ascii text):

    gpg --armor --export ${key_id} \
      |qrencode --output ${gpg_uid}.ascci.png

### Import keys

Import public or private keys:

    gpg --import <gpg-key>

Update the key trust:

    $ gpg --edit-key ${key_id}
    gpg> trust
    ...
    gpg> quit

### Restore keys

Convert public key to raw format, needed when restoring paperkey
backup below:

    cat ${gpg_uid}.gpg \
      |gpg --dearmor > ${gpg_uid}.gpg.raw

Restore private root key from paperkey backup:

    paperkey --pubring ${gpg_uid}.gpg.raw --secrets ${gpg_uid}.paperkey \
      |gpg --import

Restore private root key from paperkey backup in QR code:

    zbarimg --raw --quiet -S binary ${gpg_uid}.paperkey.png \
      |paperkey --pubring ${gpg_uid}.gpg.raw \
      |gpg --import

__Note:__ flag `-S binary` is a required but undocumented in the man page, it
was added in zbarimg 0.23.1.

Import public key in ascii from QR code:

    zbarimg --raw --quiet ${gpg_uid}.ascci.png \
      |gpg --import

### Update expiry time for subkeys

When subkeys are expired the expiry date need to be extended. This expiry date
only affetcts the public key but the private root key is needed to configure
expiry time. This will create an updated public key that needs to be distributed
to all users.

Create temporary environment for loading root key:

    export GNUPGHOME=${HOME}/.tmp/gnupg
    mkdir -m 700 ${GNUPGHOME}

Import root key:

    gpg --import ${gpg_uid}.key.gpg

Extend expiry time on subkeys for sign, encrypt, authenticate:

    $ gpg --expert --edit-key ${key_id}
    gpg> key 1
    gpg> key 2
    gpg> key 3
    gpg> expire
    ...
    Key is valid for? (0) 1y
    ...
    gpg> save

Export public key with new expiry time for distributing to all users:

    gpg --export --armor --output ${gpg_uid}.gpg ${key_id}

Cleanup environment:

    gpg --delete-secret-and-public-keys --yes ${gpg_uid}
    rm -r ${GNUPGHOME}

## Reference

* <https://github.com/drduh/YubiKey-Guide>
* <https://wiki.archlinux.org/title/Paperkey>
