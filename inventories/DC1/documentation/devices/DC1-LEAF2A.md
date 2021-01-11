# DC1-LEAF2A

# Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [DNS Domain](#dns-domain)
  - [Name Servers](#name-servers)
  - [Domain Lookup](#domain-lookup)
  - [NTP](#ntp)
  - [Management SSH](#management-ssh)
  - [Management GNMI](#management-api-gnmi)
  - [Management API](#Management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [TACACS Servers](#tacacs-servers)
  - [IP TACACS Source Interfaces](#ip-tacacs-source-interfaces)
  - [RADIUS Servers](#radius-servers)
  - [AAA Server Groups](#aaa-server-groups)
  - [AAA Authentication](#aaa-authentication)
  - [AAA Authorization](#aaa-authorization)
  - [AAA Accounting](#aaa-accounting)
- [Management Security](#management-security)
- [Aliases](#aliases)
- [Monitoring](#monitoring)
  - [TerminAttr Daemon](#terminattr-daemon)
  - [Logging](#logging)
  - [SNMP](#snmp)
  - [SFlow](#sflow)
  - [Hardware Counters](#hardware-counters)
  - [VM Tracer Sessions](#vm-tracer-sessions)
  - [Event Handler](#event-handler)
- [MLAG](#mlag)
- [Spanning Tree](#spanning-tree)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
- [VLANs](#vlans)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Port-Channel Interfaces](#port-channel-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
  - [VLAN Interfaces](#vlan-interfaces)
  - [VXLAN Interface](#vxlan-interface)
- [Routing](#routing)
  - [Virtual Router MAC Address](#virtual-router-mac-address)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [IPv6 Static Routes](#ipv6-static-routes)
  - [Router ISIS](#router-isis)
  - [Router BGP](#router-bgp)
  - [Router BFD](#router-bfd)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
  - [Router Multicast](#router-multicast)
  - [Router PIM Sparse Mode](#router-pim-sparse-mode)
- [Filters](#filters)
  - [Community-lists](#community-lists)
  - [Peer Filters](#peer-filters)
  - [Prefix-lists](#prefix-lists)
  - [IPv6 Prefix-lists](#ipv6-prefix-lists)
  - [Route-maps](#route-maps)
  - [IP Extended Communities](#ip-extended-communities)
- [ACL](#acl)
  - [Standard Access-lists](#standard-access-lists)
  - [Extended Access-lists](#extended-access-lists)
  - [IPv6 Standard Access-lists](#ipv6-standard-access-lists)
  - [IPv6 Extended Access-lists](#ipv6-extended-access-lists)
- [VRF Instances](#vrf-instances)
- [Virtual Source NAT](#virtual-source-nat)
- [Platform](#platform)
- [Router L2 VPN](#router-l2-vpn)
- [IP DHCP Relay](#ip-dhcp-relay)

# Management

## Management Interfaces

### Management Interfaces Summary

#### IPv4

| Management Interface | description | VRF | IP Address | Gateway |
| -------------------- | ----------- | --- | ---------- | ------- |
| Management1 | oob_management | MGMT | 192.168.111.37/24 | 192.168.111.1 |

#### IPv6

| Management Interface | description | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | --- | ------------ | ------------ |
| Management1 | oob_management | MGMT | -  | - |

### Management Interfaces Device Configuration

```eos
!
interface Management1
   description oob_management
   vrf MGMT
   ip address 192.168.111.37/24
```

## DNS Domain

### DNS domain: slackwei

### DNS Domain Device Configuration

```eos
dns domain slackwei
!
```

## Domain-list

Domain-list not defined

## Name Servers

### Name Servers Summary

| Name Server | Source VRF |
| ----------- | ---------- |
| 192.168.111.45 | MGMT |

### Name Servers Device Configuration

```eos
ip name-server vrf MGMT 192.168.111.45
```

## Domain Lookup

DNS domain lookup not defined

## NTP

### NTP Summary

- Local Interface: Management1

- VRF: MGMT

| Node | Primary |
| ---- | ------- |
| 192.168.111.45 | true |

### NTP Device Configuration

```eos
!
ntp local-interface vrf MGMT Management1
ntp server vrf MGMT 192.168.111.45 prefer
```

## Management SSH

Management SSH not defined

## Management API GNMI

Management API gnmi is not defined

## Management API HTTP

### Management API HTTP Summary

| HTTP | HTTPS |
| ---------- | ---------- |
|  default  |  true  |

### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| MGMT |  -  |  -  |

### Management API HTTP Configuration

```eos
!
management api http-commands
   no shutdown
   !
   vrf MGMT
      no shutdown
```

# Authentication

## Local Users

### Local Users Summary

| User | Privilege | Role |
| ---- | --------- | ---- |
| admin | 15 | network-admin |
| cvpadmin | 15 | network-admin |

### Local Users Device Configuration

```eos
!
username admin privilege 15 role network-admin secret sha512 $6$kHbbE9/L.GrNTtl0$YnmI7ytA.5OtiR.z8HCPNo48NPxufpzNeQPNDBe7TOp3jdrQuwbWJPkcIIlgTUk1JEliJYvPkMKQBOn3oRC960
username cvpadmin privilege 15 role network-admin secret sha512 $6$g7vDU1eTXmx3UNVm$vbD3LzxM/sSXAvzLVbJh27ni0hCw3rYWBX0gfj3QWl1.KmBBf9ZzlqEX2Tcz13I51WqXfvGUoPRhuDZ712PK7.
```

## TACACS Servers

### TACACS Servers

| VRF | TACACS Servers |
| --- | ---------------|
|  MGMT | 192.168.111.45 |

### TACACS Servers Device Configuration

```eos
!
tacacs-server host 192.168.111.45 vrf MGMT  key 7 052A140632584F58 
```

## IP TACACS Source Interfaces

IP TACACS source interfaces not defined

## RADIUS Servers

RADIUS servers not defined

## AAA Server Groups

AAA server groups not defined

## AAA Authentication

### AAA Authentication Summary

| Type | Sub-type | User Stores |
| ---- | -------- | ---------- |
| Login | default | group tacacs+ local |

### AAA Authentication Device Configuration

```eos
!
aaa authentication login default group tacacs+ local
!
```

## AAA Authorization

### AAA Authorization Summary

| Type | User Stores |
| ---- | ----------- |
| Exec | group tacacs+ local |

Authorization for configuration commands is disabled.

### AAA Authorization Device Configuration

```eos
aaa authorization exec default group tacacs+ local
!
```

## AAA Accounting

### AAA Accounting Summary

| Type | Sub-type | Record | Accounting Stores | Logging |
| ---- | -------- | ------ |------------------ | ------- |
| Exec | - | start-stop | tacacs+ | - |
| Commands | all | start-stop | tacacs+  | True  |

### AAA Accounting Device Configuration

```eos
!
aaa accounting exec default start-stop group tacacs+
aaa accounting commands all default start-stop group tacacs+ logging
```

# Management Security

Management security not defined

# Aliases

Aliases not defined

# Monitoring

## TerminAttr Daemon

### TerminAttr Daemon Summary

| CV Compression | Ingest gRPC URL | Ingest Authentication Key | Smash Excludes | Ingest Exclude | Ingest VRF |  NTP VRF |
| -------------- | --------------- | ------------------------- | -------------- | -------------- | ---------- | -------- |
| gzip | 192.168.111.43:9910 | magickey | ale,flexCounter,hardware,kni,pulse,strata | /Sysdb/cell/1/agent,/Sysdb/cell/2/agent | MGMT | MGMT |

### TerminAttr Daemon Device Configuration

```eos
!
daemon TerminAttr
   exec /usr/bin/TerminAttr -ingestgrpcurl=192.168.111.43:9910 -cvcompression=gzip -ingestauth=key,magickey -smashexcludes=ale,flexCounter,hardware,kni,pulse,strata -ingestexclude=/Sysdb/cell/1/agent,/Sysdb/cell/2/agent -ingestvrf=MGMT -taillogs
   no shutdown
```

## Logging

No logging settings defined

## SNMP

No SNMP settings defined

## SFlow

No sFlow defined

## Hardware Counters

No hardware counters defined

## VM Tracer Sessions

No VM tracer sessions defined

## Event Handler

No event handler defined

# MLAG

## MLAG Summary

| Domain-id | Local-interface | Peer-address | Peer-link |
| --------- | --------------- | ------------ | --------- |
| DC1_LEAF2 | Vlan4094 | 10.255.252.5 | Port-Channel3 |

Dual primary detection is enabled. The detection delay is 5 seconds.

## MLAG Device Configuration

```eos
!
mlag configuration
   domain-id DC1_LEAF2
   local-interface Vlan4094
   peer-address 10.255.252.5
   peer-address heartbeat 192.168.111.38 vrf MGMT
   peer-link Port-Channel3
   dual-primary detection delay 5 action errdisable all-interfaces
   reload-delay mlag 300
   reload-delay non-mlag 330
```

# Spanning Tree

## Spanning Tree Summary

Mode: mstp

### MSTP Instance and Priority

| Instance | Priority |
| -------- | -------- |
| 0 | 4096 |

## Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
no spanning-tree vlan-id 4093-4094
spanning-tree mst 0 priority 4096
```

# Internal VLAN Allocation Policy

## Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

## Internal VLAN Allocation Policy Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

# VLANs

## VLANs Summary

| VLAN ID | Name | Trunk Groups |
| ------- | ---- | ------------ |
| 111 | Tenant_A_OP_Zone_2 | none  |
| 211 | Tenant_B_OP_fw | none  |
| 311 | Tenant_C_OP_fw | none  |
| 3010 | MLAG_iBGP_Tenant_A_OP_Zone | LEAF_PEER_L3  |
| 3020 | MLAG_iBGP_Tenant_B_OP_Zone | LEAF_PEER_L3  |
| 3030 | MLAG_iBGP_Tenant_C_OP_Zone | LEAF_PEER_L3  |
| 4093 | LEAF_PEER_L3 | LEAF_PEER_L3  |
| 4094 | MLAG_PEER | MLAG  |

## VLANs Device Configuration

```eos
!
vlan 111
   name Tenant_A_OP_Zone_2
!
vlan 211
   name Tenant_B_OP_fw
!
vlan 311
   name Tenant_C_OP_fw
!
vlan 3010
   name MLAG_iBGP_Tenant_A_OP_Zone
   trunk group LEAF_PEER_L3
!
vlan 3020
   name MLAG_iBGP_Tenant_B_OP_Zone
   trunk group LEAF_PEER_L3
!
vlan 3030
   name MLAG_iBGP_Tenant_C_OP_Zone
   trunk group LEAF_PEER_L3
!
vlan 4093
   name LEAF_PEER_L3
   trunk group LEAF_PEER_L3
!
vlan 4094
   name MLAG_PEER
   trunk group MLAG
```

# Interfaces

## Ethernet Interfaces

### Ethernet Interfaces Summary

| Interface | Description | MTU | Type | Mode | Allowed VLANs (Trunk) | Trunk Group | VRF | IP Address | Channel-Group ID | Channel-Group Type |
| --------- | ----------- | --- | ---- | ---- | --------------------- | ----------- | --- | ---------- | ---------------- | ------------------ |
| Ethernet1 | P2P_LINK_TO_DC1-SPINE1_Ethernet3 | 1600 | routed | access | - | - | - | 10.1.0.17/31 | - | - |
| Ethernet2 | P2P_LINK_TO_DC1-SPINE2_Ethernet3 | 1600 | routed | access | - | - | - | 10.1.0.19/31 | - | - |
| Ethernet3 | MLAG_PEER_DC1-LEAF2B_Ethernet3 | *1500 | *switched | *trunk | *2-4094 | *LEAF_PEER_L3<br> *MLAG | - | - | 3 | active |
| Ethernet4 | DC1-L2LEAF2_Ethernet1 | *1500 | *switched | *trunk | *111,211 | - | - | - | 4 | active |

*Inherited from Port-Channel Interface


### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_DC1-SPINE1_Ethernet3
   mtu 1600
   no switchport
   ip address 10.1.0.17/31
!
interface Ethernet2
   description P2P_LINK_TO_DC1-SPINE2_Ethernet3
   mtu 1600
   no switchport
   ip address 10.1.0.19/31
!
interface Ethernet3
   description MLAG_PEER_DC1-LEAF2B_Ethernet3
   channel-group 3 mode active
!
interface Ethernet4
   description DC1-L2LEAF2_Ethernet1
   channel-group 4 mode active
```

## Port-Channel Interfaces

### Port-Channel Interfaces Summary

| Interface | Description | MTU | Type | Mode | Allowed VLANs (trunk) | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI | VRF | IP Address | IPv6 Address |
| --------- | ----------- | --- | ---- | ---- | --------------------- | ----------- | --------------------- ! ------------------ | ------- | -------- | --- | ---------- | ------------ |
| Port-Channel3 | MLAG_PEER_DC1-LEAF2B_Po3 | 1500 | switched | trunk | 2-4094 | LEAF_PEER_L3<br> MLAG | - | - | - | - | - | - | - |
| Port-Channel4 | DC1_L2LEAF2_Po1 | 1500 | switched | trunk | 111,211 | - | - | - | 4 | - | - | - | - |

### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel3
   description MLAG_PEER_DC1-LEAF2B_Po3
   switchport trunk allowed vlan 2-4094
   switchport mode trunk
   switchport trunk group LEAF_PEER_L3
   switchport trunk group MLAG
!
interface Port-Channel4
   description DC1_L2LEAF2_Po1
   switchport trunk allowed vlan 111,211
   switchport mode trunk
   mlag 4
```

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | EVPN_Overlay_Peering | default | 10.1.1.5/32 |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | 10.1.2.5/32 |
| Loopback100 | Tenant_A_OP_Zone_VTEP_DIAGNOSTICS | Tenant_A_OP_Zone | 10.255.1.5/32 |

#### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | EVPN_Overlay_Peering | default | - |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | - |
| Loopback100 | Tenant_A_OP_Zone_VTEP_DIAGNOSTICS | Tenant_A_OP_Zone | - |


### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description EVPN_Overlay_Peering
   ip address 10.1.1.5/32
!
interface Loopback1
   description VTEP_VXLAN_Tunnel_Source
   ip address 10.1.2.5/32
!
interface Loopback100
   description Tenant_A_OP_Zone_VTEP_DIAGNOSTICS
   vrf Tenant_A_OP_Zone
   ip address 10.255.1.5/32
```

## VLAN Interfaces

### VLAN Interfaces Summary

| Interface | Description | VRF | IP Address | IP Address Virtual | IP Router Virtual Address (vARP) |
| --------- | ----------- | --- | ---------- | ------------------ | -------------------------------- |
| Vlan111 | Tenant_A_OP_Zone_2 | Tenant_A_OP_Zone | 10.1.11.21/24 | - | 10.1.11.1 |
| Vlan211 | Tenant_B_OP_fw | Tenant_B_OP_Zone | - | - | - |
| Vlan311 | Tenant_C_OP_fw | Tenant_C_OP_Zone | - | - | - |
| Vlan3010 | MLAG_PEER_L3_iBGP: vrf Tenant_A_OP_Zone | Tenant_A_OP_Zone | 10.255.251.4/31 | - | - |
| Vlan3020 | MLAG_PEER_L3_iBGP: vrf Tenant_B_OP_Zone | Tenant_B_OP_Zone | 10.255.251.4/31 | - | - |
| Vlan3030 | MLAG_PEER_L3_iBGP: vrf Tenant_C_OP_Zone | Tenant_C_OP_Zone | 10.255.251.4/31 | - | - |
| Vlan4093 | MLAG_PEER_L3_PEERING | default | 10.255.251.4/31 | - | - |
| Vlan4094 | MLAG_PEER | default | 10.255.252.4/31 | - | - |


### VLAN Interfaces Device Configuration

```eos
!
interface Vlan111
   description Tenant_A_OP_Zone_2
   vrf Tenant_A_OP_Zone
   ip address 10.1.11.21/24
   ip virtual-router address 10.1.11.1
!
interface Vlan211
   description Tenant_B_OP_fw
   vrf Tenant_B_OP_Zone
!
interface Vlan311
   description Tenant_C_OP_fw
   vrf Tenant_C_OP_Zone
!
interface Vlan3010
   description MLAG_PEER_L3_iBGP: vrf Tenant_A_OP_Zone
   vrf Tenant_A_OP_Zone
   ip address 10.255.251.4/31
!
interface Vlan3020
   description MLAG_PEER_L3_iBGP: vrf Tenant_B_OP_Zone
   vrf Tenant_B_OP_Zone
   ip address 10.255.251.4/31
!
interface Vlan3030
   description MLAG_PEER_L3_iBGP: vrf Tenant_C_OP_Zone
   vrf Tenant_C_OP_Zone
   ip address 10.255.251.4/31
!
interface Vlan4093
   description MLAG_PEER_L3_PEERING
   ip address 10.255.251.4/31
!
interface Vlan4094
   description MLAG_PEER
   mtu 1600
   no autostate
   ip address 10.255.252.4/31
```

## VXLAN Interface

### VXLAN Interface Summary

#### Source Interface: Loopback1

#### UDP port: 4789

#### VLAN to VNI Mappings

| VLAN | VNI |
| ---- | --- |
| 111 | 10111 |
| 211 | 20211 |
| 311 | 30311 |

#### VRF to VNI Mappings

| VLAN | VNI |
| ---- | --- |
| Tenant_A_OP_Zone | 11 |
| Tenant_B_OP_Zone | 21 |
| Tenant_C_OP_Zone | 31 |

### VXLAN Interface Device Configuration

```eos
!
interface Vxlan1
   vxlan source-interface Loopback1
   vxlan virtual-router encapsulation mac-address mlag-system-id
   vxlan udp-port 4789
   vxlan vlan 111 vni 10111
   vxlan vlan 211 vni 20211
   vxlan vlan 311 vni 30311
   vxlan vrf Tenant_A_OP_Zone vni 11
   vxlan vrf Tenant_B_OP_Zone vni 21
   vxlan vrf Tenant_C_OP_Zone vni 31
```

# Routing

## Virtual Router MAC Address


### Virtual Router MAC Address Summary

#### Virtual Router MAC Address: 00:dc:00:00:00:0a

### Virtual Router MAC Address Configuration

```eos
!
ip virtual-router mac-address 00:dc:00:00:00:0a
```

## IP Routing

### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | true| | MGMT | false |
| Tenant_A_OP_Zone | true |
| Tenant_B_OP_Zone | true |
| Tenant_C_OP_Zone | true |

### IP Routing Device Configuration

```eos
!
ip routing
no ip routing vrf MGMT
ip routing vrf Tenant_A_OP_Zone
ip routing vrf Tenant_B_OP_Zone
ip routing vrf Tenant_C_OP_Zone
```

## IPv6 Routing

### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | false || MGMT | false |
| Tenant_A_OP_Zone | false |
| Tenant_B_OP_Zone | false |
| Tenant_C_OP_Zone | false |


## Static Routes

### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP             | Exit interface      | Administrative Distance       | Tag               | Route Name                    | Metric         |
| --- | ------------------ | ----------------------- | ------------------- | ----------------------------- | ----------------- | ----------------------------- | -------------- |
| MGMT  | 0.0.0.0/0 |  192.168.111.1  |  -  |  1  |  -  |  -  |  - |

### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 192.168.111.1
```

## IPv6 Static Routes

IPv6 static routes not defined

## Router ISIS

Router ISIS not defined

## Router BGP

### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65102|  10.1.1.5 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| distance bgp 20 200 200 |
| maximum-paths 2 ecmp 2 |

### Router BGP Peer Groups

#### EVPN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| Remote_as | 65100 |
| Source | Loopback0 |
| Bfd | true |
| Ebgp multihop | 3 |
| Send community | true |
| Maximum routes | 0 (no limit) |

#### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Remote_as | 65100 |
| Send community | true |
| Maximum routes | 12000 |

#### MLAG-IPv4-UNDERLAY-PEER

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Remote_as | 65102 |
| Next-hop self | True |
| Send community | true |
| Maximum routes | 12000 |

### BGP Neighbors

| Neighbor | Remote AS |
| -------- | ---------
| 10.1.0.16 | Inherited from peer group IPv4-UNDERLAY-PEERS |
| 10.1.0.18 | Inherited from peer group IPv4-UNDERLAY-PEERS |
| 10.1.1.1 | Inherited from peer group EVPN-OVERLAY-PEERS |
| 10.1.1.2 | Inherited from peer group EVPN-OVERLAY-PEERS |
| 10.255.251.5 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER |

### Router BGP EVPN Address Family

#### Router BGP EVPN MAC-VRFs

##### VLAN aware bundles

| VLAN Aware Bundle | Route-Distinguisher | Both Route-Target | Import Route Target | Export Route-Target | Redistribute | VLANs |
| ----------------- | ------------------- | ----------------- | ------------------- | ------------------- | ------------ | ----- |
| Tenant_A_OP_Zone | 10.1.1.5:11 |  65100:11  |  |  | learned | 111 |
| Tenant_B_OP_Zone | 10.1.1.5:21 |  65100:21  |  |  | learned | 211 |
| Tenant_C_OP_Zone | 10.1.1.5:31 |  65100:31  |  |  | learned | 311 |

#### Router BGP EVPN VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| Tenant_A_OP_Zone | 10.1.1.5:11 | connected |
| Tenant_B_OP_Zone | 10.1.1.5:21 | connected |
| Tenant_C_OP_Zone | 10.1.1.5:31 | connected |

### Router BGP Device Configuration

```eos
!
router bgp 65102
   router-id 10.1.1.5
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   maximum-paths 2 ecmp 2
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS remote-as 65100
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS password 7 q+VNViP5i4rVjW1cxFv2wA==
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS remote-as 65100
   neighbor IPv4-UNDERLAY-PEERS password 7 AQQvKeimxJu+uGQ/yYvv9w==
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor MLAG-IPv4-UNDERLAY-PEER peer group
   neighbor MLAG-IPv4-UNDERLAY-PEER remote-as 65102
   neighbor MLAG-IPv4-UNDERLAY-PEER next-hop-self
   neighbor MLAG-IPv4-UNDERLAY-PEER password 7 vnEaG8gMeQf3d3cN6PktXQ==
   neighbor MLAG-IPv4-UNDERLAY-PEER send-community
   neighbor MLAG-IPv4-UNDERLAY-PEER maximum-routes 12000
   neighbor 10.1.0.16 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.1.0.18 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.1.1.1 peer group EVPN-OVERLAY-PEERS
   neighbor 10.1.1.2 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.251.5 peer group MLAG-IPv4-UNDERLAY-PEER
   redistribute connected route-map RM-CONN-2-BGP
   !
   vlan-aware-bundle Tenant_A_OP_Zone
      rd 10.1.1.5:11
      route-target both 65100:11
      redistribute learned
      vlan 111
   !
   vlan-aware-bundle Tenant_B_OP_Zone
      rd 10.1.1.5:21
      route-target both 65100:21
      redistribute learned
      vlan 211
   !
   vlan-aware-bundle Tenant_C_OP_Zone
      rd 10.1.1.5:31
      route-target both 65100:31
      redistribute learned
      vlan 311
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
      no neighbor IPv4-UNDERLAY-PEERS activate
      no neighbor MLAG-IPv4-UNDERLAY-PEER activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
      neighbor MLAG-IPv4-UNDERLAY-PEER activate
   !
   vrf Tenant_A_OP_Zone
      rd 10.1.1.5:11
      route-target import evpn 65100:11
      route-target export evpn 65100:11
      router-id 10.1.1.5
      neighbor 10.255.251.5 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
   !
   vrf Tenant_B_OP_Zone
      rd 10.1.1.5:21
      route-target import evpn 65100:21
      route-target export evpn 65100:21
      router-id 10.1.1.5
      neighbor 10.255.251.5 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
   !
   vrf Tenant_C_OP_Zone
      rd 10.1.1.5:31
      route-target import evpn 65100:31
      route-target export evpn 65100:31
      router-id 10.1.1.5
      neighbor 10.255.251.5 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
```

## Router BFD

### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 1200 | 1200 | 3 |

### Router BFD Multihop Device Configuration

```eos
!
router bfd
   multihop interval 1200 min-rx 1200 multiplier 3
```

# Multicast

## IP IGMP Snooping

### IP IGMP Snooping Summary

## Router Multicast

Routing multicast not defined

## Router PIM Sparse Mode

Router PIM sparse mode not defined

# Filters

## Community-lists

Community-lists not defined

## Peer Filters

No peer filters defined

## Prefix-lists

### Prefix-lists Summary

#### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 10.1.1.0/24 eq 32 |
| 20 | permit 10.1.2.0/24 eq 32 |

### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 10.1.1.0/24 eq 32
   seq 20 permit 10.1.2.0/24 eq 32
```

## IPv6 Prefix-lists

IPv6 prefix-lists not defined

## Route-maps

### Route-maps Summary

#### RM-CONN-2-BGP

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY |

### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
```

## IP Extended Communities

No extended community defined

# ACL

## Standard Access-lists

Standard access-lists not defined

## Extended Access-lists

Extended access-lists not defined

## IPv6 Standard Access-lists

IPv6 standard access-lists not defined

## IPv6 Extended Access-lists

IPv6 extended access-lists not defined

# VRF Instances

## VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | disabled |
| Tenant_A_OP_Zone | enabled |
| Tenant_B_OP_Zone | enabled |
| Tenant_C_OP_Zone | enabled |

## VRF Instances Device Configuration

```eos
!
vrf instance MGMT
!
vrf instance Tenant_A_OP_Zone
!
vrf instance Tenant_B_OP_Zone
!
vrf instance Tenant_C_OP_Zone
```

# Virtual Source NAT

## Virtual Source NAT Summary

| Source NAT VRF | Source NAT IP Address |
| -------------- | --------------------- |
| Tenant_A_OP_Zone | 10.255.1.5 |

## Virtual Source NAT Configuration

```eos
!
ip address virtual source-nat vrf Tenant_A_OP_Zone address 10.255.1.5
```

# Platform

No platform parameters defined

# Router L2 VPN

Router L2 VPN not defined

# IP DHCP Relay

IP DHCP relay not defined

# Custom Templates

### Configuration Generated by `DC1/alias.j2`
```eos

!
alias rb router bgp 65100
```
