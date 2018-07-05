---
title: "Version Control (git)"
teaching: 105
exercises: 15
questions:
- "How to keep track of changes in text files"
objectives:
- "Learn the basic commands of git to version control text files"
keypoints:
- "Version control systems were created to keep track of changes in a set of files."
- "They work better with text files"
---

## Environmental Modules

The modules software package allows you to dynamically modify your user environment by using “modulefiles.”

Each modulefile contains the information needed to configure the shell for an application. After the modules software package is initialized, the environment can be modified on a per-module basis using the module command, which interprets modulefiles. Typically, modulefiles instruct the module command to alter or set shell environment variables such as PATH, MANPATH, and others. The modulefiles can be shared by many users on a system, and users can have their own collection to supplement or replace the shared modulefiles.

As a user, you can add and remove modulefiles from the current environment. The environment changes contained in a modulefile can also be summarized through the module show command. You are welcome to change modules in your .bashrc or .cshrc, but be aware that some modules print information (to standard error) when loaded, this should be directed to a file or /dev/null when loaded in an initialization script.

More information on modules can be found by typing module help on the NICS systems. Ignore the module init* commands – these modify a .modulerc file which is incompatible with the way NICS modules are set up. If you run into any issues, remove any .modulerc and log in again.

## Basic arguments

The following table lists the most common module command options

| Command	| Description |
|:--------|:------------|
| module list	  | Lists modules currently loaded in a user's environment. |
| module avail  | Lists all available modules on a system. |
| module show	  | Shows environment changes that will be made by loading a given module. |
| module load	  | Loads a module. |
| module unload	| Unloads a module. |
| module help	  | Shows help for a module. |
| module swap	  | Swaps a currently loaded module for an unloaded module. |

## Creating a private repository

On day 3 we will show and example of how to create a private module.
With private modules you or your research group can have control on the software
of interest for the group.

The basic procedure is to locate modules on a folder accessible by relevant users
and add the variable `MODULEPATH` to your `.bashrc`

MODULEPATH controls the path that the module command searches when looking for
modulefiles.  
Typically, it is set  to a  default  value by the bootstrap procedure.  
MODULEPATH can be set using ’module use’ or by the module initialization
script to search group or personal modulefile directories before  or  after
the master modulefile directory.

## Modules on Spruce

~~~
$ module avail

------------------------------------------/usr/share/Modules/software -------------------------------------------------------------
atomistic/abinit/8.4.2_intel17       chemistry/namd/ibverbs/2.10          genomics/emboss                      genomics/shapeit
atomistic/abinit/8.4.4_gcc63         chemistry/namd/ibverbs/2.11          genomics/errcorr_tools               genomics/sickle
atomistic/abinit/8.6.3_gcc63         chemistry/namd/ibverbs/2.9           genomics/express                     genomics/soapdenovo
atomistic/dftbplus/18.1              chemistry/namd/mpi                   genomics/falcon                      genomics/sratoolkit
atomistic/elk/4.3.6_gcc63            chemistry/orca                       genomics/falcon_171012               genomics/structure
atomistic/gromacs/2016.3             chemistry/schrodinger                genomics/fasta36                     genomics/svseq
atomistic/gromacs/2016.3_serial      data/cdf/3.5.0.2                     genomics/fastqc                      genomics/tabix
atomistic/gromacs/2016.4             data/hdf5/1.8.12                     genomics/fastx_toolkit               genomics/tablet
atomistic/lammps/2016.11.17          data/mongodb/3.6.1                   genomics/gatk/2.8                    genomics/tophat2
atomistic/lammps/2017.08.11          data/sqlite/3.9.2                    genomics/gatk/3.5                    genomics/trf
atomistic/lammps/2018.03.16          engineering/damask/2.0.1             genomics/gatk/4.0                    genomics/trinity/2.0.6
atomistic/namd/2018-04-26            engineering/damask/2.0.1_petsc364    genomics/genometools                 genomics/trinity/2.2.0
atomistic/namd/2.12                  genomics/abyss/1.3.6                 genomics/genomics-core               genomics/vcflib
atomistic/namd/2.12_iverbs           genomics/abyss/1.9.0                 genomics/hmmer                       genomics/vcftools/0.1.14
atomistic/octopus/6.0_gcc63          genomics/allpaths                    genomics/htslib                      gnu/coreutils
atomistic/octopus/7.1_gcc63          genomics/beagle                      genomics/igv                         gnu/parallel
atomistic/vasp/5.3.3_intel17         genomics/bedtools                    genomics/lastz                       mae/cmg/2014.10
atomistic/vasp/5.4.4_intel17         genomics/bioperl                     genomics/ltrfinder                   mae/cmg/2015.10
atomistic/vasp/5.4.4_intel17_ompi212 genomics/blasr                       genomics/mrsfast                     mae/cmg/2017.10
cfd/ansys/14.5.7                     genomics/blast/2.2.28                genomics/muscle                      mae/elk/2.2.10
cfd/ansys/forte/17.2                 genomics/blast/2.3.0                 genomics/pbdagcon                    mae/elk/2.3.16
cfd/converge/2.4.12                  genomics/bowtie                      genomics/phase                       singularity/2.5.1
chemistry/amber/12                   genomics/bowtie2                     genomics/phrap                       statistics/matlab/2014a
chemistry/amber/14                   genomics/breakdancer                 genomics/picard-tools                statistics/matlab/2016b
chemistry/amber/16                   genomics/bwa/0.7.10                  genomics/pindel/0.2.5b1              statistics/matlab/2018a
chemistry/autodock_vina              genomics/bwa/0.7.12                  genomics/pindel/0.2.5b8              statistics/rstudio/0.97.551
chemistry/gamess                     genomics/canu/1.6                    genomics/plink                       visualization/paraview
chemistry/gaussian/g03               genomics/celera                      genomics/qiime                       visualization/visit/2.10
chemistry/gaussian/g09               genomics/clumpp                      genomics/repeatexplorer              visualization/visit/2.10.2
chemistry/gromacs/4.6.5              genomics/cufflinks                   genomics/repeatmasker                visualization/visit/2.12.2
chemistry/gromacs/5.0.5              genomics/delly                       genomics/rsem                        visualization/visit/2.12.3
chemistry/gromacs/5.0.5-gpu          genomics/distruct                    genomics/samtools/0.1.19             visualization/vtk/7.0.0
chemistry/gromacs/5.1.2              genomics/dwgsim                      genomics/samtools/1.2
chemistry/gromacs/5.1.2-gpu          genomics/eigensoft                   genomics/sga

