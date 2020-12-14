---
title: fedora dnf replacing yum
author: PipisCrew
date: 2019-11-27
categories: [linux]
toc: true
---

DNF is a software package manager that installs, updates, and removes packages on RPM-based Linux distributions. DNF or Dandified yum is the next generation version of yum. It roughly maintains CLI compatibility with yum and defines a strict API for extensions and plugins. DNF began as a fork of Yum and is meant to address several longstanding problems in Yum, the most pressing of which is dependency resolution and interaction with online repositories.

https://fedoraproject.org/wiki/DNF?rd=Dnf

ex.
```js
//search
sudo dnf search quiterss

//install
sudo dnf install quiterss

//download only all dependencies
//https://www.ostechnix.com/download-rpm-package-dependencies-centos/
yum install --downloadonly mysql-utilities-1.6.5-1.fc27.noarch.rpm
```

You might use **RPM commands for lower-level** troubleshooting, but in most cases DNF provides all the functionality in a more friendly manner.
```js
//lists the dependencies
//http://www.softpanorama.org/Utilities/rpm.shtml
rpm -qp --provides x.rpm
```

## Disable YUM/DNF Repo manually editing repo file

```js
//https://www.if-not-true-then-false.com/2010/yum-remove-repo-repository-yum-disable-repo-repository/
Edit repo file on /etc/yum.repos.d/ as root and change enabled to 0
## Change
enabled=1
## To
enabled=0
```

* * *

## AppImage

https://fedoraproject.org/wiki/AppImage

ex.
https://github.com/martinrotter/rssguard/releases

origin - https://www.pipiscrew.com/?p=15663 fedora-dnf-replacing-yum