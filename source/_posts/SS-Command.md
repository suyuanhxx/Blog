---
title: SS Command
date: 2017-01-07 16:32:19
tags:
---

## bbr
- `yum install -y git`
- `yum install -y vim`
- `wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh` 
- `chmod +x bbr.sh` 
- `./bbr.sh`
<!--more-->   
- `uname -r`
- `sysctl net.ipv4.tcp_available_congestion_control`
- `sysctl net.ipv4.tcp_congestion_control`
- `sysctl net.core.default_qdisc`
- `lsmod | grep bbr`
## SSR
- `git clone -b manyuser https://github.com/shadowsocksr/shadowsocksr.git` 
## salsa20 或 chacha20 或 chacha20-ietf
- `yum install epel-release` 
- `yum install libsodium`
