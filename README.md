# Docker Network Security Lab

## Project Overview

This project demonstrates the design and implementation of a segmented enterprise-style network using Docker containers. The environment simulates a real-world infrastructure with separate network zones, static routing, centralized authentication, VPN access, malware scanning, and a web server hosted in a DMZ.

The goal of the project was to gain practical experience with Linux networking, Docker networking, routing, network segmentation, and security-focused services commonly used in enterprise environments.

### Key Features

* Segmented network architecture
* Management, Internal, and DMZ network zones
* Static routing between network segments
* WireGuard VPN access
* Authelia Single Sign-On (SSO)
* ClamAV malware scanning
* Nginx web server hosted in DMZ
* Network validation using ping and traceroute
* Docker-based infrastructure

---

## Architecture

The environment consists of three isolated network segments connected through dedicated routing containers.

### Network Zones

| Network            | Subnet        | Purpose                  |
| ------------------ | ------------- | ------------------------ |
| Management Network | 172.20.0.0/24 | Administrative systems   |
| Internal Network   | 172.21.0.0/24 | Internal routing segment |
| DMZ Network        | 172.22.0.0/24 | Public-facing services   |

### Components

| Component     | IP Address              |
| ------------- | ----------------------- |
| test-mgmt     | 172.20.0.100            |
| Router1       | 172.20.0.5 / 172.21.0.2 |
| Router2       | 172.21.0.3 / 172.22.0.5 |
| webserver-dmz | 172.22.0.100            |

---

## Network Segmentation

The environment is divided into three separate network zones to simulate enterprise network segmentation.

### Management Network

Administrative access and management traffic.

```text
172.20.0.0/24
```

### Internal Network

Transit network used between routers.

```text
172.21.0.0/24
```

### DMZ Network

Hosts public-facing services while remaining isolated from the management network.

```text
172.22.0.0/24
```

Traffic between zones is controlled through static routing.

---

## Security Components

### Authelia

Authelia provides centralized authentication and Single Sign-On (SSO) functionality.

Features:

* Centralized authentication
* User access control
* Session management
* Security policy enforcement

### WireGuard

WireGuard provides secure VPN access to the environment.

Features:

* Encrypted communication
* Remote administrative access
* Lightweight VPN implementation

### ClamAV

ClamAV provides malware scanning capabilities.

Features:

* Malware detection
* Signature updates
* Security monitoring

### DMZ Web Server

The DMZ contains an Nginx web server isolated from the management network.

Benefits:

* Reduced attack surface
* Service isolation
* Controlled access paths

---

## Routing Validation

Static routes were configured between Router1 and Router2.

### Router1

```text
172.22.0.0/24 via 172.21.0.3
```

### Router2

```text
172.20.0.0/24 via 172.21.0.2
```

Validation was performed using:

* Ping
* Traceroute
* Route inspection

Successful communication was verified between:

```text
test-mgmt
↓
Router1
↓
Router2
↓
webserver-dmz
```

Traceroute confirmed that packets traversed both routers before reaching the destination.

---

## Screenshots

### Environment Overview

![Containers](screenshots/01-docker-containers-running.png)

### Docker Networks

![Networks](screenshots/02-docker-networks.png)

### Router1 IP Configuration

![Router1 IP](screenshots/03-router1-ip-addresses.png)

### Router2 IP Configuration

![Router2 IP](screenshots/04-router2-ip-addresses.png)

### Router1 Routing Table

![Router1 Routes](screenshots/05-router1-routing-table.png)

### Router2 Routing Table

![Router2 Routes](screenshots/06-router2-routing-table.png)

### Routing Validation

![Ping Test](screenshots/07-routing-ping-test.png)

### Traceroute Verification

![Traceroute](screenshots/08-routing-traceroute.png)

### Authelia Service

![Authelia](screenshots/09-authelia-container-status.png)

### WireGuard Service

![WireGuard](screenshots/10-wireguard-container-status.png)

### ClamAV Service

![ClamAV](screenshots/11-clamav-container-status.png)

### DMZ Web Server

![DMZ Web Server](screenshots/12-dmz-webserver-running.png)

### Network Topology

![Network Topology](screenshots/13-network-topology-diagram.png)

---

## Lessons Learned

This project provided hands-on experience with:

* Docker networking
* Multi-network container deployments
* Linux routing
* Static route configuration
* VPN deployment
* Authentication services
* Malware scanning
* Network troubleshooting
* Enterprise network segmentation

One of the most valuable aspects of the project was troubleshooting connectivity issues and restoring routing functionality after the environment had been offline for an extended period. This reinforced practical networking skills and systematic troubleshooting techniques.

---

## Technologies Used

### Infrastructure

* Docker
* Docker Networks
* Alpine Linux

### Networking

* Static Routing
* ICMP
* Traceroute
* TCP/IP

### Security

* Authelia
* WireGuard
* ClamAV

### Services

* Nginx
* SSH

### Operating System

* Ubuntu Server

---

## Author

**Christoffer Öberg**

Project created as part of a network security and systems administration learning portfolio.
