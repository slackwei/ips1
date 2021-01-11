# DC1-SPINE2

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
| Management1 | oob_management | MGMT | 192.168.111.32/24 | 192.168.111.1 |

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
   ip address 192.168.111.32/24
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

MLAG not defined

# Spanning Tree

## Spanning Tree Summary

Mode: none

## Spanning Tree Device Configuration

```eos
!
spanning-tree mode none
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

No VLANs defined

# Interfaces

## Ethernet Interfaces

### Ethernet Interfaces Summary

| Interface | Description | MTU | Type | Mode | Allowed VLANs (Trunk) | Trunk Group | VRF | IP Address | Channel-Group ID | Channel-Group Type |
| --------- | ----------- | --- | ---- | ---- | --------------------- | ----------- | --- | ---------- | ---------------- | ------------------ |
| Ethernet1 | P2P_LINK_TO_DC1-LEAF1A_Ethernet2 | 1600 | routed | access | - | - | - | 10.1.0.2/31 | - | - |
| Ethernet2 | P2P_LINK_TO_DC1-LEAF1B_Ethernet2 | 1600 | routed | access | - | - | - | 10.1.0.10/31 | - | - |
| Ethernet3 | P2P_LINK_TO_DC1-LEAF2A_Ethernet2 | 1600 | routed | access | - | - | - | 10.1.0.18/31 | - | - |
| Ethernet4 | P2P_LINK_TO_DC1-LEAF2B_Ethernet2 | 1600 | routed | access | - | - | - | 10.1.0.26/31 | - | - |
| Ethernet6 | P2P_LINK_TO_DC1-GW1A_Ethernet2 | 1600 | routed | access | - | - | - | 10.1.0.34/31 | - | - |
| Ethernet7 | P2P_LINK_TO_DC1-GW1B_Ethernet2 | 1600 | routed | access | - | - | - | 10.1.0.42/31 | - | - |

*Inherited from Port-Channel Interface


### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_DC1-LEAF1A_Ethernet2
   mtu 1600
   no switchport
   ip address 10.1.0.2/31
!
interface Ethernet2
   description P2P_LINK_TO_DC1-LEAF1B_Ethernet2
   mtu 1600
   no switchport
   ip address 10.1.0.10/31
!
interface Ethernet3
   description P2P_LINK_TO_DC1-LEAF2A_Ethernet2
   mtu 1600
   no switchport
   ip address 10.1.0.18/31
!
interface Ethernet4
   description P2P_LINK_TO_DC1-LEAF2B_Ethernet2
   mtu 1600
   no switchport
   ip address 10.1.0.26/31
!
interface Ethernet6
   description P2P_LINK_TO_DC1-GW1A_Ethernet2
   mtu 1600
   no switchport
   ip address 10.1.0.34/31
!
interface Ethernet7
   description P2P_LINK_TO_DC1-GW1B_Ethernet2
   mtu 1600
   no switchport
   ip address 10.1.0.42/31
```

## Port-Channel Interfaces

No port-channels defined

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | EVPN_Overlay_Peering | default | 10.1.1.2/32 |

#### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | EVPN_Overlay_Peering | default | - |


### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description EVPN_Overlay_Peering
   ip address 10.1.1.2/32
```

## VLAN Interfaces

No VLAN interfaces defined

## VXLAN Interface

No VXLAN interfaces defined

# Routing

## Virtual Router MAC Address

IP virtual router MAC address not defined

## IP Routing

### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | true| | MGMT | false |

### IP Routing Device Configuration

```eos
!
ip routing
no ip routing vrf MGMT
```

## IPv6 Routing

### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | false || MGMT | false |


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
| 65100|  10.1.1.2 |

| BGP Tuning |
| ---------- |
| update wait-for-convergence |
| distance bgp 20 200 200 |
| no bgp default ipv4-unicast |
| maximum-paths 2 ecmp 2 |

### Router BGP Peer Groups

#### EVPN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| Next-hop unchanged | True |
| Source | Loopback0 |
| Bfd | true |
| Ebgp multihop | 3 |
| Send community | true |
| Maximum routes | 0 (no limit) |

#### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Maximum routes | 12000 |

### BGP Neighbors

| Neighbor | Remote AS |
| -------- | ---------
| 10.1.0.3 | 65101 |
| 10.1.0.11 | 65101 |
| 10.1.0.19 | 65102 |
| 10.1.0.27 | 65102 |
| 10.1.0.35 | 65103 |
| 10.1.0.43 | 65103 |
| 10.1.1.3 | 65101 |
| 10.1.1.4 | 65101 |
| 10.1.1.5 | 65102 |
| 10.1.1.6 | 65102 |
| 10.1.1.7 | 65103 |
| 10.1.1.8 | 65103 |

### Router BGP EVPN Address Family

#### Router BGP EVPN MAC-VRFs

#### Router BGP EVPN VRFs

### Router BGP Device Configuration

```eos
!
router bgp 65100
   router-id 10.1.1.2
   update wait-for-convergence
   distance bgp 20 200 200
   no bgp default ipv4-unicast
   maximum-paths 2 ecmp 2
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS next-hop-unchanged
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS password 7 q+VNViP5i4rVjW1cxFv2wA==
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS password 7 AQQvKeimxJu+uGQ/yYvv9w==
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 10.1.0.3 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.1.0.3 remote-as 65101
   neighbor 10.1.0.11 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.1.0.11 remote-as 65101
   neighbor 10.1.0.19 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.1.0.19 remote-as 65102
   neighbor 10.1.0.27 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.1.0.27 remote-as 65102
   neighbor 10.1.0.35 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.1.0.35 remote-as 65103
   neighbor 10.1.0.43 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.1.0.43 remote-as 65103
   neighbor 10.1.1.3 peer group EVPN-OVERLAY-PEERS
   neighbor 10.1.1.3 remote-as 65101
   neighbor 10.1.1.4 peer group EVPN-OVERLAY-PEERS
   neighbor 10.1.1.4 remote-as 65101
   neighbor 10.1.1.5 peer group EVPN-OVERLAY-PEERS
   neighbor 10.1.1.5 remote-as 65102
   neighbor 10.1.1.6 peer group EVPN-OVERLAY-PEERS
   neighbor 10.1.1.6 remote-as 65102
   neighbor 10.1.1.7 peer group EVPN-OVERLAY-PEERS
   neighbor 10.1.1.7 remote-as 65103
   neighbor 10.1.1.8 peer group EVPN-OVERLAY-PEERS
   neighbor 10.1.1.8 remote-as 65103
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
      no neighbor IPv4-UNDERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
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

No IP IGMP configuration

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
| 10 | permit 10.1.1.0/24 le 32 |

### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 10.1.1.0/24 le 32
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

## VRF Instances Device Configuration

```eos
!
vrf instance MGMT
```

# Virtual Source NAT

Virtual source NAT not defined

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
