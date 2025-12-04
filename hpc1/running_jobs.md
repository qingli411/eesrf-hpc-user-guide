---
layout: default
title: Running jobs
parent: HPC1
nav_order: 3
---

# Running jobs

## Slurm

We use [Slurm](https://slurm.schedmd.com) for cluster management and job scheduling. See [here](https://slurm.schedmd.com/quickstart.html) for a more detailed user guide of Slurm.

## Submitting jobs

As mentioned [here](connecting.html#note), you are not allowed to directly run jobs on the login node. Instead, you may submit a job to the computing nodes via Slurm. There are basically two ways you can submit a job as briefly introduced below.

### Batch jobs

You can use `sbatch` to submit a job script for later execution. A typical job script begins with a [shebang](https://en.wikipedia.org/wiki/Shebang_%28Unix%299) line (e.g., `#!/bin/bash`) followed by lines of Slurm directives each begins with `#SBATCH`. These directives tell Slurm some basic information about the job, such as a job name, a filename to save output and error message, the computational resource a job requires, including the number of nodes and CPU cores, and the *wall time* (job execution time in real world, as would be seen on a clock mounted on the wall, after which the job will be cancelled automatically), etc. After these directives, users then include the commands to be run in the script, including the setting of environment variables and the setup of the job. This is the recommended way to submit a job. Below is an example job script to submit a test case of [MPAS-Ocean](https://mpas-dev.github.io/ocean/ocean.html).

```bash
#!/bin/bash
#SBATCH  --job-name=MPASO           # job name ('MPASO' in this example)
#SBATCH  --output=MPASO.%j          # save output message to MPASO.%j where %j is the job ID assigned by Slurm
#SBATCH  --nodes=1                  # number of node requested (1 in this example)
#SBATCH  --ntasks-per-node=16       # number of MPI tasks per node (16 in this example)
#SBATCH  --time=1:00:00             # wall time requested (one hour in this example)

# load necessary modules
module purge
module load intel openmpi zlib hdf5 pnetcdf netcdf pio fftw

# set environment variables for MPAS-Ocean
export NETCDF=${NETCDF_ROOT}
export PNETCDF=${PNETCDF_ROOT}
export PIO=${PIO_ROOT}
export FFTW=${FFTW_ROOT}
export CORE=ocean
export AUTOCLEAN=true
export USE_PIO2=false

# go to the case directory and run the case
case_path="${HOME}/scratch/mpas/ocean/mixed_layer_eddy/0.6km/single_front/forward"
cd ${case_path}
mpirun -n ${SLURM_NTASKS} ./ocean_model -n namelist.ocean -s streams.ocean

```

### Interactive jobs
You can also use `salloc` to allocate resources for an interactive job so that you can SSH to the allocated computing node and run the job interactively as you would do on your personal computer. To allocate one node for one hour, run
```
> salloc --nodes=1 --time=1:00:00
salloc: Granted job allocation 13804
salloc: Waiting for resource configuration
salloc: Nodes node03 are ready for job
```
As shown in the prompt message above, `node03` is allocated. You can then SSH to the allocated node by `ssh node03` and run your job interactively. This is usually used for testing and debugging.

Note that you will not be able to directly SSH to a computing node without an allocation. If you try to SSH to a computing node without first requesting it using `salloc`, your access will be denied and you see something like the following.
```
> ssh node04
Access denied by pam_slurm_adopt: you have no active jobs on this node
Connection closed by 110.1.1.104 port 22
```

If you encounter issues when SSHing to the allocated node, you can try the following command to start a `bash` shell on the allocated node.
```
> srun --nodes=1 --time=1:00:00 --pty bash
```

## Other useful Slurm commands

* `sinfo` shows the state of partitions and nodes managed by Slurm. For example, to check the state of all 22 nodes in partition1 (we currently only have one partition), run

```
> sinfo
PARTITION   AVAIL  TIMELIMIT  NODES  STATE NODELIST
partition1*    up   infinite      1  alloc node01
partition1*    up   infinite     21   idle node[02-22]
```
It has a wide variety of filtering, sorting, and formatting options. Run `man sinfo` to learn more.

* `squeue` shows the state of jobs or job steps. For example, to see the state of the MPAS-Ocean job, run

```
> squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
             13802 partition    MPASO   qingli  R       0:05      1 node02
```
It also has a wide variety of filtering, sorting, and formatting options. By default, it reports the running jobs in priority order and then the pending jobs in priority order. Run `man squeue` to learn more.


* `scancel` is used to cancel a pending or running job or job step. For example, to cancel the above job with job ID of `13802`, run

```
> scancel 13802
```


