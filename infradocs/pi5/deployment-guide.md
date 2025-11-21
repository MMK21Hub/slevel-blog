---
title: Raspberry Pi 5 deployment guide
layout: page
---

## Network registration

Before the Pi can gain full network access, it needs to be added as a Hallnet device using the university's web service. You'll need the Pi's MAC address, which should be shown if you boot the Pi with no bootable media and connect it to a display.

Of course, if you are deploying this setup outside of university accommodation, you can skip this step.

## OS Installation

1. Flash the latest version of Ubuntu Server onto a microSD card using Raspberry Pi Imager. Add the following customization options:
   - Hostname: `pi5` (or another hostname)
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
sudo apt install micro btop fastfetch lazygit
```

### Install nice-to-have packages

```bash
sudo apt install iperf3
```

Allow `iperf3` to start as a daemon because why not.

You can also perform a bandwidth test using `iperf3 -c`.

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
2. Set its IPv4 address to something memorable like `100.64.2.10` (the `2` represents it being at uni, and the `10` is because I use multiples of 10 for Pis)

<!-- ### Optional: Allow the Pi to be used as an exit node

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
   ``` -->
