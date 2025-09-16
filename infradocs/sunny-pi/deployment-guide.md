---
title: Sunny Pi deployment guide
layout: page
---

## OS Installation

1. Flash the latest version of Ubuntu Server onto a microSD card using Raspberry Pi Imager. Add the following customization options:
   - Hostname: `sunny` (or another hostname)
   - Username: `mish` (or another username) and a password of your choice
   - Set time zone and keyboard layout
   - Enable SSH with public-key authentication only
2. Insert the microSD card into the Pi, connect power and network cables
3. SSH into the Pi to perform the rest of the setup

### Update packages

```bash
sudo apt update
sudo apt upgrade
```

More than likely, `apt` will prompt you to reboot:

```bash
sudo reboot
```

## Install useful packages

```bash
sudo apt install micro btop fastfetch
```

### Install nice-to-have packages

```bash
sudo apt install iperf3
```

Allow `iperf3` to start as a daemon because why not.

You can also perform a bandwidth test using `iperf3 -c`. I got 888 Mbps to my PC, and 791 Mbps to the Pi 400.

## Set up Tailscale

### Install Tailscale

See <https://tailscale.com/download/linux/> for instructions.

### Connect to the tailnet

Connect the Pi to the `mmk21hub.github` tailnet (use Github OAuth to sign in to Tailscale).

```bash
sudo tailscale up
```

Check that the host has appeared on the [Tailscale dashboard](https://login.tailscale.com/admin/machines). Then,

1. Disable key expiry for the device
2. Set its IPv4 address to something memorable like `100.64.1.40` (I chose `40` to match the end of its private IP address on the local network)

### Allow the Pi to be used as an exit node

1. [Enable IP forwarding](https://tailscale.com/kb/1019/subnets?tab=linux#enable-ip-forwarding) in `sysctl`:

   ```bash
   echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
   echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
   sudo sysctl -p /etc/sysctl.d/99-tailscale.conf
   ```

2. [Enable UDP performance optimizations](https://tailscale.com/kb/1320/performance-best-practices#ethtool-configuration) using an `ethtool` script:

   ```bash
   printf '#!/bin/sh\n\nethtool -K %s rx-udp-gro-forwarding on rx-gro-list off \n' "$(ip -o route get 8.8.8.8 | cut -f 5 -d " ")" | sudo tee /etc/networkd-dispatcher/routable.d/50-tailscale
   sudo chmod 755 /etc/networkd-dispatcher/routable.d/50-tailscale
   ```

   Test that the script works and activate the optimizations:

   ```bash
   sudo /etc/networkd-dispatcher/routable.d/50-tailscale
   test $? -eq 0 || echo 'An error occurred.'
   ```

3. Start advertising the Pi as a Tailscale exit node:

   ```bash
   sudo tailscale up --advertise-exit-node
   ```

### Allow the home network to be accessed via the Pi

Enable subnet routing on the Pi:

```bash
sudo tailscale set --advertise-routes=192.0.1.0/24
```

Then, approve the subnet route in the Tailscale dashboard.
