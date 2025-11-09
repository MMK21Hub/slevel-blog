---
title: Sunny Pi
layout: page
---

**Sunny Pi** is a Raspberry Pi 4 (Model B, rev 1.5) (2 GB RAM) that serves as a backup for some of the most important services provided by the [Pi 400](/infradocs/rpi). Its hostname is `sunny`.

## Pages

- [Deployment guide](./deployment-guide) (steps for deploying all the software onto a fresh Raspberry Pi)

## Hardware

The device is a **Raspberry Pi 4 Model B** (rev 1.5) with 2 GB RAM.

It's powered by a 15W USB PD power supply connected via a USB-C cable.

It uses a 64 GB microSD card for its root filesystem.

## Networking

Sunny Pi has a static IPv4 address of `192.168.1.40` and hostname `sunny`.

## Software

Sunny Pi uses Ubuntu Server, specifically Ubuntu Server 25.04 (Plucky Puffin).

## Redundancy with Pi 400

### Limitations of the redundant setup

The main single point of failure that `sunny` and `rpi` share is their network connection, as they are both connected to the same network switch. The switch also has a single dependency on a Devolo Powerline adapter. While the switch has operated without issues for 2 years (deployed Oct 2023), the Powerline adapter has gone down in the past, taking anything connected to the switch offline. I plan to remove this single point of failure by connecting `sunny` to a different Powerline adapter.
