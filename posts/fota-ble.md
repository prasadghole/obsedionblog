---
title: "Firmware update over bluetooth"
date: 2022-11-04
tags: []
publish: false
---

## Speed
Therotically speed supported is 1 M

## Network topology
### Broadcasting
#### Broadcaster
Sends nonconnectable advertising packetes periodically to anyone willing to receive them.

#### Observer
Repeatedly scans the preset frequencies to receive any nonconnectable advertising packetes
currently being broadcast ed.


### Connection
#### Central (Master)
Repeatedly scans the preset frequencies for connectabel advertising packets and
when suitable initiates a connection. Once the connection is established, the central
manages the time and initiates the periodic data exchange.
#### Peripheral *(slave)
A device that sends connectabel advertising packets periodically and accepts incoming
connections, the peripheral follows the central's timing and exchange data regularly
with it.

## Protocol basics
### Physical Layers
It uses radio of 2.4 GHz ISM band into 40 channels (2.4000 to 2.4538) channel 37,38,39 are 
used for advertising.

The standard uses frequency hopping spread spectrum, radio hops between these 2 channels
on each connection event.

channel = (curr_chanel + hop) / 37

value of hop is communicated when connection is established.

### Link Layer
It is more computationally expensive hence usually implemented in hardware.
Functionality includes
- Preamble, access address
- CRC generation
- Data whitening
- Random Number Generator
- AES encryption

a link layers define following roles
- Advertiser
A device sending advertising packets.
- Scanner
A device scanning for advertising packets.
- Master
A device initiating communication.
- Slave
A device accepts connection request and follows master timing.

When not in active connection we have Advertiser and scanner roles 
change to master and slave when connected.

#### Bluetooth address
 Similar to MAC address in ethernet we have 48 bits unique address made up of
 There are 2 types of address
- Public device address
This is factory programmed and must be registered with IEEE and will never change in 
device life time.

- Random device address
This can reprogrammed or dynamically generated at runtime.
