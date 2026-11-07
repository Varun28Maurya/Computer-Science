
# Lesson 07 — Networking Commands in Windows CMD

## 1. Introduction to Networking in CMD

Networking commands allow users and administrators to inspect, configure, troubleshoot and diagnose network connections using the Windows Command Prompt.

They are useful for:

- Checking internet connectivity.
- Finding IP addresses.
- Diagnosing DNS problems.
- Checking network routes.
- Inspecting active connections.
- Identifying listening ports.
- Examining MAC addresses.
- Troubleshooting Wi-Fi and LAN connections.
- Testing whether a remote server is reachable.

Windows provides several built-in networking utilities, including:

- `ipconfig`
- `ping`
- `tracert`
- `pathping`
- `nslookup`
- `netstat`
- `arp`
- `route`
- `getmac`
- `nbtstat`
- `netsh`

Some commands in this lesson are native CMD utilities. Others, such as PowerShell's `Test-NetConnection`, can be launched from CMD.

---

# 2. Networking Fundamentals

Before learning networking commands, understand these basic concepts.

## 2.1 What is a Computer Network?

A computer network is a group of connected devices that communicate and share information.

Examples:

- Computers connected in a college laboratory.
- Devices connected to a home Wi-Fi network.
- Servers communicating over the internet.
- Smartphones connected to a mobile network.

## 2.2 IP Address

An Internet Protocol address identifies a network interface on an IP network.

Two major versions exist:

### IPv4

IPv4 uses a 32-bit address represented by four decimal numbers.

Example:

`192.168.1.10`

Each number ranges from 0 to 255.

### IPv6

IPv6 uses a 128-bit address represented using hexadecimal notation.

Example:

`2001:db8::1`

IPv6 provides a much larger address space than IPv4.

## 2.3 MAC Address

A Media Access Control address identifies a network interface at the data-link layer.

Example:

`00-1A-2B-3C-4D-5E`

A MAC address is generally associated with a network adapter.

## 2.4 Subnet Mask

A subnet mask identifies which portion of an IPv4 address represents the network and which portion represents the host.

Example:

`255.255.255.0`

## 2.5 Default Gateway

A default gateway is the device that forwards traffic from the local network to other networks.

In a home network, this is usually the router.

Example:

`192.168.1.1`

## 2.6 DNS

DNS stands for Domain Name System.

It translates domain names into IP addresses.

Example:

`google.com` → an IP address returned by DNS.

Without DNS, users would generally need to remember IP addresses instead of domain names.

## 2.7 DHCP

DHCP stands for Dynamic Host Configuration Protocol.

It automatically assigns network configuration information to devices.

This can include:

- IP address.
- Subnet mask.
- Default gateway.
- DNS servers.

## 2.8 Ports

A port identifies a communication endpoint associated with a network service or application.

Common ports:

| Port | Protocol / Service |
|---|---|
| 20, 21 | FTP |
| 22 | SSH |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 110 | POP3 |
| 143 | IMAP |
| 443 | HTTPS |
| 3306 | MySQL |
| 5432 | PostgreSQL |
| 8080 | Common alternative HTTP port |

Ports are associated with transport-layer protocols such as TCP and UDP.

## 2.9 TCP and UDP

### TCP — Transmission Control Protocol

- Connection-oriented.
- Provides reliable, ordered delivery.
- Uses acknowledgements and retransmissions.

### UDP — User Datagram Protocol

- Connectionless.
- Does not guarantee delivery or ordering.
- Has lower protocol overhead.

## 2.10 LAN and WAN

**LAN:** Local Area Network, such as a home, office or college network.

**WAN:** Wide Area Network, which connects networks across larger geographical areas.

## 2.11 Public and Private IP Addresses

Private IPv4 address ranges include:

| Range | Private address block |
|---|---|
| Class A private | 10.0.0.0/8 |
| Class B private | 172.16.0.0/12 |
| Class C private | 192.168.0.0/16 |

Public IP addresses are globally routable, subject to internet routing and filtering policies.

---

# 3. IP Configuration Commands

## 3.1 ipconfig

The `ipconfig` command displays and manages IP configuration information.

### Basic syntax

```cmd
ipconfig
```

