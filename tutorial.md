# Linux CLI / Bandit Workshop

Linux is an operating system that sits the at core of much of the technology we interact with daily. Linux is free, secure, and having to work with it on the job is unavoidable.

We'll start the workshop by reviewing some common and good-to-know linux commands.  We'll then move into Bandit ["War Games"](http://overthewire.org/wargames/bandit/), an interactive shell-based game that reinforces basic commands and teaches security concepts.

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


## Tips

### Reverse Bash search 

One of my favorite bash features is reverse command search.  Often times you'll need to run the same command twice. You can find any commands in your history by pressing `ctrl + R` on Mac/Linux. You can now type the beginning of the command you're looking for and bash will match against your previous commands.  Press `ctrl + R` again to cycle through other options, and enter to issue the command. 

```bash
$ 
(reverse-i-search)`ssh': ssh joshua@login.ccs.neu.edu
```
