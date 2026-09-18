# Lab01: Isolated Virtual Newsroom Network Infrastructure

## Objective
Start to build a secure, completely isolated sandbox network environment inside VirtualBox. The first step is a server and an admin client configured with static IP addresses. Both are running in VirtualBox on a GEEKOM A8 Ryzen 7 8745HS, 16GB.

## Blueprint
```text
                              [ VirtualBox Host-Only Network ]
                                 The Old Millington Gazette
                                Subnet range: 192.168.0.0/24
                           +------------------------------------+
                           |           Ubuntu server            |
                           |             newssrvr01             |
                           |     Gateway, Domain, DHCP, DNS     |
                           |          IP: 192.168.0.10          |
                           +------------------------------------+
                                               |
                                               v 
                                    +---------------------+
                                    |  Linux Mint client  |
                                    |  it-admin01        |
                                    |  2GB, 2 cores       |
                                    |  IP: 192.168.0.101  |
                                    +---------------------+
```

---

## Evidence of connectivity & isolation

### Verification 1: Internal Inter-VM Connectivity
Proving the Linux Mint client it-admin01 can communicate with newssrvr01.

```bash
it-admin01@itadmin01> ping -c 3 192.168.0.10

PING 192.168.0.10 (192.168.0.10) 56(84) bytes of data.
64 bytes from 192.168.0.10: icmp_seq=1 ttl=64 time=2.10 ms
64 bytes from 192.168.0.10: icmp_seq=2 ttl=64 time=0.799 ms
64 bytes from 192.168.0.10: icmp-seq=3 ttl=64 time=1.15 ms

--- 192.168.0.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2197ms
```

### Verification 2: Strict Network Isolation Proof (LAN Boundary Check)
To prove the virtual newsroom cannot leak malicious traffic into the home network, a cross-boundary ping was attempted from it-admin01 to the physical host's home router gateway (`192.168.1.254`).

```bash
it-admin01@itadmin01> ping -c 3 192.168.1.254
ping: connect: Network is unreachable
```
* **Analysis:** The `Network is unreachable` error explicitly confirms that the VM has no routing path out of the VirtualBox private switch, proving absolute network isolation from the host LAN.

### Verification 3: VirtualBox Configuration Overview
<img width="1011" height="917" alt="Image" src="https://github.com/user-attachments/assets/b5fea189-3545-4990-b6a7-5ea351fde050" />
*Figure: Screenshot of VirtualBox configuration for Ubuntu Server newssrvr01 and Linux Mint client it-admin01*
