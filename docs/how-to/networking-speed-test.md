# networking: speed test

This instruction describes a "poor man's network speed test", using only
basic preinstalled tools found on almost every linux systems.

## Steps

### Measure upstream (upload)

Sends 100Mib to a remote server.

1. On the remote host: `nc -vvl 31000 > /dev/null`.
2. On the local host: `dd if=/dev/zero bs=1M count=100 status='progress' |nc -vv <hostname> 31000`.

### Measure downstream (download)

Receives 100MiB from a remote server.

1. On the remote host: `dd if=/dev/zero |nc -vvl 31001`.
2. On the local host: `nc -vv <HOSTNAME> 31001 |dd of=/dev/null bs=1M count=100 iflag=fullblock status='progress'`