Displays basic network configuration for available adapters.

Example output:

```text
Windows IP Configuration

Ethernet adapter Ethernet:

   IPv4 Address. . . . . . . . . . : 192.168.1.10
   Subnet Mask . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . : 192.168.1.1
```

### Display complete configuration

```cmd
ipconfig /all
```

Displays detailed information, including:

- Host name.
- Physical address.
- DHCP status.
- IPv4 and IPv6 addresses.
- DNS servers.
- DHCP server.
- Lease information.

### Release DHCP address

```cmd
ipconfig /release
```

Releases the current DHCP-assigned IPv4 configuration for applicable adapters.

**Warning:** This can temporarily disconnect your computer from the network.

### Renew DHCP address

```cmd
ipconfig /renew
```

Requests a new DHCP configuration.

### Release and renew IPv6 configuration

```cmd
ipconfig /release6
ipconfig /renew6
```

### Flush DNS cache

```cmd
ipconfig /flushdns
```

Clears the local DNS resolver cache.

Useful when a domain resolves to an outdated or incorrect cached address.

### Display DNS cache

```cmd
ipconfig /displaydns
```

Displays cached DNS resolution records.

### Register DNS records

```cmd
ipconfig /registerdns
```

Initiates dynamic DNS registration for the computer.

### Useful ipconfig options

| Command | Purpose |
|---|---|
| `ipconfig` | Basic configuration |
| `ipconfig /all` | Detailed configuration |
| `ipconfig /release` | Release DHCP IPv4 configuration |
| `ipconfig /renew` | Renew DHCP IPv4 configuration |
| `ipconfig /release6` | Release DHCP IPv6 configuration |
| `ipconfig /renew6` | Renew DHCP IPv6 configuration |
| `ipconfig /flushdns` | Clear DNS cache |
| `ipconfig /displaydns` | Display DNS cache |
| `ipconfig /registerdns` | Register DNS records |

---

# 4. Connectivity Testing Commands

## 4.1 ping

The `ping` command tests reachability by sending ICMP Echo Request messages and waiting for responses.

### Syntax

```cmd
ping [options] destination
```

### Basic example

```cmd
ping google.com
```

Tests whether the destination responds to ICMP Echo Requests.

Example output:

```text
Pinging google.com with 32 bytes of data:

Reply from 142.250.183.14: bytes=32 time=20ms TTL=116
Reply from 142.250.183.14: bytes=32 time=19ms TTL=116
```

### Ping an IP address

```cmd
ping 8.8.8.8
```

This tests IP connectivity without depending on DNS resolution for the destination name.

### Important ping options

| Option | Purpose |
|---|---|
| `-t` | Ping continuously until interrupted |
| `-n` | Specify number of requests |
| `-l` | Specify packet size in bytes |
| `-4` | Force IPv4 |
| `-6` | Force IPv6 |
| `-a` | Resolve an address to a hostname |
| `-w` | Set timeout in milliseconds |
| `-f` | Set Don't Fragment flag for IPv4 |

### Continuous ping

```cmd
ping -t google.com
```

Stop using:

`Ctrl + C`

### Send five requests

```cmd
ping -n 5 google.com
```

### Change packet size

```cmd
ping -l 1000 google.com
```

### Force IPv4

```cmd
ping -4 google.com
```

### Force IPv6

```cmd
ping -6 google.com
```

### Important concepts

- **Latency:** Time taken for a response, usually measured in milliseconds.
- **Packet loss:** Percentage of packets that do not receive responses.
- **TTL:** Time To Live, a field that limits how many router hops a packet can traverse.

**Important:** A failed ping does not always mean a server is offline. Firewalls and network policies may block ICMP traffic.

---

## 4.2 tracert

The `tracert` command traces the route packets take towards a destination.

It helps identify where delays or connectivity problems may occur.

### Syntax

```cmd
tracert [options] destination
```

### Example

```cmd
tracert google.com
```

Displays the intermediate network hops between your computer and the destination.

### Useful options

| Option | Purpose |
|---|---|
| `-d` | Do not resolve IP addresses into hostnames |
| `-h` | Set maximum number of hops |
| `-w` | Set timeout in milliseconds |
| `-4` | Force IPv4 |
| `-6` | Force IPv6 |

