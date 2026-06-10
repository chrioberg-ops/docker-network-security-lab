# Network Topology

## Overview

The Docker Network Security Lab is built around a segmented network architecture designed to simulate an enterprise environment.

The environment contains three isolated network zones:

| Network            | Subnet        | Purpose                     |
| ------------------ | ------------- | --------------------------- |
| Management Network | 172.20.0.0/24 | Administrative systems      |
| Internal Network   | 172.21.0.0/24 | Routing and transit network |
| DMZ Network        | 172.22.0.0/24 | Public-facing services      |

## Network Layout

```text
test-mgmt
172.20.0.100
      |
Management Network
172.20.0.0/24
      |
Router1
172.20.0.5
172.21.0.2
      |
Internal Network
172.21.0.0/24
      |
Router2
172.21.0.3
172.22.0.5
      |
DMZ Network
172.22.0.0/24
      |
webserver-dmz
172.22.0.100
```

## Routing

### Router1

Static route:

```text
172.22.0.0/24 via 172.21.0.3
```

### Router2

Static route:

```text
172.20.0.0/24 via 172.21.0.2
```

## Security Services

### Authelia

Provides Single Sign-On (SSO) and centralized authentication.

### WireGuard

Provides secure VPN access to the environment.

### ClamAV

Provides malware scanning capabilities.

## Validation

Network functionality was validated using:

* Ping
* Traceroute
* Route inspection

Traffic successfully traversed:

```text
test-mgmt
→ Router1
→ Router2
→ webserver-dmz
```

confirming correct routing between all network segments.
