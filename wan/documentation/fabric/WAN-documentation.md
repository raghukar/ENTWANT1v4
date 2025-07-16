# WAN

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [ISIS CLNS interfaces](#isis-clns-interfaces)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| WAN | spine | CE1 | 192.168.0.52/24 | - | Provisioned | - |
| WAN | spine | CE2 | 192.168.0.54/24 | - | Provisioned | - |
| WAN | spine | IntAgg1 | 192.168.0.56/24 | - | Provisioned | - |
| WAN | pe | PE1 | 192.168.0.11/24 | - | Provisioned | - |
| WAN | pe | PE2 | 192.168.0.12/24 | - | Provisioned | - |
| WAN | pe | PE3 | 192.168.0.13/24 | - | Provisioned | - |
| WAN | pe | PE4 | 192.168.0.14/24 | - | Provisioned | - |
| WAN | pe | PE5 | 192.168.0.15/24 | - | Provisioned | - |
| WAN | pe | PE6 | 192.168.0.16/24 | - | Provisioned | - |
| WAN | spine | RR1 | 192.168.0.31/24 | - | Provisioned | - |
| WAN | spine | RR2 | 192.168.0.33/24 | - | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 10.0.0.16/30 | 4 | 2 | 50.0 % |
| 10.251.99.0/28 | 16 | 0 | 0.0 % |
| 10.252.99.0/28 | 16 | 0 | 0.0 % |
| 10.254.99.0/28 | 16 | 0 | 0.0 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| WAN | PE1 | 10.0.0.1/32 |
| WAN | PE2 | 10.0.0.2/32 |
| WAN | PE3 | 10.0.0.3/32 |
| WAN | PE4 | 10.0.0.4/32 |
| WAN | PE5 | 10.0.0.5/32 |
| WAN | PE6 | 10.0.0.6/32 |
| WAN | RR1 | 10.0.0.17/32 |
| WAN | RR2 | 10.0.0.18/32 |

### ISIS CLNS interfaces

| POD | Node | CLNS Address |
| --- | ---- | ------------ |
| WAN | PE1 | 49.0000.0000.0100.0001.00 |
| WAN | PE2 | 49.0000.0000.0100.0002.00 |
| WAN | PE3 | 49.0000.0000.0100.0003.00 |
| WAN | PE4 | 49.0000.0000.0100.0004.00 |
| WAN | PE5 | 49.0000.0000.0100.0005.00 |
| WAN | PE6 | 49.0000.0000.0100.0006.00 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