### Skip hostname resolution

```cmd
tracert -d google.com
```

### Limit maximum hops

```cmd
tracert -h 15 google.com
```

### Set timeout

```cmd
tracert -w 1000 google.com
```

### Understanding output

Each numbered line represents a hop.

A hop is generally a router or network device that forwards traffic.

If a hop displays `* * *`, the device may not be responding to the probe. It does not necessarily mean the route is broken.

---

## 4.3 pathping

`pathping` combines route tracing with packet-loss analysis.

It sends multiple probes and estimates packet loss at different network hops.

### Syntax

```cmd
pathping destination
```

### Example

```cmd
pathping google.com
```

### Useful options

| Option | Purpose |
|---|---|
| `-n` | Do not resolve addresses into hostnames |
| `-h` | Specify maximum hops |
| `-g` | Specify a loose source route |
| `-p` | Wait interval between pings |
| `-q` | Specify number of queries per hop |
| `-w` | Set timeout in milliseconds |
| `-4` | Force IPv4 |
| `-6` | Force IPv6 |

Example:

```cmd
pathping -n -q 20 google.com
```

This performs packet-loss analysis using 20 queries per hop without hostname resolution.

**Note:** Pathping can take several minutes to finish.

---

# 5. DNS Commands

## 5.1 nslookup

`nslookup` is used to query DNS servers.

It helps investigate domain name resolution.

### Basic syntax

```cmd
nslookup domain
```

### Find IP address of a domain

```cmd
nslookup google.com
```

### Find DNS information using a specific DNS server

```cmd
nslookup google.com 8.8.8.8
```

Here, `8.8.8.8` is the DNS server being queried.

### Reverse DNS lookup

```cmd
nslookup 8.8.8.8
```

Attempts to find a hostname associated with an IP address through reverse DNS records.

### Interactive mode

```cmd
nslookup
```

You can now enter queries interactively.

Exit using:

```text
exit
```

### Query specific DNS record types

Inside interactive mode:

```text
set type=A
google.com
```

### Common DNS record types

| Record | Meaning |
|---|---|
| A | Maps a hostname to an IPv4 address |
| AAAA | Maps a hostname to an IPv6 address |
| MX | Mail exchange server |
| NS | Authoritative name server |
| CNAME | Canonical name alias |
| TXT | Text information, often used for verification |
| PTR | Reverse DNS record |
| SOA | Start of Authority information |

Examples:

```text
set type=MX
example.com
```

```text
set type=NS
example.com
```

```text
set type=TXT
example.com
```

To leave interactive mode:

```text
exit
```

---

# 6. Network Connection Monitoring

## 6.1 netstat

`netstat` displays network connections, listening ports, routing information and protocol statistics.

### Basic syntax

```cmd
netstat [options]
```

### Display active connections

```cmd
netstat
```

### Display all connections and listening ports

```cmd
netstat -a
```

### Display addresses numerically

```cmd
netstat -n
```

Avoids resolving IP addresses and port numbers into names.

### Display process IDs

```cmd
netstat -o
```

Displays the PID associated with each connection.

### Display executable names

```cmd
netstat -b
```

Displays the executable involved in creating each connection.

This may require administrator privileges.

### Display listening ports

```cmd
netstat -an
```

### Display routing table

```cmd
netstat -r
```

### Display protocol statistics

```cmd
netstat -s
```

### Display TCP connections

```cmd
netstat -p tcp
```

### Display UDP connections

```cmd
netstat -p udp
```

### Combine options

```cmd
netstat -ano
```

Displays all connections and listening ports numerically, along with their PIDs.

### Identify the process using a port

First:

```cmd
netstat -ano
```

Find the PID associated with the port.

Then:

```cmd
tasklist /FI "PID eq 1234"
```

Replace `1234` with the actual PID.

### Important netstat terms

| Term | Meaning |
|---|---|
| LISTENING | Waiting for incoming connections |
| ESTABLISHED | Connection has been established |
| TIME_WAIT | Connection is waiting before final closure |
| CLOSE_WAIT | Remote side has closed; local application has not fully closed |
| SYN_SENT | Connection request has been sent |
| UDP | Connectionless transport protocol |