----------------------------------------- /usr/share/Modules/development ------------------------------------------------------
compilers/binutils/2.26                   libraries/arpack-ng/3.5.0_intel17_ompi212 libraries/petsc/3.7.3
compilers/cuda/7.5                        libraries/bioconductor/3.2                libraries/petsc/3.7.7
compilers/gcc/4.9.0                       libraries/boost/1.57.0                    libraries/petsc/3.8.3
compilers/gcc/5.3.0                       libraries/boost/1.66                      libraries/Qt/4.7.3
compilers/gcc/6.3.0                       libraries/bupc/2.2                        libraries/Qt/5.5.1
compilers/gcc/7.3.0                       libraries/DFS/myhadoop                    libraries/R/Rhipe
compilers/idl/8.5.1                       libraries/fftw/2.1.5                      libraries/sqlite/3.9.2
compilers/intel/13.0.1                    libraries/fftw/3.3.4                      libraries/suitesparse/5.0
compilers/intel/14.0                      libraries/fftw/3.3.4-mpi                  libraries/yices2/2.5.3
compilers/intel/15.0.1                    libraries/fftw/3.3.6_gcc63                linalg/armadillo/7.600.2
compilers/intel/17.0.1                    libraries/fftw/3.3.6_intel17              linalg/armadillo/7.800.1
compilers/intel/17.0.1_MKL_only           libraries/gsl/2.1                         linalg/openblas/0.2.19
compilers/java/bazel-0.5.2                libraries/gtest/1.7.0                     mpi/intel/4.1.0.024
compilers/java/jdk1.8.0                   libraries/hdf5/1.8.12                     mpi/intel/4.1.1.036
compilers/java/jre1.8.0                   libraries/hdf5/1.8.13_intel               mpi/intel/5.0.3.048
compilers/julia/0.6.2                     libraries/hdf5/1.8.17_intel               mpi/mpich2/1.2.1
compilers/python/2.7.13                   libraries/hdf5/1.8.18_gcc63               mpi/mvapich2/2.0.1
compilers/python/2.7.14                   libraries/hdf5/1.8.19_gcc63               mpi/mvapich2/2.2.0
compilers/python/3.6.0                    libraries/hdf5/1.8.19_gcc63_ompi212       mpi/openmpi/1.10.7_gcc63
compilers/python/3.6.5                    libraries/hdf5/1.8.19_intel17             mpi/openmpi/1.6.5
compilers/R/3.1.0                         libraries/hdf5/1.8.19_intel17_impi17      mpi/openmpi/1.8.4
compilers/R/3.3.2                         libraries/jemalloc/3.6.0                  mpi/openmpi/2.0.1
compilers/R/3.4.1                         libraries/libgd/2.2.4                     mpi/openmpi/2.0.2_gcc63
compilers/ruby/2.2.3                      libraries/log4cpp/1.1.2                   mpi/openmpi/2.1.1_gcc63
compilers/swig/3.0.7                      libraries/mkl/11.2.1                      mpi/openmpi/2.1.1_gcc63_cxxbindings
environment/gcc-mpi                       libraries/mkl/4.1.1.036                   mpi/openmpi/2.1.2_gcc63
environment/gcc-serial                    libraries/netcdf/4.4.1.1_gcc63            mpi/openmpi/2.1.2_intel17
environment/intel                         libraries/netcdf/fortran-4.4.4_gcc63      mpi/ucx/1.3
git/2.8.3                                 libraries/openblas/0.2.20                 utils
kitware/cmake/3.9.0                       libraries/openfoam/3.0+                   xalt/0.6.0
libraries/arpack-ng/3.5.0_gcc63_ompi212   libraries/petsc/3.6.4

~~~
{: .source}


{% include links.md %}
