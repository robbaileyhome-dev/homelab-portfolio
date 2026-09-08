# Lab02: Active Directory setup 

## Objective
The Old Millington Gazette is a remarkably lean operation, running with just a single reporter and an IT administrator. Even so, they both need logins and appropriate user permissions. 

## Network Architecture
```text
                           [ VirtualBox NAT / Host-Only Network ]
                                 The Old Millington Gazette
                                Subnet range: 192.168.0.0/24
                                               |
        +--------------------------------------+---------------------------------+

        |                                      |                                 |
        v                                      v                                 v
+------------------------------+ +------------------------------+ +------------------------------+

|  Windows Server 2025         | |  Windows 11 Client           | |  Linux Mint Client           |
|  NEWSRV01                    | |  Reporter                    | |  itadmin                     |
|  Role: Domain / DHCP / DNS   | |  Role: Newsroom WS           | |  Role: SysAdmin/Mgmt         |
|  4GB, 2 cores                | |  4GB, 2 cores                | |  2GB, 2 cores                |
|  IP: 192.168.0.10            | |  IP: 192.168.0.100           | |  IP: 192.168.0.101           |
+------------------------------+ +------------------------------+ +------------------------------+
```

---
