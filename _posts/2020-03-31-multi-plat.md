---
title: Multi-Platform Docker Builds
author: PipisCrew
date: 2020-03-31
categories: [docker]
toc: true
---

There’s a fantastic project called [QEMU](https://www.qemu.org/) that can emulate a whole bunch of platforms. With the recent [buildx](https://github.com/docker/buildx) work, it’s easier than ever to use QEMU with Docker.

The QEMU integration relies on a Linux kernel feature with the slightly cryptic name of the [binfmt_misc handler](https://en.wikipedia.org/wiki/Binfmt_misc). When Linux encounters an executable file format it doesn’t recognise (i.e. one for a different architecture), it will check with the handler if there any “user space applications” configured to deal with the format (i.e. an emulator or VM). If there are, it will pass the executable to the application.

https://www.docker.com/blog/multi-platform-docker-builds/

origin - https://www.pipiscrew.com/?p=17854 multi-platform-docker-builds