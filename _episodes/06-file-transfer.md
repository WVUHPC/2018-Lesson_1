---
title: "Transferring Files"
teaching: 45
exercises: 15
questions:
- "How transfer files from/to cluster to/from my workstation?"
objectives:
- "Show the use of rsync"
keypoints:
- "On windows, there is no simple replacement for rsync. You can use the file trasfer application that comes with PuTTY"
---

## Rsync for secure transfer of files 

For replicating datasets between the HPC clusters and your workstation,
or between two filesystems on an HPC cluster, rsync offers powerful
functionality beyond that of cp or scp.
With rsync you can copy directories between your workstation and the HPC
clusters  - or between different filesystems - in such a way that permission
and file modification timestamps are preserved, and that only files which
have changed are transferred.

The basic usage of rsync is:

~~~
rsync [options] source [source] destination
~~~
{: .source}

Where source is a list of one or more source files or directories to copy and destination is a directory into which to copy
source. Commonly useful options are:

| Option | Description |
|:-------|:------------|
| a | "Archive" mode - permissions and timestamps of the source are replicated at the destination. |
| v | "Verbose". |
| n | "dry run" - don't actually do anything, just indicate what would be done. |

Whether rsync treats destination as a new name for the copy of source, a parent directory into which to copy source, or a parent directory into which to place the contents of source, depends on the exact context of the command. For this reason, it is highly advisable to first run rsync with -n and -v to see exactly what rsync will do before issuing the "real" command, eg:

~~~
$ rsync -nav source destination
$ rsync -av source destination
~~~
{: .source}

#{% include links.md %}