**Important:** A listening port is not automatically a security vulnerability. Its exposure depends on the interface, firewall rules and service configuration.

---

# 7. ARP Commands

## 7.1 arp

ARP stands for Address Resolution Protocol.

ARP helps resolve an IPv4 address into a MAC address on a local network.

### Display ARP cache

```cmd
arp -a
```

Displays known IPv4-to-MAC address mappings.

### Display ARP cache for a specific interface

```cmd
arp -a -N 192.168.1.10
```

Replace the address with the local interface IPv4 address.

### Delete an ARP entry

```cmd
arp -d 192.168.1.1
```

Removes a specific entry from the ARP cache.

### Delete all ARP entries

```cmd
arp -d *
```

**Warning:** This clears the ARP cache. Entries will be relearned as needed.

### Add a static ARP entry

```cmd
arp -s 192.168.1.50 00-AA-BB-CC-DD-EE
```

Associates an IPv4 address with a MAC address.

Static ARP entries should only be configured when you understand the network requirements.

---

# 8. Routing Commands

## 8.1 route

The `route` command displays and modifies the IP routing table.

The routing table determines where network packets are forwarded.

### Display routing table

```cmd
route print
```

### Display IPv4 routes

```cmd
route print -4
```

### Display IPv6 routes

```cmd
route print -6
```

### Add a route

```cmd
route add 192.168.2.0 mask 255.255.255.0 192.168.1.1
```

Adds a route to the specified destination network through the specified gateway.

### Add a persistent route

```cmd
route -p add 192.168.2.0 mask 255.255.255.0 192.168.1.1
```

The `-p` option makes the route persistent across system restarts.

### Delete a route

```cmd
route delete 192.168.2.0
```

### Change an existing route

```cmd
route change 192.168.2.0 mask 255.255.255.0 192.168.1.254
```

### Important route concepts

- Destination: Network or host being reached.
- Netmask: Identifies the destination network.
- Gateway: Next-hop router.
- Interface: Local network interface used.
- Metric: Cost used when selecting routes.

**Warning:** Incorrect routing changes can disconnect your computer from network resources. Administrative privileges may be required.

---

# 9. MAC Address Commands

## 9.1 getmac

The `getmac` command displays MAC addresses associated with network adapters.

### Basic command

```cmd
getmac
```

### Detailed output

```cmd
getmac /v
```

### Table format

```cmd
getmac /fo table
```

### CSV format

```cmd
getmac /fo csv
```

### List remote computer adapters

```cmd
getmac /s COMPUTERNAME
```

Remote queries may require appropriate permissions and network configuration.

### Common options

| Option | Purpose |
|---|---|
| `/v` | Verbose output |
| `/fo table` | Table format |
| `/fo list` | List format |
| `/fo csv` | CSV format |
| `/s` | Specify remote computer |
| `/u` | Specify user credentials |
| `/p` | Specify password |

Avoid exposing MAC addresses unnecessarily because they can reveal information about your network devices.

---

# 10. NetBIOS Commands

## 10.1 nbtstat

`nbtstat` displays NetBIOS over TCP/IP information.

NetBIOS is a legacy networking system used by some Windows network environments.

Modern networks often rely more heavily on DNS and direct TCP/IP communication.

### Display local NetBIOS names

```cmd
nbtstat -n
```

### Display NetBIOS cache

```cmd
nbtstat -c
```

### Query a remote computer by name

```cmd
nbtstat -a COMPUTERNAME
```

### Query a remote computer by IP

```cmd
nbtstat -A 192.168.1.10
```

### Purge and reload cache

```cmd
nbtstat -R
```

### Release and refresh NetBIOS names

```cmd
nbtstat -RR
```

### Important options

| Option | Purpose |
|---|---|
| `-n` | Display local NetBIOS names |
| `-c` | Display NetBIOS cache |
| `-a` | Query a remote computer by name |
| `-A` | Query a remote computer by IP |
| `-R` | Purge and reload remote cache |
| `-RR` | Release and refresh NetBIOS names |

---

# 11. Hostname Command

## 11.1 hostname

Displays the computer's network hostname.

```cmd
hostname
```

