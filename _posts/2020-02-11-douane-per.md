---
title: Douane personal firewall for GNU/Linux
author: PipisCrew
date: 2020-02-11
categories: [app,linux]
toc: true
---

http://douaneapp.com/

Douane is not using iptables at all. It uses Netfilter which is used by iptable.
https://www.digitalocean.com/community/tutorials/a-deep-dive-into-iptables-and-netfilter-architecture

  https://project-insanity.org/blog/2017/03/30/application-firewall-douane-for-archlinux/

  http://tuxdiary.com/2015/03/14/douane/

2020 Guide for installing on Ubuntu v18.04 (Bionic) - https://gitlab.com/douaneapp/Douane/merge_requests/92  ([mirror](https://docdroid.net/q1j9I6D))

## Troubleshooting

  https://www.reddit.com/r/archlinux/comments/5rqcvs/installing_dkms_modules_failed_when_installing/
  https://www.reddit.com/r/ManjaroLinux/comments/3mopuh/kernel_headers_not_found/
  https://forum.antergos.com/topic/8419/help-with-that/42?page=3
  https://www.dedoimedo.com/computers/linux-per-application-firewall.html
  https://github.com/Douane/douane-daemon/issues/3#issuecomment-42027773
  https://github.com/Douane/Douane/issues/39
  https://aur.archlinux.org/cgit/aur.git/?h=douane-dialog-git
  https://aur.archlinux.org/cgit/aur.git/?h=douane-daemon-git
  https://aur.archlinux.org/cgit/aur.git/?h=douane-dkms-git
  https://aur.archlinux.org/cgit/aur.git/?h=douane-configurator-git

similar - 
https://github.com/evilsocket/opensnitch (GNU/Linux port of the 'Little Snitch' application firewall. 'Little Snitch' is MAC firewall)
https://www.opensnitch.io/
https://github.com/subgraph/fw-daemon

#firewall

origin - http://www.pipiscrew.com/?p=11194 douane-personal-firewall-for-gnulinux