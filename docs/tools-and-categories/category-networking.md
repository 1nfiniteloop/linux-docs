# category: networking

## Tools

* `dhclient` - DHCP Client.
* `dig` - DNS lookup utility.
* `host` - DNS lookup utility.
* `hostname` - Show or set the system's host name (non-persistent/volatile).
* `hostnamectl` - Control the system hostname (on systemd based systems).
* `nslookup` (older utility than `dig`).
* `ifconfig` - Use `ip` utilities instead, when possible.
* `ip` - Show and change routing, ip-addresses, network-interfaces.
* `lsof` - list open files (and networking connections).
* `mtr` - A continuously updating traceroute, like top.
* `nmcli` - Command-line tool for changing network configuration on
  _network-manager_ based systems (desktop environments).
* `nmtui` - Menu-based tool for changing network configuration on
  _network-manager_ based systems (desktop environments).
* `networkctl` - Query the status of network links, used when
  _systemd-networkd_ is used.
* `netplan` - Front-end for configuring networks (since Ubuntu 18.04 server).
* `ss` - socket statistics (instead of deprecated `netstat`).
* `tcpdump` - Record network traffic.
* `traceroute` - Display network path to a destination.
* `tracepath` - traces path to a network host discovering MTU along this path.

## Files

* `/var/lib/NetworkManager/*.lease` - dhcp leases, on _network-manager_ based
  systems.
* `/run/systemd/netif/leases` - dhcp leases, on _systemd-networkd_ based systems.
* `/run/systemd/network` - Runtime generated network configurations, on
   netplan-based systems.
* `/etc/hosts` - Static hostname resolution.
* `/etc/hostname` - Configured name for this host.
* `/etc/services` - Port numeric-to-name mapping.

## Usage

### DHCP

Ubuntu desktop-version uses _network-manager_ as frontend to manage
networks. Server-versions uses netplan in combination with _systemd-networkd_.
Alpine linux uses `udhcpc` as dhcp client.

Command                                  | Description
-----------------------------------------|----------------------------------------------------------------
`netplan ip leases <iface>`              | Show dhcp leases, on netplan based systems.
`journalctl -u systemd-networkd.service` | Show dhcp leases, on _systemd-networkd_ based systems.
`dhclient -r <iface>`                    | Release dhcp lease, on unmanaged network interfaces*.
`dhclient <iface>`                       | Renew dhcp lease, on unmanaged network interfaces*.
`less /var/lib/dhcp/dhclient.leases`     | Show dhcp leases, on unmanaged network interfaces*.

\* Unmanaged interfaces means manually configured, i.e. not configured through
_network-manager_ (desktop systems) or _systemd-networkd_. Using `dhclient` on
already managed interfaces might result in ambiguous dhcp leases.

### DNS

Command                                   | Description
------------------------------------------|-----------------------------------------------------
`host www.google.com`                     | Get ip address of the domain-name.
`nslookup www.google.com [<name-server>]` | Get ip address of the domain-name.
`dig [@<name-server>] www.gmail.com MX`   | Get dns mx (mail) record.
`systemd-resolve --status <iface>`        | Show used dns-servers (Ubuntu 18.04 or later).
`nmcli device show enp0s3`                | Show used dns-servers (Ubuntu desktop environments).
`tracepath <fqdn>`                        | Trace dns resolution path for domain name.

### Hostname

Command                                   | Description
------------------------------------------|----------------------
`hostname` or `cat /etc/hostname`         | Get current hostname.
`hostnamectl set-hostname <new-hostname>` | Change hostname.

\* Optionally manually edit `/etc/hostname` and apply new name with
   `sudo hostname <new-hostname>`.

### Network interfaces

Command                               | Description
--------------------------------------|-----------------------------------------------------------
`ip link show` or `ls /sys/class/net` | Show all available network interfaces.
`ip route show`                       | Show routing table.
`ip addr show`                        | Show ip-addresses for all network interfaces
`ip link set dev <dev> up|down`       | Set network interface up or down, on unmanaged interfaces.

### TCP/IP

Common used flags to `ss`:

* `[-l|--listening]`
* `[-p|--processes]` - Show what process using the socket.
* `[-t|--tcp]`
* `[-u|--udp]`
* `[-n|--numeric]` - Show ports as numeric value.

Common used flags to `lsof`:

* `[-P]` - Show ports as numeric value.
* `[-n]` - Show ip-address numeric, don't resolve hostname.
* `[-i]` - Show only ip connections.

Command                                         | Description
------------------------------------------------|------------------------------------------------------------
`ss -ltpn`                                      | Show tcp listening ports and what process using the socket.
`lsof -iTCP -sTCP:LISTEN`                       | Show tcp listening ports and what process using the socket.
`lsof -i -n -P`                                 | Show active ip-connections.
`sudo tcpdump -i <iface> port bootpc or bootps` | Listen for dhcp leases.
