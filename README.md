# homelab-portfolio
I am a journalist and senior lecturer retraining in IT / Cyber / AI.

I am building a virtual newsroom lab for the *Old Millington Gazette* with AD, DNS and DHCP for Network+ and Security+

The isolated, self-contained network will be built with VMs on a GEEKOM A8 (Ryzen 7 8745HS, 16GB) using VirtualBox.

**Focus:** CompTIA Network+, Security+ and AWS Certified AI Practitioner

## Network topology blueprint
```text
                           [ VirtualBox NAT / Host-Only Network ]
                                 The Old Millington Gazette
                                Subnet range: 192.168.0.0/24
                           +------------------------------------+
                           |           Ubuntu server            |
                           |     Gateway, Domain, DHCP, DNS     |
                           |          IP: 192.168.0.10          |
                           +------------------------------------+
                                               |
           +-----------------------+----------------------+-----------------------+
           |                       |                      |                       |
           v                       v                      v                       v
+---------------------+ +---------------------+ +---------------------+ +---------------------+
|  Linux client       | |  Linux client       | |  Linux client       | |  Linux client       |
|  editor-01          | |  reporter-01        | |  it-admin-01        | |  sales-01           |
|  1GB, 1 core        | |  1GB, 1 core        | |  2GB, 1 core        | |  1GB, 1 core        |
|  IP: 192.168.0.150  | |  IP: 192.168.0.151  | |  IP: 192.168.0.101  | |  IP: 192.168.0.200  |
+---------------------+ +---------------------+ +---------------------+ +---------------------+
```

### Tools
VirtualBox, Ubuntu Server, Linux Mint, Debian

### Labs
- [ ] Lab 01 - [Two nodes, static IPs - OSI Layers 1-3](https://github.com/robbaileyhome-dev/homelab-portfolio/blob/main/Labs/Lab01%20Network%20setup.md)
- [ ] Lab 02 - DHCP and DNS
- [ ] Lab 03 - Segmentation - VLANs
- [ ] Lab 04 - Directory services - authentication
- [ ] Lab 05 - File / print - shared resources
- [ ] Lab 06 - Network monitoring
- [ ] Lab 07 - Troubleshooting

### What I'm learning
- Networking: DNS, DHCP, subnetting
- Security: Domains, authentication, group policy, network monitoring
- Documentation: Break/fix troubleshooting

Connect on LinkedIn: https://www.linkedin.com/in/rob-j-bailey-/
