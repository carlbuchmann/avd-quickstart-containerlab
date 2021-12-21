# AVD_FABRIC

# Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

# Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision |
| --- | ---- | ---- | ------------- | -------- | -------------------------- |
| AVD_FABRIC | l3leaf | leaf1 | 192.168.123.21/24 | cEOS | Provisioned |
| AVD_FABRIC | l3leaf | leaf2 | 192.168.123.22/24 | cEOS | Provisioned |
| AVD_FABRIC | l3leaf | leaf3 | 192.168.123.23/24 | cEOS | Provisioned |
| AVD_FABRIC | l3leaf | leaf4 | 192.168.123.24/24 | cEOS | Provisioned |
| AVD_FABRIC | spine | spine1 | 192.168.123.11/24 | cEOS | Provisioned |
| AVD_FABRIC | spine | spine2 | 192.168.123.12/24 | cEOS | Provisioned |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

## Fabric Switches with inband Management IP
| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

# Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | leaf1 | Ethernet49/1 | spine | spine1 | Ethernet1/1 |
| l3leaf | leaf1 | Ethernet50/1 | spine | spine2 | Ethernet1/1 |
| l3leaf | leaf1 | Ethernet51/1 | mlag_peer | leaf2 | Ethernet51/1 |
| l3leaf | leaf1 | Ethernet52/1 | mlag_peer | leaf2 | Ethernet52/1 |
| l3leaf | leaf2 | Ethernet49/1 | spine | spine1 | Ethernet2/1 |
| l3leaf | leaf2 | Ethernet50/1 | spine | spine2 | Ethernet2/1 |
| l3leaf | leaf3 | Ethernet49/1 | spine | spine1 | Ethernet3/1 |
| l3leaf | leaf3 | Ethernet50/1 | spine | spine2 | Ethernet3/1 |
| l3leaf | leaf3 | Ethernet51/1 | mlag_peer | leaf4 | Ethernet51/1 |
| l3leaf | leaf3 | Ethernet52/1 | mlag_peer | leaf4 | Ethernet52/1 |
| l3leaf | leaf4 | Ethernet49/1 | spine | spine1 | Ethernet4/1 |
| l3leaf | leaf4 | Ethernet50/1 | spine | spine2 | Ethernet4/1 |

# Fabric IP Allocation

## Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 172.31.255.0/24 | 256 | 16 | 6.25 % |

## Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| leaf1 | Ethernet49/1 | 172.31.255.1/31 | spine1 | Ethernet1/1 | 172.31.255.0/31 |
| leaf1 | Ethernet50/1 | 172.31.255.3/31 | spine2 | Ethernet1/1 | 172.31.255.2/31 |
| leaf2 | Ethernet49/1 | 172.31.255.65/31 | spine1 | Ethernet2/1 | 172.31.255.64/31 |
| leaf2 | Ethernet50/1 | 172.31.255.67/31 | spine2 | Ethernet2/1 | 172.31.255.66/31 |
| leaf3 | Ethernet49/1 | 172.31.255.129/31 | spine1 | Ethernet3/1 | 172.31.255.128/31 |
| leaf3 | Ethernet50/1 | 172.31.255.131/31 | spine2 | Ethernet3/1 | 172.31.255.130/31 |
| leaf4 | Ethernet49/1 | 172.31.255.193/31 | spine1 | Ethernet4/1 | 172.31.255.192/31 |
| leaf4 | Ethernet50/1 | 172.31.255.195/31 | spine2 | Ethernet4/1 | 172.31.255.194/31 |

## Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 192.0.255.0/25 | 128 | 2 | 1.57 % |
| 192.0.255.128/25 | 128 | 4 | 3.13 % |

## Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| AVD_FABRIC | leaf1 | 192.0.255.129/32 |
| AVD_FABRIC | leaf2 | 192.0.255.130/32 |
| AVD_FABRIC | leaf3 | 192.0.255.131/32 |
| AVD_FABRIC | leaf4 | 192.0.255.132/32 |
| AVD_FABRIC | spine1 | 192.0.255.1/32 |
| AVD_FABRIC | spine2 | 192.0.255.2/32 |

## VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 192.0.254.0/24 | 256 | 4 | 1.57 % |

## VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| AVD_FABRIC | leaf1 | 192.0.254.1/32 |
| AVD_FABRIC | leaf2 | 192.0.254.1/32 |
| AVD_FABRIC | leaf3 | 192.0.254.3/32 |
| AVD_FABRIC | leaf4 | 192.0.254.3/32 |
