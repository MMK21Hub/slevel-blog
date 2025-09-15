---
title: Raspberry Pi 400
layout: page
---

My **Raspberry Pi 400** acts as a central home server, hosting various internal and public services.

## Pages

- [Deployment guide](./deployment-guide) (steps for deploying all the software onto a fresh Raspberry Pi)

## Networking

The Pi 400 has a static IPv4 address of `192.168.1.20` and hostname `rpi`.

## Software

The Pi 400 runs Debian, specifically Debian GNU/Linux 12 (bookworm).

## Services

### Private

- **Caddy** - Reverse proxy for (almost) all my selfhosted web services
- **Immish** - [Immich](https://immich.app/) + Mish
- **Grafana** - Observability, or something
- **Terraria server** - Terraria server for my friends. Uses the [ryshe/terraria](https://hub.docker.com/r/ryshe/terraria/) Docker image

### Internal

- **Home Assistant** - Feature-packed platform for home automation shenanigans
