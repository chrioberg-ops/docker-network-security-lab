# Docker Network Security Lab

A Docker-based enterprise network environment designed to simulate real-world network segmentation and security controls.

This project demonstrates how Docker can be used to build a multi-segment network with dedicated routing, authentication, VPN access, malware scanning, and a DMZ-hosted web application.

---

# Why This Project?

The goal of this project was to gain hands-on experience with:

* Linux administration
* Docker networking
* Static routing
* Network segmentation
* VPN technologies
* Authentication systems
* Security monitoring
* Infrastructure troubleshooting

---

# Skills Demonstrated

* Linux Administration
* Docker Networking
* Static Routing
* Network Segmentation
* WireGuard VPN
* Authelia SSO
* ClamAV Malware Scanning
* Network Troubleshooting
* Technical Documentation

---

# Infrastructure Overview

The environment consists of multiple Docker containers connected through isolated network segments.

![Containers](screenshots/01-docker-containers-running.png)

---

# Architecture Overview

The environment consists of three isolated network segments connected by dedicated routing containers.

| Network            | Subnet        | Purpose                     |
| ------------------ | ------------- | --------------------------- |
| Management Network | 172.20.0.0/24 | Administrative systems      |
| Internal Network   | 172.21.0.0/24 | Routing and transit network |
| DMZ Network        | 172.22.0.0/24 | Public-facing services      |

![Network Topology](screenshots/13-network-topology-diagram.png)

---

# Network Segmentation

The lab is divided into three isolated network zones.

![Networks](screenshots/02-docker-networks.png)

### Components

| Component     | Address                 |
| ------------- | ----------------------- |
| test-mgmt     | 172.20.0.100            |
| Router1       | 172.20.0.5 / 172.21.0.2 |
| Router2       | 172.21.0.3 / 172.22.0.5 |
| webserver-dmz | 172.22.0.100            |

---

# Router Configuration

## Router1

Interfaces:

* 172.20.0.5
* 172.21.0.2

![Router1 Interfaces](screenshots/03-router1-ip-addresses.png)

### Routing Table

![Router1 Routes](screenshots/05-router1-routing-table.png)

---

## Router2

Interfaces:

* 172.21.0.3
* 172.22.0.5

![Router2 Interfaces](screenshots/04-router2-ip-addresses.png)

### Routing Table

![Router2 Routes](screenshots/06-router2-routing-table.png)

---

# Routing Validation

Static routes were configured between Router1 and Router2.

### Router1

```text
172.22.0.0/24 via 172.21.0.3
```

### Router2

```text
172.20.0.0/24 via 172.21.0.2
```

### End-to-End Connectivity Test

![Ping Test](screenshots/07-routing-ping-test.png)

### Traceroute Verification

The traceroute confirms traffic traverses both routers before reaching the DMZ host.

![Traceroute](screenshots/08-routing-traceroute.png)

---

# Security Components

## Authelia (SSO)

Provides centralized authentication and Single Sign-On functionality.

![Authelia](screenshots/09-authelia-container-status.png)

---

## WireGuard (VPN)

Provides secure remote access to the environment.

![WireGuard](screenshots/10-wireguard-container-status.png)

---

## ClamAV (Malware Scanning)

Provides malware detection and scanning capabilities.

![ClamAV](screenshots/11-clamav-container-status.png)

---

# DMZ Web Server

The DMZ contains an isolated Nginx web server.

![DMZ Web Server](screenshots/12-dmz-webserver-running.png)

---

# Lessons Learned

This project provided practical experience with:

* Docker networking
* Linux routing
* Enterprise network segmentation
* VPN deployment
* Authentication systems
* Malware scanning
* Network troubleshooting
* Infrastructure documentation

One of the most valuable parts of the project was restoring and troubleshooting the environment after it had been offline, requiring route verification, gateway configuration, connectivity testing, and service validation.

---

# Technologies Used

* Docker
* Ubuntu Server
* Alpine Linux
* WireGuard
* Authelia
* ClamAV
* Nginx
* SSH
* ICMP
* Traceroute
* Static Routing

---

# Author

**Christoffer Öberg**

System Administration & Network Security Portfolio Project