Example:

```text
DESKTOP-ABC123
```

The hostname is useful when identifying a computer on a network.

---

# 12. Network Sharing Commands

## 12.1 net view

Displays computers or shared resources visible on a network.

```cmd
net view
```

### View shared resources on a computer

```cmd
net view \\COMPUTERNAME
```

Network discovery, permissions and firewall configuration can affect the results.

## 12.2 net use

Manages network connections to shared resources.

### Display network connections

```cmd
net use
```

### Connect to a shared folder

```cmd
net use Z: \\SERVER\SharedFolder
```

Maps a shared folder to drive letter Z.

### Disconnect a mapped drive

```cmd
net use Z: /delete
```

### Remove all network connections

```cmd
net use * /delete
```

**Warning:** The final command disconnects all applicable network connections managed by `net use`.

---

# 13. HTTP and Web Testing Commands

## 13.1 curl

Modern Windows versions include `curl`.

It is a command-line tool used to transfer data through URLs.

It supports HTTP, HTTPS and several other protocols.

### Basic GET request

```cmd
curl https://example.com
```

Downloads the response body and displays it.

### Display response headers

```cmd
curl -I https://example.com
```

Sends a HEAD request and displays response headers.

### Follow redirects

```cmd
curl -L https://example.com
```

Follows HTTP redirects.

### Save response to a file

```cmd
curl -o response.html https://example.com
```

Saves the response body into a file.

### Display detailed connection information

```cmd
curl -v https://example.com
```

Displays verbose connection and protocol information.

### Important HTTP concepts

| Term | Meaning |
|---|---|
| GET | Retrieve a resource |
| POST | Submit data |
| PUT | Replace or create a resource |
| PATCH | Partially update a resource |
| DELETE | Delete a resource |
| HTTP | Hypertext Transfer Protocol |
| HTTPS | HTTP protected by TLS |

Be careful when using verbose output because it may contain sensitive request or response information.

---

# 14. Testing TCP Ports

## 14.1 PowerShell Test-NetConnection

`Test-NetConnection` is a PowerShell command, not a native CMD command.

However, it can be executed from CMD using PowerShell.

### Test basic connectivity

```cmd
powershell -NoProfile -Command "Test-NetConnection google.com"
```

### Test a specific TCP port

```cmd
powershell -NoProfile -Command "Test-NetConnection google.com -Port 443"
```

### Test a web server port

```cmd
powershell -NoProfile -Command "Test-NetConnection example.com -Port 80"
```

Important output:

- `ComputerName`: Target hostname.
- `RemoteAddress`: Resolved destination IP.
- `RemotePort`: Destination port.
- `TcpTestSucceeded`: Whether the TCP connection test succeeded.

A successful TCP test does not guarantee that the application behind the port is functioning correctly.

## 14.2 Telnet

Telnet is an older protocol that can establish terminal sessions over TCP.

It is not secure for transmitting credentials because it does not provide encryption.

The Telnet Client is an optional Windows feature and may not be installed.

If enabled:

```cmd
telnet example.com 80
```

Use modern secure protocols such as SSH instead of Telnet for remote administration.

For basic TCP port testing, `Test-NetConnection` is generally preferable.

---

# 15. Netsh Commands

## 15.1 netsh

`netsh` stands for Network Shell.

It is a Windows command-line utility used to inspect and configure network settings.

### Display network interfaces

```cmd
netsh interface show interface
```

### Display IPv4 configuration

```cmd
netsh interface ipv4 show config
```

### Display IPv6 configuration

```cmd
netsh interface ipv6 show config
```

### Display interface IP addresses

```cmd
netsh interface ip show addresses
```

### Display Wi-Fi interfaces

```cmd
netsh wlan show interfaces
```

Displays information such as:

- Wi-Fi interface name.
- Connection state.
- SSID.
- Radio type.
- Channel.
- Signal quality.

### Display saved Wi-Fi profile names

```cmd
netsh wlan show profiles
```

Displays saved wireless network profile names.

Do not publish sensitive network configuration or use commands that reveal stored Wi-Fi credentials.

### Display firewall configuration

```cmd
netsh advfirewall show allprofiles
```

Displays Windows Defender Firewall profile configuration.

