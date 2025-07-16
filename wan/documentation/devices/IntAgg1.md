# IntAgg1

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
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Multicast](#multicast)
  - [Router Multicast](#router-multicast)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
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
| Management1 | OOB_MANAGEMENT | oob | default | 192.168.0.56/24 | - |

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
   ip address 192.168.0.56/24
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
| Timestamp | traditional year timezone |
| Hostname | hostname |
| Sequence-numbers | false |
| RFC5424 | False |

#### Logging Servers and Features Device Configuration

```eos
!
logging format timestamp traditional year timezone
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
| Loopback0 | ROUTER_ID | default | - |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | ROUTER_ID | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description ROUTER_ID
   no shutdown
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

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 1000 | - |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| maximum-paths 4 ecmp 4 |

#### Router BGP Peer Groups

##### EVPN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| Next-hop unchanged | True |
| Source | Loopback0 |
| BFD | True |
| Ebgp multihop | 3 |
| Send community | all |
| Maximum routes | 0 (no limit) |

##### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

#### Router BGP EVPN Address Family

##### EVPN Peer Groups

| Peer Group | Activate | Route-map In | Route-map Out | Encapsulation | Next-hop-self Source Interface |
| ---------- | -------- | ------------ | ------------- | ------------- | ------------------------------ |
| EVPN-OVERLAY-PEERS | True |  - | - | default | - |

#### Router BGP Device Configuration

```eos
!
router bgp 1000
   no bgp default ipv4-unicast
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS next-hop-unchanged
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
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

## Multicast

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

## Filters

### Prefix-lists

#### Prefix-lists Summary

##### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 10.251.99.0/28 eq 32 |

#### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 10.251.99.0/28 eq 32
```

### Route-maps

#### Route-maps Summary

##### RM-CONN-2-BGP

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | permit | ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY | - | - | - |

#### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
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
no router bgp 1000
no interface Loopback0
!
no ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
!
no route-map RM-CONN-2-BGP
!
interface Ethernet1
  description host1
  no switchport
  ip address 100.200.10.21/30
!
interface Ethernet49
  description PE1
  no switchport
  ip address 100.1.0.1/31
!
interface Ethernet50
  description PE2
  no switchport
  ip address 100.2.0.1/31
!
ip route 192.168.9.1/32 100.1.0.0
ip route 192.168.9.10/32 100.1.0.0
!
router bgp 100
  maximum-paths 2
  bgp additional-paths install
  neighbor 100.1.0.0 remote-as 65000
  neighbor 100.1.0.0 local-as 300 no-prepend replace-as
  neighbor 100.1.0.0 maximum-routes 0
  neighbor 100.2.0.0 remote-as 65000
  neighbor 100.2.0.0 local-as 200 no-prepend replace-as
  neighbor 100.2.0.0 maximum-routes 0
  redistribute connected
!
```
