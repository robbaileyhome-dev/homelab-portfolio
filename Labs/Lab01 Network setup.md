# Lab 1: Isolated Virtual Newsroom Network Infrastructure

## Objective
To plan and deploy a secure, completely isolated sandbox environment inside VirtualBox to serve as the baseline infrastructure for my virtual newsroom. All VMS are running on a GEEKOM A8 Ryzen 7 8745HS, 16GB.

## Network Architecture

                         [ VirtualBox NAT / Host-Only Network ]
                             **The Old Millington Gazette**
                              Subnet range: 192.168.0.0/24
                                            |
           +--------------------------------+--------------------------------+
           |                                |                                |
           v                                v                                v
+------------------------------+ +------------------------------+ +------------------------------+
|  Windows Server 2025         | |  Windows 11 Client           | |  Linux Mint Client           |
|  NEWSRV01                    | |  Reporter                    | |  itadmin                     |
|  Role: Domain / DHCP / DNS   | |  Role: Newsroom WS           | |  Role: SysAdmin/Mgmt         |
|  4GB, 2 cores                | |  4GB, 2 cores                | |  2GB, 2 cores                |
|  IP: 192.168.0.10            | |  IP: 192.168.0.100           | |  IP: 192.168.0.101           |
+------------------------------+ +------------------------------+ +------------------------------+

---

## Evidence of Isolation & Connectivity

### Verification 1: Internal Inter-VM Connectivity
Proving the Windows 11 client can successfully talk to the Linux Mint client over the private switch.

```cmd
C:\Users\Reporter> ping 192.168.0.101

Pinging 192.168.0.101 with 32 bytes of data:
Reply from 192.168.0.101: bytes=32 time=1ms TTL=64
Reply from 192.168.0.101: bytes=32 time<1ms TTL=64
Reply from 192.168.0.101: bytes=32 time=1ms TTL=64
Reply from 192.168.0.101: bytes=32 time<1ms TTL=64

Ping statistics for 192.168.0.101:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

### Verification 2: Strict Network Isolation Proof (LAN Boundary Check)
To prove the virtual newsroom cannot leak malicious traffic into the physical production home network, a cross-boundary ping was attempted from the Linux Admin VM (`192.168.0.101`) to the physical host's home router gateway (`192.168.1.254`).

```bash
itadmin@rob-VirtualBox:~\$ ping -c 3 192.168.1.254
ping: connect: Network is unreachable
```
* **Analysis:** The `Network is unreachable` error explicitly confirms that the VM has no routing path out of the VirtualBox private switch, proving absolute network isolation from the host LAN.

### Verification 3: VirtualBox Configuration Overview
<img width="1298" height="813" alt="Image" src="https://github.com/user-attachments/assets/c565bcc9-bbdb-4f91-abb1-857ef911e150" />
*Figure: Screenshot highlighting the internal/host-only switch assignment bindings applied to all three instances.*