### Reset Winsock catalog

```cmd
netsh winsock reset
```

Resets the Winsock catalog.

**Warning:** This changes network configuration and may require a restart. Use it only when troubleshooting justifies it.

### Reset TCP/IP configuration

```cmd
netsh int ip reset
```

Resets TCP/IP configuration settings.

**Warning:** This can affect network configuration and may require restarting Windows. Do not run it as a routine maintenance command.

---

# 16. Combining Networking Commands

CMD supports pipes and output redirection, allowing networking commands to be combined.

## 16.1 Using findstr

Find a particular port:

```cmd
netstat -ano | findstr :443
```

Find a particular IP address:

```cmd
ipconfig | findstr IPv4
```

Find listening connections:

```cmd
netstat -an | findstr LISTENING
```

## 16.2 Save network information to a file

Save IP configuration:

```cmd
ipconfig /all > network-info.txt
```

Append network connections:

```cmd
netstat -ano >> network-info.txt
```

Save route information:

```cmd
route print >> network-info.txt
```

## 16.3 Display only DNS server information

```cmd
ipconfig /all | findstr /i "DNS Servers"
```

The `/i` option makes the search case-insensitive.

---

# 17. Network Troubleshooting Guide

The following table connects common symptoms with useful diagnostic commands.

| Problem | Command |
|---|---|
| Find local IP address | `ipconfig` |
| Find full network configuration | `ipconfig /all` |
| Check IP connectivity | `ping 8.8.8.8` |
| Check DNS resolution | `nslookup google.com` |
| Clear DNS cache | `ipconfig /flushdns` |
| Trace network path | `tracert google.com` |
| Analyze packet loss | `pathping google.com` |
| Find active connections | `netstat -ano` |
| Find listening ports | `netstat -an` |
| Find MAC addresses | `getmac` |
| Inspect ARP cache | `arp -a` |
| Inspect routing table | `route print` |
| Inspect Wi-Fi connection | `netsh wlan show interfaces` |

## 17.1 No Internet Connectivity

Possible causes:

- Wi-Fi disconnected.
- Router problem.
- Incorrect IP configuration.
- Gateway unavailable.
- ISP outage.
- Firewall or security software restrictions.

Useful commands:

```cmd
ipconfig /all
ping 127.0.0.1
ping 192.168.1.1
ping 8.8.8.8
```

Replace `192.168.1.1` with your actual default gateway.

## 17.2 DNS Resolution Failure

Symptoms:

- Websites fail to load by domain name.
- Direct IP connectivity may still work.
- DNS lookup fails.

Commands:

```cmd
nslookup google.com
ipconfig /displaydns
ipconfig /flushdns
```

## 17.3 APIPA Address

An address in the range:

`169.254.0.0/16`

is an IPv4 link-local address.

Windows may assign this type of address when it cannot obtain an IPv4 address from DHCP.

Possible causes:

- DHCP server unavailable.
- Router problem.
- Network cable disconnected.
- Wi-Fi authentication or connection failure.

## 17.4 High Latency

Use:

```cmd
ping -n 20 google.com
tracert google.com
pathping google.com
```

High latency can be caused by congestion, routing distance, wireless interference or overloaded network equipment.

## 17.5 Application Port Not Working

Use:

```cmd
netstat -ano
```

Then identify the process:

```cmd
tasklist /FI "PID eq 1234"
```

Replace the PID with the actual process ID.

You can also test a remote TCP port:

```cmd
powershell -NoProfile -Command "Test-NetConnection example.com -Port 443"
```

---

# 18. Networking Security and Safety

Networking commands can reveal sensitive system and network information.

Follow these precautions:

1. Do not scan or probe networks without authorization.
2. Do not expose public IP addresses unnecessarily.
3. Avoid publishing MAC addresses and complete network configuration.
4. Do not modify routing tables without understanding the consequences.
5. Avoid resetting TCP/IP or Winsock unless troubleshooting requires it.
6. Be careful when releasing DHCP configuration because it may disconnect your device.
7. Do not disable the firewall just to test connectivity.
8. Do not expose credentials in command output or screenshots.
9. Use secure protocols such as HTTPS and SSH.
10. Only test services and ports on systems you own or are authorized to assess.

