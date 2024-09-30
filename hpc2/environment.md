---
layout: default
title: Environment
parent: HPC2
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
------------------------------- /share/apps/modules/modulefiles/mpi/intel/2023.2/impi/2021.10 -------------------------------
   esmf/8.5.0    fftw/3.3.10    hdf5/1.14.3    nco/5.2.2    netcdf/4.9.2    pio/1.10.1    pnetcdf/1.12.3

----------------------------------- /share/apps/modules/modulefiles/compiler/intel/2023.2 -----------------------------------
   advisor/2023.2.0               dnnl-cpu-gomp/2023.2.0        inspector/2023.2.0                  oclfpga/2023.2.0
   ccl/2021.10.0                  dnnl-cpu-iomp/2023.2.0        intel_ipp_ia32/2021.9.0             oclfpga/2023.2.1 (L,D)
   compiler-rt/2023.2.1    (L)    dnnl-cpu-tbb/2023.2.0         intel_ipp_intel64/2021.9.0          openmpi/4.1
   compiler-rt32/2023.2.1         dnnl/2023.2.0                 intel_ippcp_ia32/2021.8.0           tbb/2021.10.0    (L)
   compiler/2023.2.1       (L)    dpct/2023.2.0                 intel_ippcp_intel64/2021.8.0        tbb32/2021.10.0
   compiler32/2023.2.1            dpl/2022.2.0                  itac/2021.10.0                      udunits/2.2.28
   dal/2023.2.0                   icc/2023.2.1                  mkl/2023.2.0                 (L)    vtune/2023.2.0
   debugger/2023.2.0              icc32/2023.2.1                mkl32/2023.2.0                      zlib/1.2.13
   dev-utilities/2021.10.0        impi/2021.10           (L)    mpi/2021.10.0                (L)

------------------------------------------- /share/apps/modules/modulefiles/core --------------------------------------------
   StdEnv (L)    anaconda3/2023.09-0    gcc/12.3    intel/2023.2 (L)    julia/1.6.7    julia/1.9.4 (D)

  Where:
   L:  Module is loaded
   D:  Default Module
```
The three levels of modules from bottom to top are core modules, modules compiled with a specific compiler, and modules compiled with a specific combination of compiler/MPI, respectively. The compiler/MPI combination of `intel/2023.2` and `impi/2021.10` is automatically loaded when logging in the system (managed by a standard set of modules `StdEnv`, read more [here](https://lmod.readthedocs.io/en/latest/070_standard_modules.html)). To use other compilers, e.g., the GNU compiler, simply run `module swap intel gcc` and `module load openmpi`. Currently, we have the [GNU Compiler Collection](https://gcc.gnu.org) (`gcc`), and [Intel oneAPI Toolkits](https://www.intel.com/content/www/us/en/developer/tools/oneapi/overview.html) (`intel`) installed on the system. Combinations of `intel/impi`, `intel/openmpi`, and `gcc/openmpi` are supported. All libraries are compiled using these combinations of compiler/MPI.

