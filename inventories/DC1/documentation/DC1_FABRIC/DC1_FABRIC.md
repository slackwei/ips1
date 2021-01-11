# DC1_FABRIC

## Table of Contents

- [DC1_FABRIC](#dc1fabric )
  - [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Topology](#fabric-topology)
  - [Fabric IP Allocation](#fabric-ip-allocation)
    - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
    - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
    - [Overlay Loopback Interfaces (BGP EVPN Peering)](#overlay-loopback-interfaces-bgp-evpn-peering)
    - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
    - [VTEP Loopback VXLAN Tunnel Source Interfaces (Leafs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-leafs-only)
    - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| Node | Management IP | Platform |
| ---- | ------------- | -------- |
| DC1-SPINE1 | 192.168.111.31/24 | vEOS-LAB |
| DC1-SPINE2 | 192.168.111.32/24 | vEOS-LAB |
| DC1-GW1A | 192.168.111.61/24 | vEOS-LAB |
| DC1-GW1B | 192.168.111.62/24 | vEOS-LAB |
| DC1-LEAF1A | 192.168.111.34/24 | vEOS-LAB |
| DC1-LEAF1B | 192.168.111.35/24 | vEOS-LAB |
| DC1-LEAF2A | 192.168.111.37/24 | vEOS-LAB |
| DC1-LEAF2B | 192.168.111.38/24 | vEOS-LAB |
| DC1-L2LEAF1 | 192.168.111.33/24 | vEOS-LAB |
| DC1-L2LEAF2 | 192.168.111.36/24 | vEOS-LAB |

## Fabric Topology

| Type | Leaf Node | Leaf Interface | Peer Node | Peer Interface |
| ---- | --------- | -------------- | --------- | -------------- |
| L3 Leaf | DC1-GW1A | Ethernet1 | DC1-SPINE1 | Ethernet6 |
| L3 Leaf | DC1-GW1A | Ethernet2 | DC1-SPINE2 | Ethernet6 |
| L3 Leaf | DC1-GW1B | Ethernet1 | DC1-SPINE1 | Ethernet7 |
| L3 Leaf | DC1-GW1B | Ethernet2 | DC1-SPINE2 | Ethernet7 |
| L3 Leaf | DC1-LEAF1A | Ethernet1 | DC1-SPINE1 | Ethernet1 |
| L3 Leaf | DC1-LEAF1A | Ethernet2 | DC1-SPINE2 | Ethernet1 |
| L3 Leaf | DC1-LEAF1B | Ethernet1 | DC1-SPINE1 | Ethernet2 |
| L3 Leaf | DC1-LEAF1B | Ethernet2 | DC1-SPINE2 | Ethernet2 |
| L3 Leaf | DC1-LEAF2A | Ethernet1 | DC1-SPINE1 | Ethernet3 |
| L3 Leaf | DC1-LEAF2A | Ethernet2 | DC1-SPINE2 | Ethernet3 |
| L3 Leaf | DC1-LEAF2B | Ethernet1 | DC1-SPINE1 | Ethernet4 |
| L3 Leaf | DC1-LEAF2B | Ethernet2 | DC1-SPINE2 | Ethernet4 |
| L2 Leaf | DC1-L2LEAF1 | Ethernet1 | DC1-LEAF1A | Ethernet4 |
| L2 Leaf | DC1-L2LEAF1 | Ethernet2 | DC1-LEAF1B | Ethernet4 |
| L2 Leaf | DC1-L2LEAF2 | Ethernet1 | DC1-LEAF2A | Ethernet4 |
| L2 Leaf | DC1-L2LEAF2 | Ethernet2 | DC1-LEAF2B | Ethernet4 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| P2P Summary | Available Addresses | Assigned addresses | Assigned Address % |
| ----------- | ------------------- | ------------------ | ------------------ |
| 10.1.0.0/24 | 256 | 48 | 18.75 % |

### Point-To-Point Links Node Allocation

| Leaf Node | Leaf Interface | Leaf IP Address | Spine Node | Spine Interface | Spine IP Address |
| --------- | -------------- | --------------- | ---------- | --------------- | ---------------- |
| DC1-GW1A | Ethernet1 | 10.1.0.33/31 | DC1-SPINE1 | Ethernet6 | 10.1.0.32/31 |
| DC1-GW1A | Ethernet2 | 10.1.0.35/31 | DC1-SPINE2 | Ethernet6 | 10.1.0.34/31 |
| DC1-GW1B | Ethernet1 | 10.1.0.41/31 | DC1-SPINE1 | Ethernet7 | 10.1.0.40/31 |
| DC1-GW1B | Ethernet2 | 10.1.0.43/31 | DC1-SPINE2 | Ethernet7 | 10.1.0.42/31 |
| DC1-LEAF1A | Ethernet1 | 10.1.0.1/31 | DC1-SPINE1 | Ethernet1 | 10.1.0.0/31 |
| DC1-LEAF1A | Ethernet2 | 10.1.0.3/31 | DC1-SPINE2 | Ethernet1 | 10.1.0.2/31 |
| DC1-LEAF1B | Ethernet1 | 10.1.0.9/31 | DC1-SPINE1 | Ethernet2 | 10.1.0.8/31 |
| DC1-LEAF1B | Ethernet2 | 10.1.0.11/31 | DC1-SPINE2 | Ethernet2 | 10.1.0.10/31 |
| DC1-LEAF2A | Ethernet1 | 10.1.0.17/31 | DC1-SPINE1 | Ethernet3 | 10.1.0.16/31 |
| DC1-LEAF2A | Ethernet2 | 10.1.0.19/31 | DC1-SPINE2 | Ethernet3 | 10.1.0.18/31 |
| DC1-LEAF2B | Ethernet1 | 10.1.0.25/31 | DC1-SPINE1 | Ethernet4 | 10.1.0.24/31 |
| DC1-LEAF2B | Ethernet2 | 10.1.0.27/31 | DC1-SPINE2 | Ethernet4 | 10.1.0.26/31 |

### Overlay Loopback Interfaces (BGP EVPN Peering)

| Overlay Loopback Summary | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------------ | ------------------- | ------------------ | ------------------ |
| 10.1.1.0/24 | 256 | 8 | 3.13 % |

### Loopback0 Interfaces Node Allocation

| Node | Loopback0 |
| ---- | --------- |
| DC1-SPINE1 | 10.1.1.1/32 |
| DC1-SPINE2 | 10.1.1.2/32 |
| DC1-GW1A | 10.1.1.7/32 |
| DC1-GW1B | 10.1.1.8/32 |
| DC1-LEAF1A | 10.1.1.3/32 |
| DC1-LEAF1B | 10.1.1.4/32 |
| DC1-LEAF2A | 10.1.1.5/32 |
| DC1-LEAF2B | 10.1.1.6/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (Leafs Only)

| VTEP Loopback Summary | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 10.1.2.0/24 | 256 | 6 | 2.35 % |

### VTEP Loopback Node allocation

| Node | Loopback1 |
| ---- | --------- |
| DC1-GW1A | 10.1.2.7/32 |
| DC1-GW1B | 10.1.2.8/32 |
| DC1-LEAF1A | 10.1.2.3/32 |
| DC1-LEAF1B | 10.1.2.3/32 |
| DC1-LEAF2A | 10.1.2.5/32 |
| DC1-LEAF2B | 10.1.2.5/32 |
