---
title: "Logging in to Spruce"
teaching: 45
exercises: 15
questions:
- "How to connect without using passwords?"
objectives:
- "Learn how to connect to Spruce in several ways"
keypoints:
- "Use ssh to connect to Spruce"
- "On windows you can use PuTTY"
- "To get X Window on Windows use for example MobaXTerm"
---

# ssh

Currently WVU has two clusters for HPC, mountaineer and spruce. You can access them using SSH.
SSH provides a secure channel over an unsecured network such as internet.
Both Linux and macOS commonly include the SSH client by default. On Windows machines you can use a free application called PuTTY or MobaXTerm.

To connect to Mountaineer use:

~~~
ssh <username>@mountaineer.hpc.wvu.edu
~~~
{: .source}

For Spruce

~~~
ssh <username>@spruce.hpc.wvu.edu
~~~
{: .source}

Once you enter on the system, you can start typing commands. You can open several connections simultaneously. Each connection is independent of each other.

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
