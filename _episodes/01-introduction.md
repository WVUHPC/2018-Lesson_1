---
title: "Getting access to the Cluster"
teaching: 15
exercises: 15
questions:
- "How to connect without using passwords?"
objectives:
- "Learn how to connect with SSH to a HPC cluster"
keypoints:
- "Use ssh to connect. Use ssh -X to get X11 Forwarding"
- "On windows you can use PuTTY"
- "To get X Window on Windows use for example MobaXTerm"
---

The most common way of accessing a HPC computer cluster is via a remote shell.
A remote shell allow you to execute commands on another machine same as you do sitting on front of it. A remote shell is good because it also allow other people to do the same, so you get a shared resource being utilized by several users at the same time.

All that you need on your computer is a SSH client, a program on your computer that allow you to connect to the SSH server from another computer. In the old times, people used to create a remote shell using Telnet. SSH provides a secure channel over an unsecured network such as internet. SSH offers similar capabilities to telnet but adding encryption, so all data sent and received between your computer and the remote host is encrypted in such a way that only your computer and the remote computer can see the data. If you want to know more about Secure Shell:

https://en.wikipedia.org/wiki/Secure_Shell


# ssh

Currently WVU has two clusters for HPC, Mountaineer and Spruce. You can access them using SSH.
Both Linux and macOS include an SSH client by default. On Windows machines you need to install an external application. A free application called [PuTTY](https://www.putty.org) offers a simple SSH client and [MobaXTerm](https://mobaxterm.mobatek.net) offers you a full featured SSH client plus the ability to open X11 windows from the remote machine.

To connect to Mountaineer use:

~~~
ssh <username>@mountaineer.hpc.wvu.edu
~~~
{: .source}

For Spruce:

~~~
ssh <username>@spruce.hpc.wvu.edu
~~~
{: .source}

Once you enter on the system, you can start typing commands. You can open several connections simultaneously. Each connection is independent of each other.

> ## Entering on Spruce
>
> Using the username and password given to you for this training or using your own account login into Spruce and execute the command hostname.
> What do you see on the terminal?
>
> > ## Solution
>>  You should get:
>>
>> spruce.hpc.wvu.edu
> {: .solution}
{: .challenge}

## tmux

Power users can benefit from a terminal multiplexer such as tmux.
tmux is a terminal multiplexer.
It lets you switch easily between several programs in one terminal, detach them
 (they keep running in the background) and reattach them to a different terminal.

tmux allows users to keep several virtual windows and panels open from a single connection. It offers also preserve the terminal status in case of disconnection from the server.

To use tmux, first connect to the server and execute the command

~~~
tmux
~~~
{: .source}

You can create new virtual windows with `CTRL-b c`, you move between windows with `CTRL-b n` and `CTRL-b p`. You can detach from your multiplexed terminals with `CTRL-b d`.

If for some reason you lost the connection to the server or you detached from the multiplexer all that you have to do to reconnect is to execute the command:

~~~
tmux a
~~~
{: .source}

In tmux, hit the prefix `CTRL+b` and then:

### Sessions
~~~
    :new<CR>  new session
    s  list sessions
    $  name session
~~~
{: .source}

### Windows (tabs)

~~~
    c  create window
    w  list windows
    n  next window
    p  previous window
    f  find window
    ,  name window
    &  kill window
~~~
{: .source}

### Panes (splits)

~~~
    %  vertical split
    "  horizontal split
    o  swap panes
    q  show pane numbers
    x  kill pane
    +  break pane into window (e.g. to select text by mouse to copy)
    -  restore pane from window
    ⍽  space - toggle between layouts
    q (Show pane numbers, when the numbers show up type the key to goto that pane)
    { (Move the current pane left)
    } (Move the current pane right)
    z toggle pane zoom
~~~
{: .source}

### Copy model

~~~
    [  Copy mode
~~~
{: .source}

### Others

~~~
    d  detach
    t  big clock
    ?  list shortcuts
    :  prompt
~~~
{: .source}

{% include links.md %}
