---
title: "Software Containers (Singularity)"
teaching: 15
exercises: 15
questions:
- "What is a software container and hoy to use it?"
objectives:
- "Use singularity containers"
keypoints:
- "Containers provide a easy way to keep code and data reproducible by creating a consistent environment for a workflow."
---

## Singularity Containers

Containers are a software technology that allows us to keep control of the environment where a given code runs. Consider for example that you want to run a code in such a way the same code runs on several machines or clusters ensuring that the same libraries are loaded and the same general environment is present. Different clusters could come installed with different compilers, different Linux distributions and different libraries in general. Containers can be used to package entire scientific workflows, software and libraries, and even data and move them to several compute infrastructures with complete reproducibility.

Containers are similar to Virtual Machines, however, the differences are enough to consider them different technologies and those differences are very important for HPC. Virtual Machines takes up a lot of system resources. Each Virtual Machine (VM) runs not just a full copy of an operating system, but a virtual copy of all the hardware that the operating system needs to run. This quickly adds up to a lot of precious RAM and CPU cycles, valuable resources for HPC.

In contrast, all that a container requires is enough of an operating system, supporting programs and libraries, and system resources to run a specific program. From the user perspective, a container is in most cases a single file that contains the file system, ie a rather complete Unix filesystem tree with all libraries, executables, and data that are needed for a given workflow or scientific computation.

There are several container solutions, one prominent example is Docker, however, the main issue with containers is security, despite the name, containers do not actually contain the powers of the user who executes code on them. That is why you do not see Docker installed on an HPC cluster. Using dockers requires superuser access something that on shared resources like an HPC cluster is not widely offered.

Singularity offers an alternative solution to Docker, users can run the prepared images that we are offering on Spruce or bring their own.

For more information about Singularity and complete documentation see: https://singularity.lbl.gov/quickstart

### How to use a singularity Image

There are basically two scenarios, interactive execution and job submission.

#### Interactive Job

If you are using Visit or RStudio, programs that uses the X11 forwarding, ensure to connect first to the cluster with X11 forwarding, before asking for an interactive job.
In order to connect into Spruce with X11 forwarding use:

~~~
ssh -X <username>@spruce.hpc.wvu.edu
~~~
{: .source}


Once you have login into the cluster, create an interactive job with the following command line, in this case we are using standby as queue but any other queue is valid.

~~~
qsub -X -I -q standby
~~~
{: .source}


Once you get inside a compute node, load the module:

~~~
module load singularity/2.5.1
~~~
{: .source}


After loading the module the command singularity is available for usage, and you can get a shell inside the image with:

~~~
singularity shell /shared/software/containers/<Image Name>
~~~
{: .source}


#### Job Submission

In this case you do not need to export X11, just login into Spruce

~~~
ssh <username>@spruce.hpc.wvu.edu
~~~
{: .source}


Once you have login into the cluster, create a submission script ("runjob.pbs" for this example), in this case we are using standby as queue but any other queue is valid.

~~~
#!/bin/sh

#PBS -N JOB
#PBS -l nodes=1:ppn=1
#PBS -l walltime=04:00:00
#PBS -m ae
#PBS -q standby

module load singularity/2.5.1

singularity exec /shared/software/containers/<Image Name> <command_or_script_to_run>
~~~
{: .source}


Submit your job with

~~~
qsub runjob.pbs
~~~
{: .source}

## Excercises

### Interactive

This excercise propose the use of singularity to access RStudio 1.1 and R 3.4.3

Follow the instructions for accesisng an interactive session

The image is located at:

~~~
/shared/software/containers/RStudio-desktop-1.1.423_R-3.4.3.simg
~~~
{: .source}

### Non-interactive




{% include links.md %}
