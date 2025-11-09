---
title: Raspberry Pi 5
layout: page
---

The **Raspberry Pi 5** exists in my term-time accommodation room, and is used for experimentation and to host Home Assistant for my room.

## Pages

- [Deployment guide](./deployment-guide) (steps for deploying all the software onto a fresh Raspberry Pi)

## Hardware

The device is a **Raspberry Pi 5** with 4 GB RAM.

I currently don't have a 6A-capable USB-C cable available, so its input power is limited to 3A.

Its only storage device is a 1 TB SATA SSD connected via a USB to SATA adapter.

## Networking

The Pi 5 has a dynamic private IPv4 address. It has no globally-routable IPv6 address due to university firewalls. Its hostname is `rp5`.

It is connected to the network via a 100 Mbps switch (which has an upstream connection to [Hallnet wired](https://www.lboro.ac.uk/services/it/getting-online/hallnet/)). I plan to upgrade the switch to a faster one.

## Software

The Pi 5 runs **Ubuntu Server 25.10**.
