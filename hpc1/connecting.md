---
layout: default
title: Connecting
parent: HPC 01
nav_order: 2
---

# Connecting

## On campus
If you are connected to the HKUST(GZ) network, you can connect to the server using SSH. The IP address is `10.120.16.38`. On Unix-like systems such as MacOS and Linux, you can do this directly in your Terminal app by `ssh username@10.120.16.38`. On Windows, you need to use an SSH client app, such as [MobaXterm](https://mobaxterm.mobatek.net), [PuTTY](https://www.putty.org), or [Xshell](https://www.xshell.com/en/xshell/).

## Off campus
To use the server from outside the HKUST(GZ) network, you should first connect to the HKUST(GZ) VPN. Visit [https://remote.hkust-gz.edu.cn](https://remote.hkust-gz.edu.cn) to start. Once you are connected to the HKUST(GZ) VPN, you can log in the server using SSH.

## Note
Please note that you are now connected to the login node of the HPC system, not the computing nodes. The login node is used to provide login service to all users. It is fine to do light interactive work such as editing the source code, setting up experiments, or compiling the code on the login node. But please **do not** run CPU- or memory-intensive jobs on the login node -- that will significantly degrade the performance of the login node and affect all users. You should allocate those heavy computing jobs to the computing nodes (see [Running jobs](running_jobs.html) for instructions).

