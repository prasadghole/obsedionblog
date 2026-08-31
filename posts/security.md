---
title: "Security"
date: 2020-10-06
tags: []
publish: true
---

# Five Principals for of embedded security
## Message
Off course this is what you want to protect from intruder.

## Integrity 
Original message sent from sender should not altered when received by receiver.

## Authentication
Message should be received from intended sender party.

## Authorization
Sender of message should have be authorized to execute some action on receptor 

## Anti-replay
A valid message should not be used again by intruder to carry out malicious activities

## Nonreduating
Sender of message should not able to disown the message.

# Encryption types
## Symmetric key cryptography

* Simple
* Fast

## Asymmetric (public key cryptography)
* More failsafe
* slower

# Algorithms security levels
1. MD5 Unsecured
2. SHA-1 Unsecured
3. 

# Hash functions 
## Consistency
Get same value for same input
## compression
Compress large data into small output range
## Lossiness
We loose information from input to output.

# Threat modeling
## What we are building 
## What can go wrong
## How we mitigate it
## How well we done our job.

STRIDE for finding threats


# GPG 
## GPG key usage
1. I want anyone receiving my email to know that I cannot repudiate it. 
Sign my message with private key.
2. I want to verify message I received is sent by person who say he is. 
Verify the signature by senders public key.
3. I want to send message which only intended recipient can read.
Encrypt message with recipient public key.
4. I want to read message i received.
Decrypt message with your private key.


# FOTA
Firmeware over the air. For IOT devices we need to update the firmware on the field.
