---
title: "Torque and Moab"
teaching: 45
exercises: 15
questions:
- "How to submit jobs on the HPC cluster?"
objectives:
- "Show the user commands for Torque and Moab. The queue system used on Spruce"
keypoints:
- "It is a good idea to keep aliases to common torque commands for easy execution."
---

## TORQUE

TORQUE is a resource management system for submitting and controlling jobs on
supercomputers, clusters, and grids.
TORQUE manages jobs that users submit to various queues on a computer system,
each queue representing a group of resources with attributes necessary
for the queue's jobs.

This is a list of frequently used TORQUE commands:

| Command | Purpose |
|:--------|:--------|
| qsub	  | Submit a job. |
| qstat	  | Monitor the status of a job. |
| qdel	  | Terminate a job prior to its completion. |

TORQUE includes numerous directives, which are used to specify resource
requirements and other attributes for batch and interactive jobs.
TORQUE directives can appear as header lines (lines that start with #PBS)
in a batch job script or as command-line options to the qsub command.

## Submission scripts

A TORQUE job script for a serial job might look like this:

~~~
#!/bin/bash
#PBS -k o
#PBS -l nodes=1:ppn=1,walltime=00:30:00
#PBS -M username@mix.wvu.edu
#PBS -m abe
#PBS -N JobName
#PBS -j oe
#PBS -q standby

cd $PBS_O_WORKDIR
./a.out
~~~
{: .source}

The following table describes the most basic directives

| TORQUE directive	| Description |
|:------------------|:------------|
|#PBS -k o	| Keeps the job output |
|#PBS -l nodes=1:ppn=1,walltime=00:30:00	| Indicates the job requires one node, one processor per node, and 30 minutes of wall-clock time |
|#PBS -M username@mix.wvu.edu	| Sends job-related email to username@mix.wvu.edu |
|#PBS -m abe	| Sends email if the job is (a) aborted, when it (b) begins, and when it (e) ends |
|#PBS -N JobName	| Names the job JobName |
|#PBS -j oe	| Joins standard output and standard error |
|#PBS -q standy | Submit the job on the standby queue |

A parallel job using MPI could be like this:

~~~
#!/bin/bash
#PBS -k o
#PBS -l nodes=1:ppn=16,walltime=30:00
#PBS -M username@mix.wvu.edu
#PBS -m abe
#PBS -N JobName
#PBS -j oe
#PBS -q standby

cd $PBS_O_WORKDIR
mpirun -np 12 -machinefile $PBS_NODEFILE ./a.out
~~~
{: .source}

The directives are very similat to the serial case

| TORQUE directive	| Description |
|:------------------|:------------|
|#PBS -l nodes=1:ppn=16,walltime=00:30:00	| Indicates the job requires one node, using 16 processors per node, and 30 minutes of runtime. |

### Job Arrays

Job array is a way to submit many jobs that can be indexed. The jobs are
independent between them but you can submit them with a single qsub

~~~
#!/bin/sh

#PBS -N <name_${PBS_ARRAYID}
#PBS -t <num_range>
#PBS -l nodes=<number_of_nodes>:ppn=<PPN number>,walltime=<time_needed_by_job>
#PBS -m ae
#PBS -M <email_address>
#PBS -q <queue_name>

cd $PBS_O_WORKDIR
# Enter the command here
mpirun -np <PPN number> ./a.out
~~~
{: .source}

### Environment variables

We are using PBS_O_WORKDIR to change directory to the place where the job was submitted
The following environment variables will be available to the batch job.

| Variable | Description |
|:---------|:------------|
|PBS_O_HOST| the name of the host upon which the qsub command is running. |
|PBS_SERVER| the hostname of the pbs_server which qsub submits the job to. |
|PBS_O_QUEUE | the name of the original queue to which the job was submitted. |
|PBS_O_WORKDIR | the absolute path of the current working directory of the qsub command. |
|PBS_ARRAYID | each member of a job array is assigned a unique identifier (see -t) |
|PBS_ENVIRONMENT | if set to PBS_BATCH is a batch job, if set to PBS_INTERACTIVE is an interactive job. |
|PBS_JOBID| the job identifier assigned to the job by the batch system. |
|PBS_JOBNAME| the job name supplied by the user. |
|PBS_NODEFILE| the name of the file contain the list of nodes assigned to the job (for parallel and cluster systems). |
|PBS_QUEUE| the name of the queue from which the job is executed. |

### Montioring jobs

To monitor the status of a queued or running job, use the qstat command from Torque
of showq from Moab.

Useful qstat options include:

| qstat option |	Description |
|:-------------|:-------------|
|-Q |show all queues available |
|-u user_list	| Displays jobs for users listed in user_list |
|-a	| Displays all jobs |
|-r	| Displays running jobs |
|-f	| Displays the full listing of jobs (returns excessive detail) |
|-n	| Displays nodes allocated to jobs |

Moab showq offers:

| showq option |	Description |
|:-------------|:-------------|
| -b	| blocked jobs only |
| -c	| details about recently completed jobs. |
| -g	| grid job and system id's for all jobs. |
| -i	| extended details about idle jobs. |
| -l	| local/remote view. For use in a Grid environment, displays job usage of both local and remote compute resources.
| -n	| normal showq output, but lists job names under JOBID |
| -o	| jobs in the active queue in the order specified (uses format showq -o <specifiedOrder>). Valid options include REMAINING, REVERSEREMAINING, JOB, USER, STATE, and STARTTIME. The default is REMAINING. |
| -p	| only jobs assigned to the specified partition. |
| -r	| extended details about active (running) jobs.  |
| -R	| only jobs which overlap the specified reservation. |
| -u	| specified user's jobs. Use showq -u -v to display the full username if it is truncated in normal -u output. |
| -v	| local and full resource manager job IDs as well as partitions. |
| -w	| only jobs associated with the specified constraint. Valid constraints include user, group, acct, class, and qos. |

### Deleting jobs

With Torque you can use `qdel`. Moab uses `mjobctl -c`. For example:

~~~
qdel 1045
~~~
{: .source}

~~~
mjobctl -c 1045
~~~
{: .source}

{% include links.md %}
