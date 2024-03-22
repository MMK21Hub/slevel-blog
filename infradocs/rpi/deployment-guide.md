---
title: RPi deployment guide
layout: page
---

A guide to deploy my home server stack on a Raspberry Pi.

## Rough guide

Done from memory without testing. Proper guide coming soon, maybe

## Part 1: Installation and configuration

1. Install the latest Raspberry Pi OS onto an SD card, with SSH access (via pubkey ofc) available for a user called `rpi`, and hostname `rpi`
2. Ensure the two storage SSDs are connected: the 64 GB homelab-data SSD and the 500 GB Immich SSD
3. Install important sysadmin software, notably the `micro` text editor (and add `dust`, `lazygit` and `btop` at some point)
4. Add the SSDs to fstab: (apply with `sudo mount -a`)
```fstab
LABEL="homelab-data-2" /mnt/data   ext4 defaults,rw,noatime,data=ordered 0 0
LABEL="immich" /mnt/immich ext4 defaults,rw,noatime,data=ordered,nofail 0 0
```
5. Increase swapfile size (this is mainly to prevent Immich's machine learning bringing down the system) in `/etc/dphys-swapfile`
```bash
CONF_SWAPFILE=/mnt/immich/swapfile
CONF_SWAPSIZE=8192
CONF_MAXSWAP=8192
```
6. Apply the swapfile changes: `sudo dphys-swapfile {swapoff,setup,swapon}`
7. Install and set up PiVPN - <https://www.pivpn.io/>
7. Install `iperf3`
8. Install Docker: https://docs.docker.com/engine/install/debian/#install-using-the-repository
9. Install Git, configure it, and set up authentication via SSH
```ini
# git config -l
user.name=MMK21
user.email=50421330+MMK21Hub@users.noreply.github.com
core.editor=micro
```
```bash
# cat ~/.ssh/config
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/github
```
10. Clone the Docker compose files from Github: `git clone https://github.com/MMK21Hub/rpi-docker-compose.git ~/docker-compose-configs`

11. Add bash aliases for Docker:
```bash
alias dc='docker compose'
alias up='docker compose up -d'
```
12. Also, hoard Bash history lines
```bash
HISTSIZE=10000
HISTFILESIZE=10000
```
13. Install dependencies for bash scripts: `jq` and `age` (for encryption)
15. Get the Home Assistant Backup private key from Bitwarden and save it to `~/secrets/backup-passwords/home-assistant-db`
16. `chmod 400 ~/secrets/backup-passwords/home-assistant-db`
14. Set up user cron jobs (don't use `sudo`)
```bash
# crontab -l
0 2 * * * /bin/bash /home/pi/docker-compose-configs/backup-file-to-pomf.sh /mnt/data/terraria/worlds/ACMO-S3.wld.bak
0 2 * * * /bin/bash /home/pi/docker-compose-configs/home-assistant/upload-latest-backup.sh
```

### Part 2: Bringing it online

1. `cd ~/docker-compose-configs`
2. Bring up Caddy first becuase it has the definition for the `caddy-network` network (`cd caddy` and then `up`)
2. Bring up `victoria` (VictoriaMetrics) becuse quite a few things send/recieve from it
3. Bring up the other services: `cloudflare-ddns`, `grafana`, `home-assistant`, `immich-app`, `librechat`, `netdata`, `ntfy`, `socks5`, `syncthing`, `terraria` (note that this list changes pretty frequently, so be sure to `ls ~/docker-compose-configs` to check if anything's been missed accidentally)
5. Check CPU/RAM usage with `btop`, check `df -h`
6. Use a web broswer to test that services are running as expected 