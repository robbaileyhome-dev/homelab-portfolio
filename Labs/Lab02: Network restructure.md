# Lab02: Reconfiguring the network

## Background and objective
My initial goal here was to add the rest of the machines to the *Old Millington Gazette* network but I immediately hit RAM bandwidth issues on my 16GB host. I was forced to rethink my network topography to reduce the number of nodes and find lightweight solutions for key network services. So my new goal became configuring a pfSense router for subnetting, firewall and as a DHCP and DNS server for the network. I also reconfigured my it-admin01 client into the new network structure and tested its connection to pfSense.

## Blueprint
```mermaid
graph TB
    NAT["Internet<br/>(VirtualBox NAT)"]
    pfSense["pfSense Router/Firewall<br/>WAN: DHCP (10.0.2.15)<br/>newsroom-lanA: 192.168.10.1/24<br/>newsroom-lanB: 192.168.20.1/24<br/>Domain: omgnews.test"]
    Mint["it-admin01 (Linux Mint)<br/>192.168.10.101<br/>Admin workstation / diagnostics"]
    Ubuntu["newssrvr1 (Ubuntu Server) — PENDING<br/>Planned: 192.168.10.10<br/>Role: DNS"]
    Mint["newsroom-client01 (Linux Mint) — PENDING<br/>Planned: 192.168.20.0/24 (DHCP)<br/>Role: End-user client"]

    NAT --> pfSense
    pfSense -->|newsroom-lanA| Mint
    pfSense -.->|newsroom-lanA planned| Ubuntu
    pfSense -.->|newsroom-lanB planned| Mint

    classDef live fill:#d4edda,stroke:#28a745,color:#000;
    classDef pending fill:#f8f9fa,stroke:#adb5bd,stroke-dasharray: 5 5,color:#666;
    class NAT,pfSense,Mint live;
    class Ubuntu,Mint pending;
```

---

## Evidence
to come

### Troubleshooting 
to come
