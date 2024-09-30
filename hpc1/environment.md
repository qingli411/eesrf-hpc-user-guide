---
layout: default
title: Environment
parent: HPC1
nav_order: 2
---

# Environment

## Lmod

[Lmod](https://lmod.readthedocs.io/en/latest/index.html) is a Lua based module system that helps manage the user environment (`PATH`, `LD_LIBRARY_PATH` etc.) through module files. It supports hierarchical `MODULEPATH`. We use Lmod to provide and manage different versions of libraries compiled by different combinations of compilers and MPI libraries.

## Some useful `module` commands

| --------------------------------- | --------------------------------------------------------------------- |
| Command                           | Description                                                           |
| --------------------------------- | --------------------------------------------------------------------- |
| `module avail`                    | List available modules in `MODULEPATH`                                |
| --------------------------------- | --------------------------------------------------------------------- |
| `module list`                     | List active modules in the user environment                           |
| --------------------------------- | --------------------------------------------------------------------- |
| `module load [module]`            | Load a module file in the users environment                           |
| --------------------------------- | --------------------------------------------------------------------- |
| `module unload [module]`          | Remove a loaded module from the user environment                      |
| --------------------------------- | --------------------------------------------------------------------- |
| `module swap [module1] [module2]` | Replace `module1` with `module2`                                      |
| --------------------------------- | --------------------------------------------------------------------- |
| `module purge`                    | Remove all modules from the user environment                          |
| --------------------------------- | --------------------------------------------------------------------- |
| `module use [-a] [path]`          | Prepend or Append path to `MODULEPATH`                                |
| --------------------------------- | --------------------------------------------------------------------- |
| `module unuse [path]`             | Remove path from `MODULEPATH`                                         |
| --------------------------------- | --------------------------------------------------------------------- |

Like many other commands in Linux, you can use `man module` or `module --help` to find more instructions on how to use it. See also [here](https://lmod.readthedocs.io/en/latest/010_user.html) for a user guide for Lmod.

## Modules on this machine

On this machine, we adopt the naming convention described [here](https://lmod.readthedocs.io/en/latest/055_module_names.html) and module hierarchy described [here](https://lmod.readthedocs.io/en/latest/080_hierarchy.html). Running `module avail` gives the following three levels of modules.

```
------------------------------- /public/apps/module/modulefiles/mpi/gcc/12.3/openmpi/4.1 --------------------------------
   esmf/8.5.0    fftw/3.3.10    hdf5/1.14.1    netcdf/4.9.2    pio/1.10.1    pnetcdf/1.12.3

----------------------------------- /public/apps/module/modulefiles/compiler/gcc/12.3 -----------------------------------
   openmpi/4.1 (L)    zlib/1.2.13

----------------------------------------- /public/apps/module/modulefiles/core ------------------------------------------
   R/4.3.1        anaconda3/2023.07-2    cmake/3.27.4 (L)    intel/2023.2    julia/1.9.3  (D)    nvidia/23.7
   StdEnv  (L)    cdo/2.2.1              gcc/12.3     (L)    julia/1.6.7     matlab/2018a

  Where:
   L:  Module is loaded
   D:  Default Module
```
The three levels of modules from bottom to top are core modules, modules compiled with a specific compiler, and modules compiled with a specific combination of compiler/MPI, respectively. The compiler/MPI combination of `gcc/12.3` and `openmpi/4.1` is automatically loaded when logging in the system (managed by a standard set of modules `StdEnv`, read more [here](https://lmod.readthedocs.io/en/latest/070_standard_modules.html)). To use other compilers, e.g., the Intel compiler, simply run `module swap gcc intel` and `openmpi` compiled with Intel compiler will automatically be swapped and reloaded. Currently, we have the [GNU Compiler Collection](https://gcc.gnu.org) (`gcc`), [Intel oneAPI Toolkits](https://www.intel.com/content/www/us/en/developer/tools/oneapi/overview.html) (`intel`), and [Nvidia HPC SDK](https://developer.nvidia.com/hpc-sdk) (including the PGI compiler; `nvidia`) installed on the system, but only [OpenMPI](https://www.open-mpi.org) (`openmpi`) is supported at this moment. All libraries are compiled using these combinations of compiler/MPI.

