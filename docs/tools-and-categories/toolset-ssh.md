# toolset: openssh

## Tools

* `ssh` - for logging into a remote machine.
* `scp` - Copy files and folders between hosts.
* `ssh-agent` - authentication agent.
* `ssh-add` - adds private key identities to the authentication agent.
* `ssh-copy-id` - Copy ssh key into host.
* `ssh-import-id-*` - Retrieve one or more public keys from a public keyserver.
* `ssh-keygen` - Generate ssh keypair.

## Files

* `~/.ssh/config` - OpenSSH client configuration files, see `man ssh_config`
* `/etc/ssh/sshd_config` - OpenSSH daemon configuration file, see `man sshd_config`

## Usage

### ssh

Common used flags for `ssh`:

* `[-A]` - Forward authentication agent connection.
* `[-i]` - Private key file to use for this connection.
* `[-L]` - Forward a local port to a remote port.
* `[-N]` - No shell is started, only the connection is established. Usually in
  combination with port forwarding.
* `[-f]` - run in the background, usually in combination with port forwarding.
* `[-R]` - forward a port on the remote host to local (reverse direction).
* `[-o  ...]` - Additional options, see further in `man ssh`.
* `[-p]` - connect to specific port.
* `[-X]` - Enables X11 forwarding, run graphical applications on remote host.
* `[-v]` - Print debug info to console.

Command                                        | Description
-----------------------------------------------|----------------------------------------------------------------------
`ssh -o PubkeyAuthentication=no <user>@<fqdn>` | Connect only with password authentication.
`ssh -X <user>@<fqdn>`                         | Allow x11 forwarding to open graphical applications on remote.
`ssh -A <user>@<fqdn>`                         | Use local ssh keys on remote host, to do another hop with ssh.
`ssh -NL 8080:localhost:80 <user>@<fqdn>`      | Local port 8080 is forwarded to the remote host's "localhost" port 80

### ssh keys

Command                                                 | Description
--------------------------------------------------------|---------------------------------------------------------------------------------------------------------------
`ssh-keygen -a 128 -t ed25519 -f ~/.ssh/<user>@<fqdn>`  | Generate new keypair* based on elliptic curve 25519 and with 128 passphrase key derivation rounds.
`ssh-copy-id -i ~/.ssh/<user>@<fqdn>.pub <user>@<fqdn>` | Copy and enable ssh key to remote host.
`eval $(ssh-agent)`                                     | Start ssh agent. __Note:__ `gnome-keyring` is normally the ssh-agent on desktop environments, thus not needed.
`ssh-add -l`                                            | list available keys in ssh agent.

\* Naming the key according to `<user>@<fqdn>` is good practice for distinguish
keys, example `alice@bob.sh`.
