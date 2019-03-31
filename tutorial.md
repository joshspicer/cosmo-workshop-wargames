# Linux CLI / Bandit Workshop

Linux is an operating system that sits the at core of much of the technology we interact with daily. Linux is free, secure, and having to work with it on the job is unavoidable.

We'll start the workshop by reviewing some common and good-to-know linux commands.  We'll then move into Bandit ["War Games"](http://overthewire.org/wargames/bandit/), an interactive shell-based game that reinforces basic commands and teaches security concepts.

## Why Learn Linux?

Linux knowledge is invaluable in the CS field. Odds are servers you'll interact with on the job will be running some distro of Linux. In addition, small or embedded systems often run some flavor of Linux.  Ever used a raspberry pi? Those devices are generally running Raspbian, a Linux distribution.  Linux provides a stable development environment, and of course is free and open for users to get started with!

## Setup 

Before we start, lets get our enviornments set up.

### Khoury Account

Khoury college provides a Linux server for students to utilize. You connect to this server over SSH, a protocol that forwards all the terminal commands you type to the remote server.  You can adminsister remote servers from your own computer this way.  We're going to SSH into the Khoury College servers to practice some basics.

Let's create your CCIS/Khoury account. This is the same account you use for Bottlenose!  Note: If you aren't a CCIS student you can skip this step and just connect directly to Over The Wire (more on that later!).

* You can create your account [here](https://www.khoury.northeastern.edu/systems/getting-started/)
* If you have an account and forgot your password, you can reset it [here](https://my.ccs.neu.edu/forgot/password)
* If you have an account but forgot your username check [here](https://my.ccs.neu.edu/forgot/username)


### MacOS/Linux

Open up your terminal program. On MacOS this can be done by opening Spotlight (CMD+Spacebar) and typing in "Terminal". 

You can now connect to our college SSH server by typing 
`ssh <username>@login.ccs.neu.edu`

To make it easier to connect in the future you can add the following configuration to your ssh config. Open up the file by typing `vim ~/.ssh/config`.  Press "i" to enter vim's insert (typing) mode.
```bash
 Host ccis
      Hostname login.ccs.neu.edu
      User <YOUR USERNAME>

```
You can save the file by entering `ESC :wq`.  This will (w)rite the file and (q)uit vim. Now all I have to type is `ssh ccis` and all the information is entered for me.

### Windows

You'll need to install a program like [PuTTY](https://bit.ly/2pV44Vj). 

After installing PuTTY, open the program and enter `login.ccs.neu.edu` as the hostname. You'll then be able to add in your username and password.

## The Basics

Great - at this point you should be ssh'd into the server and ready to practice some commands!  Linux at its core is just a collection of files organized into different directories. Check what directory you're in by typing `pwd` (Print Working Directory).

```bash
-bash-4.2$ pwd
/home/joshua
```

All commands you run will be executed with this directory (my home directory) as context.  When cloning something like a git repo, those files will be cloned into whatever your working directory is, unless you specify otherwise.

Lets fire off a few other commands while we're here.
* `ls` - lists all files and directories in the current working directory
* `cd <PATH>` - (c)hange (d)irectory to the given path. 
* `mkdir <NAME>` - make a new directory in the current working directory
* `touch <NAME>` - Creates a new (empty) file in the working directory

```bash
bash-4.2$ pwd
/home/joshua
-bash-4.2$ ls
cs3650       hw05         My Music     Systems       Visual Studio 2012
Desktop      hw07         My Pictures  tmp
-bash-4.2$ mkdir CoSMO
-bash-4.2$ ls
CoSMO        cs3650       hw05         My Music     Systems          Visual Studio 2008
Desktop      hw07         My Pictures  tmp
-bash-4.2$ cd Co
Contacts/ CoSMO/
-bash-4.2$ cd CoSMO/
-bash-4.2$ touch file.txt
-bash-4.2$ ls
file.txt
```

 

## Linux file structure

TODO: use tree

## Switches

TODO


## Tips

### Reverse Bash search 

One of my favorite bash features is reverse command search.  Often times you'll need to run the same command twice. You can find any commands in your history by pressing `ctrl + R` on Mac/Linux. You can now type the beginning of the command you're looking for and bash will match against your previous commands.  Press `ctrl + R` again to cycle through other options, and enter to issue the command. 

```bash
$ 
(reverse-i-search)`ssh': ssh joshua@login.ccs.neu.edu
```

## Over The Wire

...
...

# Acknowledgments

Thanks to Anuj Modi for inspiration on some of the supporting content!
