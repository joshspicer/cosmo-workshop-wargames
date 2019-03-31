# Linux CLI / Bandit Workshop

Linux is an operating system that sits the at core of much of the technology we interact with daily. Linux is free, secure, and having to work with it on the job is unavoidable.

We'll start the workshop by reviewing some common and good-to-know linux commands.  We'll then move into Bandit ["War Games"](http://overthewire.org/wargames/bandit/), an interactive shell-based game that reinforces basic commands and teaches security concepts.

## Why Learn Linux?

Linux knowledge is invaluable in the CS field. Odds are servers you'll interact with on the job will be running some distro of Linux. In addition, small or embedded systems often run some flavor of Linux.  Ever used a raspberry pi? Those devices are generally running Raspbian, a Linux distribution.  Linux provides a stable development environment, and of course is free and open for users to get started with!

## Setup 

Before we start, lets get our environment set up.

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

### Directory Traversal

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
* `cat <FILE>` - Print the contents of the file to standard out.
* `echo <TEXT>` - "Echos" a given string to standard out (the screen)

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
Contacts/ CoSMO/

-bash-4.2$ cd CoSMO/

-bash-4.2$ touch file.txt

-bash-4.2$ ls
file.txt
```

### Bash Operators

Bash is a special kind of programming language that we  interact with in terminal.  Just like Java or Python have operators like `+` and `*`, we see those operators in Bash too (along with some other helpful ones!).

* `>` Used to redirect standard output to a file. Overwrites existing file is it exists!
* `>>` Also used to redirect, but appends to a current file.
* `<` Accept input from a file
* `|` A "Pipe". Sends the output of the first command as the input of the next command


```bash
-bash-4.2$ echo "Hello, CoSMO" > greeting.txt

-bash-4.2$ cat greeting.txt
Hello, CoSMO

-bash-4.2$ echo "How are you?" >> greeting.txt

-bash-4.2$ cat greeting.txt
Hello, CoSMO
How are you?

-bash-4.2$ cat greeting.txt | grep "CoSMO"
Hello, CoSMO
```

## Useful Linux Programs

Let's break down that last command we issued with `grep`.  Grep is a built in unix program that seraches files for a specified pattern of words. In the above command we passed our file `greeting.txt` as the input to grep, and searched for a line with the pattern "CoSMO". Grep scanned the file line by line and, see you can see, found one line matched and and printed it. 

### Manual Pages

You might be asking at this point, how am I supposed to remember all these commands? Good news - you don't.  Most linux programs will come with a "manual" file that explains exactly how to use them. Let's see what grep's manual page looks like by running the `man` command. 

Type `man grep`

```
GREP(1)                                          General Commands Manual                                         GREP(1)

NAME
       grep, egrep, fgrep - print lines matching a pattern

SYNOPSIS
       grep [OPTIONS] PATTERN [FILE...]
       grep [OPTIONS] [-e PATTERN | -f FILE] [FILE...]

DESCRIPTION
       grep  searches the named input FILEs (or standard input if no files are named, or if a single hyphen-minus (-) is
       given as file name) for lines containing a match to the given PATTERN.  By  default,  grep  prints  the  matching
       lines.

       In  addition,  two  variant  programs egrep and fgrep are available.  egrep is the same as grep -E.  fgrep is the
       same as grep -F.  Direct invocation as either egrep or fgrep is deprecated, but is provided to  allow  historical
       applications that rely on them to run unmodified.

OPTIONS
   Generic Program Information
       --help Print  a  usage message briefly summarizing these command-line options and the bug-reporting address, then
              exit.

       -V, --version

    ...
    ...
    ...
```

The file is divided into explanation what the program is used for, the correct syntax, as well as a variety of options that can be run.

### Options

Linux programs often can do more than one thing, and grep is no exception.  If you look on grep's man page you see a lot of options to modify the behavior of the program.  

```
    ...
    ...
   Matching Control
       -e PATTERN, --regexp=PATTERN
              Use PATTERN as the pattern.  This can be used to specify multiple search patterns, or to protect a pattern
              beginning with a hyphen (-).  (-e is specified by POSIX.)

       -f FILE, --file=FILE
              Obtain patterns from FILE, one per line.  The empty file contains zero  patterns,  and  therefore  matches
              nothing.  (-f is specified by POSIX.)

       -i, --ignore-case
              Ignore case distinctions in both the PATTERN and the input files.  (-i is specified by POSIX.)

       -v, --invert-match
              Invert the sense of matching, to select non-matching lines.  (-v is specified by POSIX.)

    ...
    ...
```

As you can see, specifying the flag `-i` tells grep to ignore case.


```bash
-bash-4.2$ cat greeting.txt | grep -i "cosmo"
Hello, CoSMO

-bash-4.2$ cat greeting.txt | grep  "cosmo"

```



## Tips

### Reverse Bash search 

One of my favorite bash features is reverse command search.  Often times you'll need to run the same command twice. You can find any commands in your history by pressing `ctrl + R` on Mac/Linux. You can now type the beginning of the command you're looking for and bash will match against your previous commands.  Press `ctrl + R` again to cycle through other options, and enter to issue the command. 

```bash
$ 
(reverse-i-search)`ssh': ssh joshua@login.ccs.neu.edu
```


## Over The Wire

Congrats - you just learned all you need to know to hop into [Bandit](http://overthewire.org/wargames/bandit)!Bandit and the rest of the over the wire "war games" are security labs intended to teach you the security fundamentals.  Bandit especially is a great introduction to practical Linux usage! 

Head over the [Level0](http://overthewire.org/wargames/bandit/bandit0.html) and SSH into the first challenge. (You'll _first_ need to disconnect from the Khoury college server!).  

```bash
josh$ ssh -p 2220 bandit0@bandit.labs.overthewire.org

The authenticity of host '[bandit.labs.overthewire.org]:2220 ([176.9.9.172]:2220)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496E...hczc.

Are you sure you want to continue connecting (yes/no)? yes

Welcome to OverTheWire!
...
...
```

Note that we had to specify a port with ssh's `-p` flag. 

Let's apply what we just learned to find next level's password!

```bash
bandit0@bandit:~$ pwd
/home/bandit0
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
bandit0@bandit:~$
```

Hey look, we found something in a file called `readme` that looks like a password. If we use this password on [the next level](http://overthewire.org/wargames/bandit/bandit1.html) we see that it works! Note that we changed the username from `bandit0` to `bandit1`.

```bash
bandit0@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.
tracy:bandit-workshop josh$ ssh -p 2220 bandit1@bandit.labs.overthewire.org

Password: boJ9jbbUNNfktd78OOpsqOltutMc3MY1

Welcome to Overthewire!
...
...
```










# Acknowledgments

Thanks to Anuj Modi for inspiration on some of the supporting content!
