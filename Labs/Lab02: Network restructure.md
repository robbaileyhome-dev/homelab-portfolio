# Lab02: Reconfiguring the network

## Background and objective
My initial goal here was to add the rest of the machines to the *Old Millington Gazette* network but I immediately hit RAM bandwidth issues on my 16GB host. I was forced to rethink my network topography to reduce the number of nodes and find lightweight solutions for key network services. So my new goal became configuring a pfSense router for subnetting, firewall and as a DHCP and DNS server for the network. I also reconfigured my it-admin01 client into the new network structure and tested its connection to pfSense.

## Blueprint
```mermaid
graph TB
    subgraph WAN["Internet (NAT)"]
        NAT[VirtualBox NAT]
    end

    subgraph FW["pfSense (Firewall/Router)"]
        pfSense["pfSense<br/>WAN | newsroom-lanA: 192.168.10.1/24 | newsroom-lanB: 192.168.20.1/24"]
    end

    subgraph LANA["newsroom-lanA: Admin Segment (192.168.10.0/24)"]
        Ubuntu["newssrvr1 (Ubuntu Server)<br/>192.168.10.10<br/>Role: DNS"]
        Mint["it-admin01 (Linux Mint)<br/>192.168.10.101<br/>Role: Admin workstation / diagnostics"]
    end

    subgraph LANB["newsroom-lanB: Newsroom Segment (192.168.20.0/24)"]
        Mint["news-ed01 (Linux Mint)<br/>192.168.20.50 (DHCP)<br/>Role: End-user client"]
    end
```

---

## Evidence
to come

### Troubleshooting 
to come
