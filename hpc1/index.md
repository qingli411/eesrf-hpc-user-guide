---
layout: home
title: HPC 01
nav_order: 2
has_children: true
---

# HPC 01

## Overview
This first HPC server at EESRF has 22 computing nodes connected by InfiniBand network. Each computing node has two Intel Xeon Gold 6348 CPU @ 2.60GHz (56 CPU cores per node) and 256GB of DDR4 memory. In total, there are 1232 CPU cores in the system. The total available storage is ~300TB, shared by all users and mounted at `/public`. We currently have users' home directory in `/public/home` and a shared space for common data used by multiple users (e.g., input data for CESM) in `/public/project`.

This storage has redundancy, so we won't lose data if one or two hard drives in the storage system fail. But there is no backup -- so if you mistakenly delete something, we will not be able to retrieve it. So it is a good idea to always back up important data on your local drive. A good strategy is the so-called 3-2-1 backup rule, which means that you should have 3 copies of your data on 2 different media, with 1 copy being off-site.

