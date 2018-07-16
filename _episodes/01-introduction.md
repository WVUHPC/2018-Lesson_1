---
title: "Getting access to the Cluster"
teaching: 45
exercises: 15
questions:
- "How to connect without using passwords?"
objectives:
- "Learn how to connect with SSH to a HPC cluster"
keypoints:
- "Use ssh to connect. Use ssh -X to get X11 Forwarding"
- "On windows you can use PuTTY"
- "To get X Window on Windows use MobaXTerm"
- "tmux is a terminal multiplexer that can boost your interaction with
HPC cluster"
---

The most common way of accessing a HPC computer cluster is via a remote shell.
A remote shell allow you to execute commands on another machine same as you do sitting on front of it. A remote shell is good because it also allow other people to do the same, so you get a shared resource being utilized by several users at the same time.

All that you need on your computer is a SSH client, a program on your computer that allow you to connect to the SSH server from another computer. In the old times, people used to create a remote shell using Telnet. SSH provides a secure channel over an unsecured network such as internet. SSH offers similar capabilities to telnet but adding encryption, so all data sent and received between your computer and the remote host is encrypted in such a way that only your computer and the remote computer can see the data. If you want to know more about Secure Shell see at [Wikipedia](https://en.wikipedia.org/wiki/Secure_Shell)


## ssh

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

> ## Login on Spruce
>
> Using the username and password given to you for this training or using your own account login into Spruce and execute the command `hostname`.
>
> What do you see on the terminal?
>
>> ## Solution
>>  You should get:
>>
>> spruce.hpc.wvu.edu
> {: .solution}
{: .challenge}

## Connecting with SSH without password

If you do not have a pair of public and private keys on your own computer, create a new pair with (Linux and Mac only)

~~~
$ ssh-keygen -t ecdsa
~~~
{: .source}

~~~
Generating public/private ecdsa key pair.
Enter file in which to save the key (/users/gufranco/.ssh/id_ecdsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /users/gufranco/.ssh/id_ecdsa.
Your public key has been saved in /users/gufranco/.ssh/id_ecdsa.pub.
The key fingerprint is:
ca:fe:2c:df:10:a0:97:ca:fe:fd:34:5c:34:ce:33:64 gufranco@srih0001.hpc.wvu.edu
The key's randomart image is:
+--[ECDSA  256]---+
|      o=.. o=    |
|     ..+o += .   |
|    . o .o .=    |
|     . . ..  o   |
|      . .        |
|     . = +       |
|      o o .      |
|                 |
|                 |
+-----------------+
~~~
{: .output}

Now we need to transfer the public key to be accepted as a authorized key on the remote server

~~~
ssh-copy-id -i .ssh/id_ecdsa.pub <USERNAME>@spruce.hpc.wvu.edu
~~~
{: .source}

Next time, log in to spruce with that username will happen without asking you for password. As far as you are using the same machine your private key will give you access to the remote machine.

This procedure will not work if you need to use DUO authentication, for example for external access out of campus network.

> ## ECDSA vs DSA vs RSA
>
> There are several digital signing algorithms. The best known are RSA (Used by SSH2 for signing), DSA and ECDSA.
>
> In practice this is the rational for when use each:
>
> RSA key will work everywhere. ECDSA support is newer, so some old client or server may have trouble with ECDSA keys. DSA used to work everywhere, as per the SSH standard, but recently OpenSSH 7.0 and higher no longer accept DSA keys by default.
>
> [ECDSA](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm) is computationally lighter, a smaller key will give you the same level of protection than a much larger RSA key.
>
> Right now, if you use large enough keys (2048 bits for RSA or DSA, 256 bits for ECDSA) you are considered safe. Key size is specified with the -b parameter.
>
{: .callout}

## tmux

For normal usage, the terminal that you get is probably enough.
Power users can benefit from a terminal multiplexer such as tmux.

It lets you switch easily between several virtual terminals organized in panels, windows and sessions. One big advantage of terminal multiplexing is that all those virtual terminals are still alive when you logout from the system.
You can work for a while remotely, close the connection and reconnect again, attaching your tmux session and continuing exactly where you left your work.

tmux allows users to keep several sessions. You can attach only one session each time. Each session can have several windows, you can create several windows but it is better not to have more than 10. Each window can be split in panes you can move around between the different panes on a window, the different windows of a session and you can leave one session and reattach another one.

To use tmux, first connect to the server and execute the command

~~~
tmux
~~~
{: .source}

You can create new virtual windows with <kbd>Ctrl</kbd>+<kbd>b</kbd> <kbd>c</kbd>, you move between windows with <kbd>Ctrl</kbd>+<kbd>b</kbd> <kbd>n</kbd> and <kbd>Ctrl</kbd>+<kbd>b</kbd> <kbd>p</kbd>. You can detach from your multiplexed terminals with <kbd>Ctrl</kbd>+<kbd>b</kbd> <kbd>d</kbd>.

If for some reason you lost the connection to the server or you detached from the multiplexer all that you have to do to reconnect is to execute the command:

~~~
tmux a
~~~
{: .source}

In tmux, hit the prefix <kbd>Ctrl</kbd>+<kbd>b</kbd> followed by one of the options below:

## Sessions
~~~
    :new<CR>  new session
    s  list sessions
    $  name session
~~~
{: .source}

## Windows (tabs)

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

## Panes (splits)

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

## Copy model

~~~
    [  Copy mode
~~~
{: .source}

## Others

~~~
    d  detach
    t  big clock
    ?  list shortcuts
    :  prompt
~~~
{: .source}

## Command line arguments for tmux

~~~
    tmux ls                       list sessions
    tmux new                      new session
    tmux rename -t <ID> new_name  rename a session
    tmux kill-session -t <ID>     kill session by target
~~~
{: .source}

> ## Exercise: Using tmux
>
> Using the tables above follow this simple challenge with tmux
>
> 1. Log in to Spruce and create a tmux session
>
> 2. Inside the session create a new window
>
> 3. Go back to window 0 and create a horizontal pane and inside on of those panes create a vertical pane.
>
> 4. Create a big clock pane
>
> 5. Detach from your current session, close your terminal and reconnect.
> Log in again on Spruce and reattach your session.
>
> 6. Now that you are again in you original session, create a new session.
> You will be automatically redirected there. Leave your session, check the list of sessions.
>
> 7. Kill the second session (session ID is 1)
>
>{: .source}
{: .challenge}

Now we are ready to learn the first commands on our next episode.

{% include links.md %}
