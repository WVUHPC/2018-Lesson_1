---
title: "Environment Modules"
teaching: 15
exercises: 15
questions:
- "How to load modules to access software that I want to use for my research?"
objectives:
- "Learn about *modules*, how to search, load and unload modules"
keypoints:
- "You can preload modules for each login by adding the load line on your .bashrc"
---

## Environment Modules

The modules software package allows you to dynamically modify your user environment by using “modulefiles.”

Each modulefile contains the information needed to configure the shell for an application. After the modules software package is initialized, the environment can be modified on a per-module basis using the module command, which interprets modulefiles. Typically, modulefiles instruct the module command to alter or set shell environment variables such as PATH, MANPATH, and others. The modulefiles can be shared by many users on a system, and users can have their own collection to supplement or replace the shared modulefiles.

As a user, you can add and remove modulefiles from the current environment. The environment changes contained in a modulefile can also be summarized through the module show command. You are welcome to change modules in your `.bashrc` or `.cshrc`, but be aware that some modules print information (to standard error) when loaded, this should be directed to a file or /dev/null when loaded in an initialization script.

More information on modules can be found by typing module help on the NICS systems. Ignore the module init* commands – these modify a `.modulerc` file which is incompatible with the way NICS modules are set up. If you run into any issues, remove any `.modulerc` and log in again.

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

The basic procedure is to locate modules on a folder accessible by relevant users
and add the variable `MODULEPATH` to your `.bashrc`

`MODULEPATH` controls the path that the module command searches when looking for
modulefiles.  
Typically, it is set  to a  default  value by the bootstrap procedure.  
`MODULEPATH` can be set using ’module use’ or by the module initialization
script to search group or personal modulefile directories before  or  after
the master modulefile directory.

## Modules on Spruce

~~~
$ module avail

---------------- /usr/share/Modules/modulefiles -----------------
dot     modules null    use.own

------------------ /usr/share/Modules/software ------------------
atomistic/abinit/8.4.2_intel17       genomics/eigensoft
atomistic/abinit/8.4.4_gcc63         genomics/emboss
atomistic/abinit/8.6.3_gcc63         genomics/errcorr_tools
atomistic/dftbplus/18.1              genomics/express
atomistic/elk/4.3.6_gcc63            genomics/falcon
atomistic/gromacs/2016.3             genomics/falcon_171012
atomistic/gromacs/2016.3_serial      genomics/fasta36
atomistic/gromacs/2016.4             genomics/fastqc
atomistic/lammps/2016.11.17          genomics/fastx_toolkit
atomistic/lammps/2017.08.11          genomics/gatk/2.8
atomistic/lammps/2018.03.16          genomics/gatk/3.5
atomistic/namd/2018-04-26            genomics/gatk/4.0
atomistic/namd/2.12                  genomics/genometools
atomistic/namd/2.12_iverbs           genomics/genomics-core
atomistic/octopus/6.0_gcc63          genomics/hmmer
atomistic/octopus/7.1_gcc63          genomics/htslib
atomistic/vasp/5.3.3_intel17         genomics/igv
atomistic/vasp/5.4.4_intel17         genomics/lastz
atomistic/vasp/5.4.4_intel17_ompi212 genomics/ltrfinder
cfd/ansys/14.5.7                     genomics/mrsfast
cfd/ansys/forte/17.2                 genomics/muscle
cfd/converge/2.4.12                  genomics/pbdagcon
chemistry/amber/12                   genomics/phase
chemistry/amber/14                   genomics/phrap
chemistry/amber/16                   genomics/picard-tools
chemistry/autodock_vina              genomics/pindel/0.2.5b1
chemistry/gamess                     genomics/pindel/0.2.5b8
chemistry/gaussian/g03               genomics/plink
chemistry/gaussian/g09               genomics/qiime
chemistry/gromacs/4.6.5              genomics/repeatexplorer
chemistry/gromacs/5.0.5              genomics/repeatmasker
chemistry/gromacs/5.0.5-gpu          genomics/rsem
chemistry/gromacs/5.1.2              genomics/samtools/0.1.19
chemistry/gromacs/5.1.2-gpu          genomics/samtools/1.2
chemistry/namd/ibverbs/2.10          genomics/sga
chemistry/namd/ibverbs/2.11          genomics/shapeit
chemistry/namd/ibverbs/2.9           genomics/sickle
chemistry/namd/mpi                   genomics/soapdenovo
chemistry/orca                       genomics/sratoolkit
chemistry/schrodinger                genomics/structure
data/cdf/3.5.0.2                     genomics/svseq
data/hdf5/1.8.12                     genomics/tabix
data/mongodb/3.6.1                   genomics/tablet
data/sqlite/3.9.2                    genomics/tophat2
engineering/damask/2.0.1             genomics/trf
engineering/damask/2.0.1_petsc364    genomics/trinity/2.0.6
genomics/abyss/1.3.6                 genomics/trinity/2.2.0
genomics/abyss/1.9.0                 genomics/vcflib
genomics/allpaths                    genomics/vcftools/0.1.14
genomics/beagle                      gnu/coreutils
genomics/bedtools                    gnu/parallel
genomics/bioperl                     mae/cmg/2014.10
genomics/blasr                       mae/cmg/2015.10
genomics/blast/2.2.28                mae/cmg/2017.10
genomics/blast/2.3.0                 mae/elk/2.2.10
genomics/bowtie                      mae/elk/2.3.16
genomics/bowtie2                     singularity/2.5.1
genomics/breakdancer                 statistics/matlab/2014a
genomics/bwa/0.7.10                  statistics/matlab/2016b
genomics/bwa/0.7.12                  statistics/matlab/2018a
genomics/canu/1.6                    statistics/rstudio/0.97.551
genomics/celera                      visualization/paraview
genomics/clumpp                      visualization/visit/2.10
genomics/cufflinks                   visualization/visit/2.10.2
genomics/delly                       visualization/visit/2.12.2
genomics/distruct                    visualization/visit/2.12.3
genomics/dwgsim                      visualization/vtk/7.0.0

