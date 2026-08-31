---
title: "Virtual Box Networking"
date: 2021-03-27
tags: [development, networking]
description: "Host to guest networking access with VirtualBox"
publish: false
---

# Network Settings
VirtualBox provide multiple ways to connect guest to host OS along with external 
internet acsess. I have summarized high level configuration with respect to access
to internet and host environment.

| Type              | Internet Access | Guest Acess | Host Access | IP Address  |
|-------------------|-----------------|-------------|-------------|-------------|
| NAT               | Yes             | No          | No          | Auto DHCP   |
| NAT Network       | Yes             | No          | No          | Auto DHCP   |
| Bridged Adapter   | Yes             | Yes         | Yes         | Auto/manual |
| Internal Network  | No              | No          | No          | Auto/manual |
| Host-only Adapter | No              | No          | Yes         | Auto/manual |
| Generic Drive     |                 |             |             |             |

[Referance 1](https://www.nakivo.com/blog/virtualbox-network-setting-guide/)

## NAT
This is very basic default confiugration used for access to internet connection
to host.
