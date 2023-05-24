# toolset: openssl

## Tools

* `openssl`

## Files

_None_

## Usage

### pkey

Create rsa key:

    openssl genpkey \
      -algorithm RSA \
      -pkeyopt rsa_keygen_bits:2048 \
      -out key.pem

Create EC key:

    openssl genpkey \
      -algorithm EC \
      -pkeyopt ec_paramgen_curve:P-256 \
      -out key.pem

### x509

Create key and self signed cert:

    openssl req \
      -x509 \
      -newkey rsa:4096 \
      -keyout key.pem \
      -out cert.pem \
      -sha256 \
      -days 365
      -subj "/C=SE/L=Goteborg/O=Local Area Network/OU=Local Area Network Certificate Authority/CN=server.lan"

Create self signed cert with existing key:

    openssl req \
      -x509 \
      -key "path/to/ca.key.pem" \
      -out "path/to/ca.cert.pem" \
      -sha256 \
      -days 365 \
      -subj "/C=SE/L=Goteborg/O=Local Area Network/OU=Local Area Network Certificate Authority/CN=server.lan"

### Inspect and verify

Inspect key:

    openssl pkey -noout -text -in ca.key.pem

Inspect cert:

    openssl x509 -noout -text -in ca.cert.pem

Inspect csr:

    openssl req -noout -text -in ca.csr

Verify intermediate certificate:

    openssl verify -CAfile ca_root.pem ca_intermediate.pem

Verify server/client certificates:

    openssl verify -CAfile ca-bundle.pem server.lan.pem
