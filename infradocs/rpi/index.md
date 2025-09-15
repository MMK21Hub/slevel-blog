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

### Public

- **Slevel blog** - You are here! ([blog.slevel.xyz](https://blog.slevel.xyz/))

### My projects

Some of my personal coding projects are self-hosted here.

- [**Hide and Squeak**](https://github.com/MMK21Hub/hide-and-squeak) - Run your own large-scale IRL hide and seek game (WIP) ([has.slevel.xyz](https://has.slevel.xyz/))
- **Support Watcher**, **GOV.UK Watcher**, **Summer of Making Watcher**, **Daydream Watcher** - Prometheus metric exporters for various things I care about. Source code available on [my GitHub](https://github.com/MMK21Hub/).

### Invite-only

- **Immish** - [Immich](https://immich.app/) + Mish ([photos.slevel.xyz](https://photos.slevel.xyz/) or `:2024`)
- **Grafana** - Observability, or something ([grafana.slevel.xyz](https://grafana.slevel.xyz/))
- **Terraria server** - Terraria server for my friends. Uses the [ryshe/terraria](https://hub.docker.com/r/ryshe/terraria/) Docker image ([terraria.slevel.xyz](https://terraria.slevel.xyz/))
- **Home Assistant** - Feature-packed platform for home automation shenanigans ([home.slevel.xyz](https://home.slevel.xyz/) or `:8123`)
- **Open WebUI** - Chat with LLMs ([chat.slevel.xyz](https://chat.slevel.xyz/))
- **Tinyproxy** - Evade network restrictions. Not currently in use
- **Vikunja** - My to-do list ([todo.slevel.xyz](https://todo.slevel.xyz/))

### Internal

- **Caddy** - Reverse proxy for (almost) all my selfhosted web services (ping it at [ping.slevel.xyz](https://ping.slevel.xyz/))
- **Netdata** - Provides detailed monitoring for a massive range of performance and stability metrics (`:19999`)
- **Syncthing** - Peer-to-peer file synchronisation tool. Currently unused
- **Synthetic Monitoring Agent** - A [Synthetic Monitoring Agent](https://github.com/grafana/synthetic-monitoring-agent) (by Grafana) instance used by my Grafana Cloud instance for uptime checks (`:4050`)
- **VictoriaMetrics** - Time-series database for storing Prometheus metrics that can be shown in Grafana
- **Loki** - Log storage database, used by Grafana (`:3050`)
- **Promtail** - Forwards system log files to Loki