---------------- /usr/share/Modules/development -----------------
compilers/binutils/2.26                   libraries/hdf5/1.8.17_intel
compilers/cuda/7.5                        libraries/hdf5/1.8.18_gcc63
compilers/gcc/4.9.0                       libraries/hdf5/1.8.19_gcc63
compilers/gcc/5.3.0                       libraries/hdf5/1.8.19_gcc63_ompi212
compilers/gcc/6.3.0                       libraries/hdf5/1.8.19_intel17
compilers/gcc/7.3.0                       libraries/hdf5/1.8.19_intel17_impi17
compilers/idl/8.5.1                       libraries/jemalloc/3.6.0
compilers/intel/13.0.1                    libraries/libgd/2.2.4
compilers/intel/14.0                      libraries/log4cpp/1.1.2
compilers/intel/15.0.1                    libraries/mkl/11.2.1
compilers/intel/17.0.1                    libraries/mkl/4.1.1.036
compilers/intel/17.0.1_MKL_only           libraries/netcdf/4.4.1.1_gcc63
compilers/java/bazel-0.5.2                libraries/netcdf/fortran-4.4.4_gcc63
compilers/java/jdk1.8.0                   libraries/openblas/0.2.20
compilers/java/jre1.8.0                   libraries/openfoam/3.0+
compilers/julia/0.6.2                     libraries/petsc/3.6.4
compilers/python/2.7.13                   libraries/petsc/3.7.3
compilers/python/2.7.14                   libraries/petsc/3.7.7
compilers/python/3.6.0                    libraries/petsc/3.8.3
compilers/python/3.6.5                    libraries/Qt/4.7.3
compilers/R/3.1.0                         libraries/Qt/5.5.1
compilers/R/3.3.2                         libraries/R/Rhipe
compilers/R/3.4.1                         libraries/sqlite/3.9.2
compilers/ruby/2.2.3                      libraries/suitesparse/5.0
compilers/swig/3.0.7                      libraries/yices2/2.5.3
environment/gcc-mpi                       linalg/armadillo/7.600.2
environment/gcc-serial                    linalg/armadillo/7.800.1
environment/intel                         linalg/openblas/0.2.19
git/2.8.3                                 mpi/intel/4.1.0.024
kitware/cmake/3.9.0                       mpi/intel/4.1.1.036
libraries/arpack-ng/3.5.0_gcc63_ompi212   mpi/intel/5.0.3.048
libraries/arpack-ng/3.5.0_intel17_ompi212 mpi/mpich2/1.2.1
libraries/bioconductor/3.2                mpi/mvapich2/2.0.1
libraries/boost/1.57.0                    mpi/mvapich2/2.2.0
libraries/boost/1.66                      mpi/openmpi/1.10.7_gcc63
libraries/bupc/2.2                        mpi/openmpi/1.6.5
libraries/DFS/myhadoop                    mpi/openmpi/1.8.4
libraries/fftw/2.1.5                      mpi/openmpi/2.0.1
libraries/fftw/3.3.4                      mpi/openmpi/2.0.2_gcc63
libraries/fftw/3.3.4-mpi                  mpi/openmpi/2.1.1_gcc63
libraries/fftw/3.3.6_gcc63                mpi/openmpi/2.1.1_gcc63_cxxbindings
libraries/fftw/3.3.6_intel17              mpi/openmpi/2.1.2_gcc63
libraries/gsl/2.1                         mpi/openmpi/2.1.2_intel17
libraries/gtest/1.7.0                     mpi/ucx/1.3
libraries/hdf5/1.8.12                     utils
libraries/hdf5/1.8.13_intel               xalt/0.6.0
~~~
{: .source}

