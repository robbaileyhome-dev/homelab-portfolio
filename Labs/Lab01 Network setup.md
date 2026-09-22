# Lab01: Setting up the network infrastructure

## Objective
Day one for the *Old Millington Gazette*. This is the first in a series of labs in which I am setting up a secure, isolated sandbox network environment. It will simulate a small digital newsroom, with editorial and sales departments and an IT administrator. In this lab I will configure a host-only network in VirtualBox, starting with a server and a Linux client with static IP addresses. I will demonstrate that the devices can ping each other and that they are isolated from my home network.

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
        |  it-admin01         |
        |  2GB, 2 cores       |
        |  IP: 192.168.0.101  |
        +---------------------+
```

---

## Evidence of connectivity & isolation

### Troubleshooting
After setting up newssrvr01 with a static IP address I attempted to ping the virtual network adapter (192.168.0.1) to prove connectivity. The ping failed.
I used diagnostic tools **ip a** and **ip route** to ensure the correct IP configurations were in place and checked VirtualBox settings to ensure the correct host-only adapter was configured on the server. I then checked the Windows host to ensure its firewall settings were not blocking ICMP traffic. In PowerShell I used **Get-NetAdapter** to check the adapter was up and **Get-NetConnectionProfile** to check whether it was using the public profile. This was confirmed to be the issue.

I used the following command to allow ICMP traffic and successfully ping the adapter:

```powershell
New-NetFirewallRule -DisplayName "Allow ICMP from Host-Only Lab" -Protocol ICMPv4 -IcmpType 8 -RemoteAddress 192.168.0.0/24 -Action Allow -Profile Any
```

**Lessons learned:** Host-only adapters are not classified by Windows NLA and so use the default public firewall profile with the highest security settings. 

### Verification 1: Internal inter-VM connectivity
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

### Verification 2: Strict network isolation
To prove the virtual newsroom cannot leak malicious traffic into the home network, a cross-boundary ping was attempted from it-admin01 to the physical host's home router gateway (`192.168.1.254`).

```bash
it-admin01@itadmin01> ping -c 3 192.168.1.254
ping: connect: Network is unreachable
```

**Analysis:** The `Network is unreachable` error explicitly confirms that the VM has no routing path out of the VirtualBox private switch, proving absolute network isolation from the host LAN.

### Verification 3: VirtualBox configuration overview
<img width="1011" height="917" alt="Image" src="https://github.com/user-attachments/assets/b5fea189-3545-4990-b6a7-5ea351fde050" />
*Figure: Screenshot of VirtualBox configuration for Ubuntu Server newssrvr01 and Linux Mint client it-admin01*
