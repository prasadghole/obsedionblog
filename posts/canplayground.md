---
title: "CAN Playground"
date: 2022-07-05
tags: [can]
description: "Can bus on PC"
publish: true
---

# CAN Playground
Sometime instead of testing CAN communication on actual hardware interface, we can
simulate multiple node communication and logic on PC environment. Once tested just
by changing CAN interface we can test on real hardware.

python-can modules virtual interface has a limitation that it can communicate only
in single process [link](https://python-can.readthedocs.io/en/master/interfaces/virtual.html).
Hence to test we may have to create two threads and have separate UI or console to be manged.

## CAN Remote
[Python CAN Remote](https://github.com/christiansandberg/python-can-remote) provide solution
where we start a central server through which CAN messages are exchanged.

### Start server

```
python -m can_remote --interface=virtual --channel=0 --bitrate=500000
```

### CAN send script

```
import can
import time

# Create a connection to server. Any config is passed to server.
bus = can.Bus('ws://localhost:54701/',
bustype='remote',
bitrate=500000,
receive_own_messages=True)

# Send messages
for i in range(10):
  msg = can.Message(arbitration_id=0x12345, data=[1,2,3,4,5,6,7,8])
  bus.send(msg)
  time.sleep(1)

# Disconnect
bus.shutdown()

```

### CAN reception script
```
import can

# Create a connection to server. Any config is passed to server.
bus = can.Bus('ws://localhost:54701/',
bustype='remote',
bitrate=500000,
receive_own_messages=True)

while(True):
  msg2 = bus.recv()
  print(msg2)

# Disconnect
bus.shutdown()
```