> ## Exercise: Using modulefiles
>
> 1. Check the modules that you currently have and clean (purge) your environment from them. Check again and confirm that no module is loaded.
>
> 2. Check which versions of Python, R and GCC you have from the RHEL itself. Try to get and idea of how old those three components are. For python and R all that you have to do is enter the corresponding command (`R` or `python`). For GCC you need to use `gcc --version` and see the date of those programs.
>
> 3. Now lets get newer version of those 3 components by loading the corresponding modules. Search for the module for Python 3.6.0 and R 3.4.1 and GCC 6.3.0 and load the corresponding modules. To make things easier, you can use check the availability of modules just in the compilers section.
>
> ~~~
> module avail compilers
> ~~~
> {: .source}
>
> 4. Check again which version of those 3 components you have now. Notice that in the case of Python 3, the command python still goes towards the old python 2.6.6, as the python 3.x interpreter is not backwards compatible with python 2.x the new command is called `python3`, check its version by entering the command.
>
> 5. Go back and purge all the modules from your environment. We will now explore why is important to use a recent compiler. Try to compile the code at `1.IntroHPC/4.Modules/lambda_c++14.cpp`. Go to the folder and execute:
>
> ~~~
> g++ lambda_c++14.cpp
> ~~~
> {: .source}
>
> At this point you should have receive a list of errors, that is because even if the code is C++ it uses elements of the language that were not present at that time on C++ Specification. The code actually uses C++14 and only recent versions of GCC allows for these declarations. Lets check how many GCC compilers we have available on Spruce.
>
> ~~~
> module avail compilers/gcc
> ~~~
> {: .source}
>
> Now from that list, start loading and trying to compile the code as indicated above. Which versions of GCC allow you to compile the code? Try also the Intel compilers. In the case of intel the command to compile the code is
> ~~~
> icpc lambda_c++14.cpp
> ~~~
> {: .source}
>
> Try with all the Intel compilers, it will fail with all of them. That is because the default standard for the Intel C++ compiler is not C++14, you need to declare it explicitly and only for Intel Compiler suite 17.0.1
>
> ~~~
> icpc lambda_c++14.cpp -std=c++14
> ~~~
> {: .source}
>
>Now it should be clearer why modules is an important feature of any HPC infrastructure as it allows you to use several compilers, libraries and packages in different versions. On a normal computer, you usually have just one.
>{: .source}
{: .challenge}

{% include links.md %}
