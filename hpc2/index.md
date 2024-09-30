---
layout: home
title: HPC2
nav_order: 3
has_children: true
---

# HPC2

## Overview
This second HPC server at EESRF has 19 computing nodes connected by InfiniBand network. Two of them are large memory nodes, each of which has four Intel Xeon Gold 5318H CPUs (2.5GHz, 18 cores per CPU) and 2 TB of DDR4 memory. The rest are regular computing nodes, each of which has two Intel Xeon Platinum 8374C CPUs (2.7GHz, 32 cores per CPU) and 256GB of DDR4 memory. In total, there are 1368 CPU cores in the system. The total available storage is ~772 TB, shared by all users and mounted at `/share`. We currently have users' home directory in `/share/home` and a shared space for common data used by multiple users (e.g., input data for CESM) in `/share/project`.

This storage has redundancy, so we won't lose data if one or two hard drives in the storage system fail. But there is no backup -- so if you mistakenly delete something, we will not be able to retrieve it. So it is a good idea to always back up important data on your local drive. A good strategy is the so-called 3-2-1 backup rule, which means that you should have 3 copies of your data on 2 different media, with 1 copy being off-site.