---

# 19. Important Command Comparisons

## ping vs tracert vs pathping

| Command | Main purpose |
|---|---|
| ping | Test reachability and measure response time |
| tracert | Trace intermediate network hops |
| pathping | Analyze route and packet loss |

## ipconfig vs getmac

| Command | Main purpose |
|---|---|
| ipconfig | Displays IP configuration |
| getmac | Displays MAC addresses |

## nslookup vs ping

| Command | Main purpose |
|---|---|
| nslookup | Queries DNS |
| ping | Tests ICMP reachability |

## netstat vs arp

| Command | Main purpose |
|---|---|
| netstat | Displays connections, ports and statistics |
| arp | Displays IPv4-to-MAC address mappings |

## route vs tracert

| Command | Main purpose |
|---|---|
| route | Displays or modifies the routing table |
| tracert | Examines the path towards a destination |

---

# 20. Quick Reference Cheat Sheet

| Command | Description |
|---|---|
| `ipconfig` | Display IP configuration |
| `ipconfig /all` | Display complete network details |
| `ipconfig /flushdns` | Clear DNS cache |
| `ping google.com` | Test reachability |
| `ping -t google.com` | Continuous ping |
| `tracert google.com` | Trace network route |
| `pathping google.com` | Analyze packet loss |
| `nslookup google.com` | Query DNS |
| `netstat -ano` | Show connections and PIDs |
| `netstat -an` | Show numerical connections and ports |
| `arp -a` | Display ARP cache |
| `route print` | Display routing table |
| `getmac` | Display MAC addresses |
| `nbtstat -n` | Display local NetBIOS names |
| `hostname` | Display computer hostname |
| `net view` | Display network computers |
| `net use` | Manage network connections |
| `curl https://example.com` | Make an HTTP request |
| `netsh wlan show interfaces` | Display Wi-Fi information |

---

# 21. Important Networking Terminology

| Term | Full form / Meaning |
|---|---|
| IP | Internet Protocol |
| IPv4 | Internet Protocol Version 4 |
| IPv6 | Internet Protocol Version 6 |
| MAC | Media Access Control |
| DNS | Domain Name System |
| DHCP | Dynamic Host Configuration Protocol |
| TCP | Transmission Control Protocol |
| UDP | User Datagram Protocol |
| ICMP | Internet Control Message Protocol |
| ARP | Address Resolution Protocol |
| LAN | Local Area Network |
| WAN | Wide Area Network |
| HTTP | Hypertext Transfer Protocol |
| HTTPS | Hypertext Transfer Protocol Secure |
| TTL | Time To Live |
| ISP | Internet Service Provider |
| NAT | Network Address Translation |
| VPN | Virtual Private Network |
| NIC | Network Interface Card |
| APIPA | Automatic Private IP Addressing |

---

# 22. Official Documentation and References

1. [Microsoft - ipconfig](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ipconfig)
2. [Microsoft - ping](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ping)
3. [Microsoft - tracert](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/tracert)
4. [Microsoft - pathping](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/pathping)
5. [Microsoft - nslookup](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/nslookup)
6. [Microsoft - netstat](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/netstat)
7. [Microsoft - arp](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/arp)
8. [Microsoft - route](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/route_ws2008)
9. [Microsoft - getmac](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/getmac)
10. [Microsoft - nbtstat](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/nbtstat)
11. [Microsoft - netsh](https://learn.microsoft.com/en-us/windows-server/networking/technologies/netsh/netsh)
12. [Microsoft - curl documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/curl)

---

# 23. Key Takeaways

- `ipconfig` is used to inspect IP configuration.
- `ping` checks ICMP reachability.
- `tracert` traces network hops.
- `pathping` investigates packet loss along a route.
- `nslookup` investigates DNS resolution.
- `netstat` inspects network connections and ports.
- `arp` examines local IPv4-to-MAC mappings.
- `route` manages the routing table.
- `getmac` displays network adapter MAC addresses.
- `netsh` provides advanced Windows network configuration.
- `curl` is useful for testing HTTP and HTTPS requests.

**Lesson 07 completed — Networking Commands in Windows CMD.**
