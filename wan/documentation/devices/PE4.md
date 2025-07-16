# PE4

## Table of Contents

- [Management](#management)
  - [Agents](#agents)
  - [Management Interfaces](#management-interfaces)
  - [DNS Domain](#dns-domain)
  - [IP Name Servers](#ip-name-servers)
  - [Clock Settings](#clock-settings)
  - [NTP](#ntp)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Enable Password](#enable-password)
  - [AAA Authorization](#aaa-authorization)
- [Aliases Device Configuration](#aliases-device-configuration)
- [Monitoring](#monitoring)
  - [TerminAttr Daemon](#terminattr-daemon)
  - [Logging](#logging)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Device Configuration](#internal-vlan-allocation-policy-device-configuration)
- [Interfaces](#interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Router ISIS](#router-isis)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [MPLS](#mpls)
  - [MPLS and LDP](#mpls-and-ldp)
  - [MPLS Device Configuration](#mpls-device-configuration)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
  - [Router Multicast](#router-multicast)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [System L1](#system-l1)
  - [Unsupported Interface Configurations](#unsupported-interface-configurations)
  - [System L1 Device Configuration](#system-l1-device-configuration)
- [EOS CLI Device Configuration](#eos-cli-device-configuration)

## Management

### Agents

#### Agent KernelFib

##### Environment Variables

| Name | Value |
| ---- | ----- |
| KERNELFIB_PROGRAM_ALL_ECMP | 'true' |

#### Agents Device Configuration

```eos
!
agent KernelFib environment KERNELFIB_PROGRAM_ALL_ECMP='true'
```

### Management Interfaces

#### Management Interfaces Summary

##### IPv4

| Management Interface | Description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | OOB_MANAGEMENT | oob | default | 192.168.0.14/24 | - |

##### IPv6

| Management Interface | Description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management1 | OOB_MANAGEMENT | oob | default | - | - |

#### Management Interfaces Device Configuration

```eos
!
interface Management1
   description OOB_MANAGEMENT
   no shutdown
   ip address 192.168.0.14/24
```

### DNS Domain

DNS domain: sjc.aristanetworks.com

#### DNS Domain Device Configuration

```eos
dns domain sjc.aristanetworks.com
!
```

### IP Name Servers

#### IP Name Servers Summary

| Name Server | VRF | Priority |
| ----------- | --- | -------- |
| 169.254.169.254 | default | - |

#### IP Name Servers Device Configuration

```eos
ip name-server vrf default 169.254.169.254
```

### Clock Settings

#### Clock Timezone Settings

Clock Timezone is set to **PST8PDT**.

#### Clock Device Configuration

```eos
!
clock timezone PST8PDT
```

### NTP

#### NTP Summary

##### NTP Servers

| Server | VRF | Preferred | Burst | iBurst | Version | Min Poll | Max Poll | Local-interface | Key |
| ------ | --- | --------- | ----- | ------ | ------- | -------- | -------- | --------------- | --- |
| 0.us.pool.ntp.org | default | True | - | - | - | - | - | - | - |

#### NTP Device Configuration

```eos
!
ntp server 0.us.pool.ntp.org prefer
```

### Management API HTTP

#### Management API HTTP Summary

| HTTP | HTTPS | UNIX-Socket | Default Services |
| ---- | ----- | ----------- | ---------------- |
| False | True | - | - |

#### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| default | - | - |

#### Management API HTTP Device Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf default
      no shutdown
```

## Authentication

### Enable Password

Enable password has been disabled

### AAA Authorization

#### AAA Authorization Summary

| Type | User Stores |
| ---- | ----------- |
| Exec | local |

Authorization for configuration commands is disabled.

#### AAA Authorization Device Configuration

```eos
aaa authorization exec default local
!
```

## Aliases Device Configuration

```eos
alias cc clear counters
alias cpc clear platform trident counters
alias senz show interface counter error | nz
alias shmc show int | awk '/^[A-Z]/ { intf = $1 } /, address is/ { print intf, $6 }'
alias snz show interface counter | nz
alias sqnz show interface counter queue | nz
alias srnz show interface counter rate | nz
username admin role network-admin privilege 15 secret sha512 $6$Jb3g.EWhQcUL.Ypz$.nH6693N11A4e7Zcsv8sWDxSKRO/0vTzbabDVGaSjDng/r7HvL8qrcojyCxUOwTyCOK15VrRz3iBj4HogSszq1
username cvpadmin secret sha512 $6$a/HsQ.4E0VbyEi4v$jsX5fxEwQJ4pmAX0GOXerffTmMmXfQ4aX/01f/iqqdXlOycL2UCrVZa96vPegCwV.LsYy4VV4JjOcNKJVkuxB.
username cwomble secret *
username cwomble ssh-key ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDOZFQIhHNghkuJryYiNyFUbkVPyGH2tU1gFuoJ/wDDg420VY9tb1OQn7k+XoDaVWWoEoOek07sJzns0Yy7WYUhgHP3T8Q3qW2DRjRDCUgUXnt9iW9N/axh4U4OP71UbWJNw3D6b5JE4EWt56okFcR6eSAyyKoYZvUAiCX1oUGVbRDz0cTNTbbnYHXp8DFBM/3fLNrO7Ntif+1ZtY8IQoZoDaOZpQLqTt40QGBAJgyXy0xP3urSaSJP2alSZP0g2IY9WebHaJAKnzP+SCuU4pMpcWYE3EoevYB6RLy12WylXq7Ht8sy2cjB9HH19BM4lNvRJ7ArjsL8enBP4OdqdyCH/SfLy6YrQ2EFidNpxnGBNVxIA7lkK82jLGFiqKJJNapZW4nRljT+KVMFEh/NTDP61wYmUPCR331+e3TiKsapwcIN/Q1+20WBVf11RseChjLqZzu54y9PDw/MA8ra8mPbuenhNJ6Xw8nkZbeUr+o/jZHwTP0sTLFyv4uJKvOACBc=
username dlyssenko secret *
username dlyssenko ssh-key ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDNXb2O9ciq3TIVGJOh3/XARvlg45QUAo6FFB0p7rnAXAd+z7AzXg2j9uFQ9NTuiupFdYWDAXYg6RNcrX3vjoSBOxb/cnSYREG9GLB+aVyxZ8fPDN4wq4s+VQzrSmzvBZ+P7/Y4E4GAZiRE3MaK/cPIqFrbHhZYfrg8BBivenCK4ztEI/OYAGWzza/5v6Mx3fW1xGsgZtFO6epmv0/OqRq8WnwoJiXdn0INa0Yx3xI5JbBpUj49EHUXpwo1HB+SEIzy0WxSoy4gVBic7qEXG2alfUtOqNPmgU6MVE0uiKspdKqoF0NYEO/cLSwIgBENnGX4y2NvAxTfgrHub2z+WpA9/Mo65rNnKNQdQ8xOAVyoeXMHwGcRZYN3HkK5NK+7jb7RWHcIieb/+7LGhRAQg8BhY7h3I6cpA7qTF4j3UAJRH6zS7wVRNqDM40EgEmylA+w2qMt7E+csTjgNJ3KX/jY0AG8jWeR7cZhvTnIfkGw4u9fhmLQSW4LSJpztJ0T0Otc=
username ec2-user shell /bin/bash nopassword
username ec2-user ssh-key ssh-rsa ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDjacklo6yEWBtpXU2rL8mq6ab3qWWn2U7QrHz0yfl4+YW8FKV0xnlY6z/fAzOMEBcewq6M6cjDcUdqVNK/kWulAUcwa657zI0UmN+cjjJ3Gg7zRUTq6eijRWde0j6b09kfg5ZE9eFs+wBtwCa41yPl7kL61dXHkaqcQc0m9CPB3rSh0aF7DXtUrRHJipKRtkaXlIluwX5KRfedn5jz7yIweVCT0Ji8JqZcGnX8GtZaWuAlAZMIJMPlp+a+Dh9pSFozCERKPN14bt3syVQrLx3bfEcA5A3567G5BQoYdojM1wAaDl/aqVLWTYSIWoqIEZU5Fp9Gghp2TTX1JJeLVt2+YApllo0XNE0qf+l7IGojL/7wQN1vMoZ/+BjeLENiGkstwvGgZyY9cd5F8fFn/c4LldC8X7EX8oP8fznGkx7RTrXGOxpu/oRQ0Leg2Px8SULsL1g0DRkMt48UKIWcY7CBC6jDxA5T1C4CtxWpAPZaHiIH8F0nU3nPPyEvDLfdf+s= nonroot@buildkitsandbox
username gcp-user secret *
username gcp-user ssh-key ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDGPEoZ2l67eEEwrlGfBAHPMx44IoqhyfjqXj2Ka4PxLuHgi1mv131VuCRlyWjOjddccyFUilfR1Bprdmd1Tj7o4Q11YQ138LOqFWJT3h0pxgHFdIHo70y4rI8aL15ixukZYa+g9KX8qTN+ZpFfea2d3CEFzMp+Y3xVPiWwLKzalq1JwT5J4MK2VHCbcnpN3zRON+gca/iZH9upA0WaXWJXNBnYXrgXFVGCJFk6Yl1ZXIGnEcKGe44c77zWgF4C66VhltsW999XD5vF31f6TTs25qxGScsiKMDg2uM1AzVg5KfxxhVy5HKd23YJJMytvUXL9h5Wq1HEEluSCcFtNI81
username mircea secret *
username mircea ssh-key ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDw26o1dbfin+wgiYhiHybYebcYlS1EpucVdzfZASTkaMnCiaGy61mLtCaiZA82MEMNbkHLr9WgO2f9pHN2fiIiJc2gmlZPAUvSDzOHQapGuWzoPbeoKTaPyEzkDD5IzerV8wgMooaJOIWU9dWRjVPpUyj2GJ3JirC3HiLRnhkHFh3F+vUkEL81lMzJ/0HdnW3WrIjU6JnuOnpjiJ+np1OEPSbBdANT89tzaEm87QUioPQF7hHknKFUYK2Zqh5SXR6vQaLEcIhRqlAvZyjc95vDtYFWzqrdrHTdznyr8Hs/R2OeLmPGArGm6V8sGC9Q1bGfbhwjxvoWH9igUO6d82HKL2h8PJ1gXJU4XCb6Dkft7y0M4CDx6tIOo9jDxwFRtim9oC0uwxsRoXL4xCDYGH+jO4RAQSVxP6MQsJBEOvXez6whUev1lR91CiXmtUwQfzfmol03U8xMsBkdZ+Y4B7AkBUIpi/+8aEbMwRACyDZJB0+FzkYuWIYpiqoQ4pwUVw8=
username service shell /bin/bash secret sha512 $6$rpyy.A3lNlFHChhB$VZxv2tWR6cX.tBALsAy.GUwR8ZLLp5KnShXclEpGhbTm3Cs0R9063wsYQ4OopovX8JSe2ucLBVHBfopeGUlP..

!
```

## Monitoring

### TerminAttr Daemon

#### TerminAttr Daemon Summary

| CV Compression | CloudVision Servers | VRF | Authentication | Smash Excludes | Ingest Exclude | Bypass AAA |
| -------------- | ------------------- | --- | -------------- | -------------- | -------------- | ---------- |
| gzip | 10.18.152.163:9910 | default | token,/tmp/token | ale,flexCounter,hardware,kni,pulse,strata | /Sysdb/cell/1/agent,/Sysdb/cell/2/agent | True |

#### TerminAttr Daemon Device Configuration

```eos
!
daemon TerminAttr
   exec /usr/bin/TerminAttr -cvaddr=10.18.152.163:9910 -cvauth=token,/tmp/token -cvvrf=default -disableaaa -smashexcludes=ale,flexCounter,hardware,kni,pulse,strata -ingestexclude=/Sysdb/cell/1/agent,/Sysdb/cell/2/agent -taillogs
   no shutdown
```

### Logging

#### Logging Servers and Features Summary

| Type | Level |
| -----| ----- |

| Format Type | Setting |
| ----------- | ------- |
| Hostname | hostname |
| Sequence-numbers | true |
| RFC5424 | False |

#### Logging Servers and Features Device Configuration

```eos
!
logging format sequence-numbers
```

## Spanning Tree

### Spanning Tree Summary

STP mode: **mstp**

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
```

## Internal VLAN Allocation Policy

### Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

### Internal VLAN Allocation Policy Device Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

## Interfaces

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 10.0.0.4/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | ROUTER_ID | default | - |

##### ISIS

| Interface | ISIS instance | ISIS metric | Interface mode |
| --------- | ------------- | ----------- | -------------- |
| Loopback0 | IGP | - | passive |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description ROUTER_ID
   no shutdown
   ip address 10.0.0.4/32
   node-segment ipv4 index 2
   isis enable IGP
   node-segment ipv4 index 102 flex-algo LOWLATENCY
   node-segment ipv4 index 202 flex-algo CHEAPBW
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |

#### IP Routing Device Configuration

```eos
!
ip routing
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| default | false |

### Router ISIS

#### Router ISIS Summary

| Settings | Value |
| -------- | ----- |
| Instance | IGP |
| Net-ID | 49.0000.0000.0100.0004.00 |
| Type | level-2 |
| Router-ID | 10.0.0.4 |
| Log Adjacency Changes | True |
| SR MPLS Enabled | True |
| SPF Interval | 2 seconds |
| SPF Interval Wait Time| 10 milliseconds |
| SPF Interval Hold Time| 100 milliseconds |

#### ISIS Route Timers

| Settings | Value |
| -------- | ----- |
| Local Convergence Delay | 10000 milliseconds |
| LSP Out-delay | 2000 milliseconds |

#### ISIS Interfaces Summary

| Interface | ISIS Instance | ISIS Metric | Interface Mode |
| --------- | ------------- | ----------- | -------------- |
| Loopback0 | IGP | - | - |

#### ISIS Segment-routing Node-SID

| Loopback | IPv4 Index | IPv6 Index |
| -------- | ---------- | ---------- |
| Loopback0 | 2 | - |

#### ISIS IPv4 Address Family Summary

| Settings | Value |
| -------- | ----- |
| IPv4 Address-family Enabled | True |
| Maximum-paths | 4 |
| TI-LFA Mode | link-protection |

#### Router ISIS Device Configuration

```eos
!
router isis IGP
   net 49.0000.0000.0100.0004.00
   router-id ipv4 10.0.0.4
   is-type level-2
   log-adjacency-changes
   timers local-convergence-delay 10000 protected-prefixes
   set-overload-bit on-startup 300
   spf-interval 2 10 100
   timers lsp out-delay 2000
   !
   address-family ipv4 unicast
      maximum-paths 4
      fast-reroute ti-lfa mode link-protection
   !
   segment-routing mpls
      no shutdown
```

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65000 | 10.0.0.4 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| maximum-paths 4 ecmp 4 |

#### Router BGP Device Configuration

```eos
!
router bgp 65000
   router-id 10.0.0.4
   no bgp default ipv4-unicast
   maximum-paths 4 ecmp 4
```

## BFD

### Router BFD

#### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 300 | 300 | 3 |

#### Router BFD Device Configuration

```eos
!
router bfd
   multihop interval 300 min-rx 300 multiplier 3
```

## MPLS

### MPLS and LDP

#### MPLS and LDP Summary

| Setting | Value |
| -------- | ---- |
| MPLS IP Enabled | True |
| LDP Enabled | False |
| LDP Router ID | - |
| LDP Interface Disabled Default | - |
| LDP Transport-Address Interface | - |

### MPLS Device Configuration

```eos
!
mpls ip
```

## Multicast

### IP IGMP Snooping

#### IP IGMP Snooping Summary

| IGMP Snooping | Fast Leave | Interface Restart Query | Proxy | Restart Query Interval | Robustness Variable |
| ------------- | ---------- | ----------------------- | ----- | ---------------------- | ------------------- |
| Enabled | - | - | - | - | - |

#### IP IGMP Snooping Device Configuration

```eos
```

### Router Multicast

#### IP Router Multicast Summary

- Software forwarding by the Linux kernel

#### Router Multicast Device Configuration

```eos
!
router multicast
   ipv4
      software-forwarding kernel
```

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |

### VRF Instances Device Configuration

```eos
```

## System L1

### Unsupported Interface Configurations

| Unsupported Configuration | action |
| ---------------- | -------|
| Speed | error |
| Error correction | error |

### System L1 Device Configuration

```eos
!
system l1
   unsupported speed action error
   unsupported error-correction action error
```

## EOS CLI Device Configuration

```eos
!
tunnel-ribs
  tunnel-rib system-tunnel-rib
      source-protocol nexthop-group
      source-protocol rsvp-ler
      source-protocol bgp labeled-unicast
      source-protocol static
      source-protocol ldp
      source-protocol isis flex-algo preference 100
      source-protocol isis segment-routing preference 200
!
vlan 501
  name SVC4-L2EVPN
!
vlan 601
  name SVC6
!
vrf instance SVC6
!
vrf instance SVC7
!
vrf instance SVC8
!
interface Ethernet9.101
  description SVC1-VPWS-SINGLE-2
  !
  encapsulation vlan
      client dot1q 101
!
interface Ethernet9.501
  description SVC4-L2EVPN
  vlan id 501
  !
  encapsulation vlan
    client dot1q 501
  !
  evpn ethernet-segment
      identifier 0020:0000:0000:0000:0501
      route-target import 00:20:00:00:05:01
  !
!
interface Ethernet9.601
  description SVC6-L3EVPN
  vlan id 601
  !
  encapsulation vlan
      client dot1q 601
!
interface Ethernet9.701
  description SVC7-4364
  encapsulation dot1q vlan 701
  vrf SVC7
  ip address 192.168.107.1/24
!
interface Ethernet9.801
  description SVC8-INTERWORKING
  encapsulation dot1q vlan 801
  vrf SVC8
  ip address 192.168.108.1/24
!
interface Ethernet1
  description PE3
  no switchport
  ip address 10.1.0.10/31
  bfd interval 50 min-rx 50 multiplier 3
  isis enable IGP
  isis network point-to-point
  traffic-engineering min-delay static 10 milliseconds
!
interface Ethernet5
  description PE5
  no switchport
  ip address 10.1.0.9/31
  bfd interval 50 min-rx 50 multiplier 3
  isis enable IGP
  isis network point-to-point
  traffic-engineering min-delay static 10000 milliseconds
!
interface Ethernet9
  no switchport
  description CE1
  bgp session tracker ROUTE_REFLECTORS
  no switchport
  evpn ethernet-segment
      identifier 0020:2000:0000:0000:0000
      route-target import 20:20:00:00:00:00
  !
!
interface Loopback0
  ip address 10.0.0.4/32
  node-segment ipv4 index 4
  node-segment ipv4 index 102 flex-algo LOWLATENCY
  node-segment ipv4 index 202 flex-algo CHEAPBW
  isis instance IGP
!
interface Vlan601
  vrf SVC6
  ip address 192.168.206.1/24
!
ip routing vrf SVC6
ip routing vrf SVC7
ip routing vrf SVC8
!
patch panel
  patch subintpo9.101
      connector 1 interface Ethernet9.101
      connector 2 pseudowire bgp vpws SVC1-VPWS-SINGLE-2 pseudowire pw1
!
router bgp 65000
  router-id 10.0.0.4
  maximum-paths 4 ecmp 4
  neighbor IBGP-PEER peer group
  neighbor IBGP-PEER remote-as 65000
  neighbor IBGP-PEER update-source Loopback0
  neighbor IBGP-PEER bfd
  neighbor IBGP-PEER session tracker ROUTE_REFLECTORS
  neighbor IBGP-PEER send-community
  neighbor IBGP-PEER maximum-routes 0
  neighbor 10.0.0.17 peer group IBGP-PEER
  neighbor 10.0.0.18 peer group IBGP-PEER
  !
  vlan 501
      rd 10.0.0.4:10501
      route-target both 0.0.0.0:10501
      redistribute learned
      redistribute static
  !
  vlan 901
      rd 10.0.0.4:10901
      route-target both 0.0.0.0:10901
      redistribute learned
      redistribute static
  !
  vpws SVC1-VPWS-SINGLE-2
      rd 10.0.0.4:11101
      route-target import export evpn 0.0.0.0:11101
      mpls control-word
      label flow
      !
      pseudowire pw1
        evpn vpws id local 11101 remote 21101
  !
  address-family evpn
      neighbor default encapsulation mpls next-hop-self source-interface Loopback0
      next-hop mpls resolution ribs tunnel-rib colored system-colored-tunnel-rib tunnel-rib system-tunnel-rib
      neighbor IBGP-PEER activate
  !
  address-family ipv4
      neighbor IBGP-PEER activate
      neighbor IBGP-PEER additional-paths receive
      neighbor IBGP-PEER additional-paths send limit 2
      redistribute connected
  !
  address-family vpn-ipv4
      neighbor IBGP-PEER activate
  !
  vrf SVC6
      rd 10.0.0.4:20601
      route-target import evpn 0.0.0.0:20601
      route-target export evpn 0.0.0.0:20601
      redistribute connected
      redistribute static
  !
  vrf SVC7
      rd 10.0.0.4:10701
      route-target import vpn-ipv4 0.0.0.0:10701
      route-target export vpn-ipv4 0.0.0.0:10701
      redistribute connected
      redistribute static
  !
  vrf SVC8
      rd 10.0.0.4:10801
      route-target import evpn 0.0.0.0:20801
      route-target import vpn-ipv4 0.0.0.0:20801
      route-target export evpn 0.0.0.0:20801
      route-target export vpn-ipv4 0.0.0.0:20801
      redistribute connected
      redistribute static
  !
  session tracker ROUTE_REFLECTORS
      recovery delay 600 seconds
!
router traffic-engineering
  segment-routing
      rib system-colored-tunnel-rib
      !
      policy endpoint 10.0.0.3 color 30
        binding-sid 1000001
        name PE3_COLOR30
        !
        path-group preference 1
            segment-list label-stack 900001 900006 900005 900004 900003
  !
  flex-algo
      flex-algo 128 LOWLATENCY
        metric min-delay
        color 130
      !
      flex-algo 255 CHEAPBW
        color 230
!
router isis IGP
  net 49.0000.0000.0100.0004.00
  is-type level-2
  timers local-convergence-delay protected-prefixes
  set-overload-bit on-startup 300
  spf-interval 2 10 100
  timers lsp out-delay 2000
  !
  address-family ipv4 unicast
      fast-reroute ti-lfa mode node-protection
  !
  segment-routing mpls
      no shutdown
      flex-algo CHEAPBW level-2 advertised
      flex-algo LOWLATENCY level-2 advertised
!
```
