---
layout: post
title: Variables (Linux 3.2.2)
key: 20180322
tags: Linux bash
picture_frame: shadow
---

*What are variables? Simply put, a particular string represents something that is not fixed. To give you an example of math that you'll learn in school, y = ax+b, where (y) on the left-hand side is the variable, and (ax+b) on the right-hand side is the variable's expression. Note that the left side is unknown and the right side is known. To put it more simply, we can "substitute a simple word" for another data that is more complex or easily changed." What's the good of that? The biggest benefit is "convenience!" .*

<!--more-->


## Variable access


Let's show you the contents of the variable. You can use the `echo` command to access variables, but variables must be preceded by `$` or `${variable}`. For example,


```
Frank@cavalry:~$ echo $PATH

/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```


Now that we know the correlation between variables and their contents, how do I "configure" or "modify" the contents of a variable? It's easy! Just use "equals (=)" to connect a variable to its content. For example: I want to configure the contents of the variable name `myName` as "Frank", then:


```
[root@www ~] # echo $myname
<== there is no data here ~ because this variable has not been configured! Is empty!
[root@www ~] # myname = Frank
[root@www ~] # echo $myname
Frank <== appears! Because this variable is already configured!
```


## Variable assign rules


The following examples show you how to assign a variable


### Example 1: Configure a variable name with the content


```
[root@www ~] # 12name=Frank
- bash: 12name=VBird: Command not found <== screen displays error! Because you can't start with a number!
[root@www ~]# name= Frank <== error again! Because there is a space!
[root@www ~]# name=Frank <==OK!
```


### Example 2: The variable contains a special symbol.

```
[root@www ~]# name=Frank's name

# single and double quotes must be paired, there is only one single quote in the above configuration, so when you press Enter, you can continue to enter variable content. This is not what we need!
# Remember, to recover after failure, press [CTRL] -C to end!

[root@www ~]# name="Frank's name" <==OK!

# The command looks from left to right → quotes first are useful, so as shown above, single quotes will be invalid!

[root@www ~]# name='Frank's name' <== failed!

# Since the first two single quotes are already paired, there will be an unpaired single quote after them! And so it failed!

[root@www ~]# name=Frank\'\ name <==OK!

# Using backslash (\) to skip special characters, such as single quotes and space keys, is also OK!

```


### Example 3: I'm going to append `:/home/dmtsai/bin` to the `PATH` variable 

```
[root@www ~]# PATH=$PATH:/home/dmtsai/bin
[root@www ~]# PATH="$PATH":/home/dmtsai/bin
[root@www ~]# PATH=${PATH}:/home/dmtsai/bin

All three of the above formats are OK in the PATH configuration! But the following example is not necessarily true!
```

### Example 4: By example 3, do I want to add "yes" to the content of variable `name`?

```
[root@www ~]# name=$nameyes
This expression tell system assign variable `nameyes` to vairable `name` though we have not configured the variable call "nameyes" yet! So, it should be done like this:

[root@www ~]# name="$name"yes
[root@www ~]# name=${name}yes <== I prefer this way!
```


### Example 5: How do I make the name=VBird that I just configured work with the other shell?

```
[root@www ~]# name=Frank
[root@www ~]# bash <== into a so-called subroutine
[root@www ~]# echo $name <== subroutine: echo once again;
    <== There is no content here.
[root@www ~]# exit <== Leave this subroutine

[root@www ~]# export name
[root@www ~]# bash <== into a so-called subroutine
[root@www ~]# echo $name <== subroutine: run here!
Frank <== Look! value appears!
[root@www ~]# exit <== Leave this subroutine

Command `export` will make a variable become Environment Variable, you can check with command `env` and there is the variable "name".
```


### Example 6: How do I get to your current core module directory?

```
[root-@www ~]# cd /lib/modules/`uname-r`/kernel
[root-@www ~]# cd /lib/modules/$(uname-r)/kernel
```


### Example 7: Single quote and double quote

```
[root@www ~]# myname="$name is me"
[root@www ~]# echo $myname
Frank is me
[root@www ~]# myname='$name is me'
[root@www ~]# echo $myname
$name is me

Double quotes "" can still hold the contents of a variable
single quotes '' can only contain generic characters, not special symbols. 
Text between backticks `` is executed and replaced by the output of the command. That is called command substitution because it is substituted with the output of the command.

```


## Environment variables


Use `env` or `export` to check out current env variables, something like this:

```
root@www:# env
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:
LESSCLOSE=/usr/bin/lesspipe %s %s
LANG=C.UTF-8
SUDO_GID=1003
USERNAME=root
SUDO_COMMAND=/bin/bash
USER=root
PWD=/lib/modules
HOME=/root
SUDO_USER=gcpvm
XDG_DATA_DIRS=/usr/local/share:/usr/share:/var/lib/snapd/desktop
name=Frank
SUDO_UID=1002
MAIL=/var/mail/root
SHELL=/bin/bash
TERM=xterm
SHLVL=1
LOGNAME=root
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin
LESSOPEN=| /usr/bin/lesspipe %s
_=/usr/bin/env
OLDPWD=


```

- HOME

Represents the user's home directory. Remember when we could use CD ~ to go to our home directory? Or use the CD to go directly to the user's home directory. That is access to this variable, there are many programs can access the value of this variable!


- SHELL

Tell us, which SHELL is currently used in this environment? Linux USES /bin/bash by default!


- HISTSIZE

This is related to the "historical command", that is, the commands we have made can be recorded by the system, and the number of strokes recorded is configured by this value.


- MAIL

When we use mail to receive a letter, the system will read the mailbox file (mailbox).


- PATH

The directory is separated from the directory by a colon (:). Since the file is searched sequentially by the directory in the PATH variable, the order of the directory is also important.


- LANG

This is important! For example, when we start some perl programming language files, he will actively analyze the language data files. If he finds some coding language files that he cannot parse, it may cause errors. In general, our Chinese encoding is usually zh_tw.big5 or zh_tw.UTF-8, which cannot be easily interpreted, so sometimes the language data may need to be revised. This part will be introduced in the next section!


- RANDOM

This thing is a random number variable. Now most distributions have a random number generator and that is /dev/random file. We can get the RANDOM value through the variable related to the RANDOM number file ($RANDOM). In BASH, the contents of this RANDOM variable are between 0 and 32767, so whenever you echo $RANDOM, the system will actively pull out a value between 0 and 32767. What if I want to use values between 0 and 9? To declare the numeric type, declare the numeric type using the declare method, then do so:

```
[root@www ~]# declare -i number=$RANDOM*10/32768 ; echo $number
```


Observe all variables with `set` (including environment variables and custom variables)


Bash is not just about environment variables. There are also variables related to the bash interface and user-defined variables that exist. So how do we look at these variables? At this point, use the set command. In addition to the environment variables, set displays all the other variables within Bash. There is a lot of information, but the following is just a few important ones:


Root @ WWW ~ # set

BASH=/bin/ BASH <== BASH's main program placement path

BASH_VERSINFO = ([0] = "3" [1] = "2" [2] = "25" [3] = "1" [4] = "release"

[5]=" i686-redhat-Linux-gnu ") <== bash version ah!

BASH_VERSION='3.2.25(1) -Release '<== bash version too!

COLORS= /etc/dir_color.xterm <== the color record file used

COLUMNS=115 <== In the current terminal environment, the fields used have several character lengths

HISTFILE=/root/.bash_history <== Hide file for history command records

HISTFILESIZE=1000 <== Maximum number of recorded items in a file stored (related to the previous variable).

(HISTSIZE=1000 <==) The largest amount of historical commands recorded in the current environment.

HOSTTYPE=i686 <== main type of software installed on the host. We used i686 compatible machine software

IFS=$' \t\n' <== default delimiter

LINES=35 <== The maximum number of LINES under the current terminal

MACHTYPE= i686-Redhat-Linux-gnu <== Machine type installed

MAILCHECK=60 <== is related to mail. Scan your mailbox every 60 seconds for new messages!

OLDPWD=/home <== Last working directory. We can use CD - to access this variable.

OSTYPE= Linux-GNU <== type of operating system!

PPID=20025 <== PID of the parent program (this will be covered in a later section)

PS1='[\u@\h \W]\$' <== PS1. This is the command prompt character, which is what we often see

[root@www ~]# or [dMTSai ~]$configuration value! It can be changed!

PS2='> '<== if you use the hop symbol (\) after the second line of the prompt character also

Name =VBird <== Custom variable just configured can also be listed!

$<== the PID that the shell is currently using

? <== the return value of the command just finished running.


In general, variables related to the interface of our current shell, whether they are environment variables or not, are usually configured with uppercase characters. That is to say, "Basically, by default on Linux, variables configured with {uppercase} are generally required variables within the system." OK! OK! So which of those variables are more important? There are probably a few of them!


PS1 :(configuration of prompt characters)


This is PS1, this is our command prompt character. Every time we press the [Enter] key to run a command, and the prompt character appears again, we will actively read the variable value. What is shown on the top PS1 is some special symbols and these special symbols can show different information. The default PS1 variable content of each bash may be slightly different, never mind, "get used to your own habits" is good. You can use Man bash to look up the instructions for PS1 to understand some of the symbolic meanings below.


\d: Date format with "Week/Month/Day" displayed, such as: "Mon Feb 2"

\H: Full host name. For example, Bird's exercise machine is www.vbird.tsai

\h: Only take the name of the host before the first decimal point, if the bird's host is omitted after "WWW"

\t: Display time, "HH:MM:SS" in 24-hour format

\T: Display time, "HH:MM:SS" in 12-hour format

\A: Display time, "HH:MM" in 24-hour format

\@ : Display time, "AM/PM" style in 12-hour format

\u: The current user's account name, such as "root";

\v: BASH version information, such as Bird's test motherboard is 3.2.25(1), only take "3.2" to display

\w: Full working directory name, directory name written from the root directory. But the home directory will be replaced by ~;

\W: Gets the working directory name using the basename function, so only the last directory name is listed.

\# : Which order was given.

\$: Prompt character, # if root, $~ if not


Ok, let's take a look at CentOS's default PS1 content: "[\u@\h \W]\$". Now you know what those backslashes mean? Be careful! The data after the backslash is a special function of PS1, regardless of bash's variable configuration! Don't get mixed up! Now do you know why your command prompt is: "[root-@www ~]#"? Okay, so let's say I want to have a prompt like this:


[root @ WWW/home/dmtsai thus # 12] were #


The # stands for the order given at the 12th time. So how should you configure PS1? Here's how it works:


[root@www ~]# CD /home

[root-@www home]# PS1='[\u@\h \w \A #\#]\$'

Root @ WWW/home 17:02 # 85 #

Do you see #? The prompt character has changed! Become very interesting! Of these, the number 85 is interesting,

If you type ls a few more times, the number will be added. Why? It has instructions on it!



$:(about the PID of this shell)


Money size itself is also a variable oh! This click represents the "thread code of the current Shell", which is also called PID (Process ID). More procedural ideas, which we'll come back to in canto IV. To find out the PID of our shell, just use: "Echo $$"! The number that appears is your PID number.


? (About the return value of the last run command)


What? Question marks are also a special variable, right? That's right! This variable is very important in bash! This variable is "value returned by last run command". This variable is "value returned by last run command". When we run certain commands, these commands return a run code. In general, if the command is successfully run, a value of 0 will be returned. If there is an error, an "error code" will be returned. It is usually replaced by a number that is not zero. Let's look at the following example:


/ root @ WWW ~ # echo $SHELL

/bin/bash <== display smoothly! No mistakes!

/ root @ WWW ~ # echo $?

0 <== because it's ok, so the return value is 0

Name = [root @ WWW ~] # 12 VBird

- Bash: 12name=VBird: Command not found <== error! Bash is reporting problems

/ root @ WWW ~ # echo $?

127 <== return error code (not 0) because there is a problem

Error code return values vary according to the software, we can use this code to search for the cause of the error oh!

/ root @ WWW ~ # echo $?

0

# yi! How did it get right again? That's because "?" Related only to "last run command",

So, our last command was to run "echo $?" and of course there was no error, so it was 0!



OSTYPE, HOSTTYPE, MACHTYPE :(level of host hardware and core)


We talked about Cpus in chapter 0, the CPU level description in the introduction to calculators. At present, THE CPU of personal computers is mainly divided into 32/64 bits, among which 32 bits can be divided into I386, I586, i686, and 64 bits are called x86_64. Because different levels of CPU command sets are different, your software may be optimized for certain Cpus to achieve better software performance. So there are i386, I686 and X86_64. In terms of current (2009) mainstream hardware, x86_64 dominates almost all of it! But after all, there are still a lot of old machines, in the bird's environment, I use a P-III computer, so they found that My level is I686!


Keep in mind that higher-order hardware is often downwardly compatible with older software, but higher-order software may not be installed on older machines! As we explained in chapter 3, again, you can install The Linux operating system i386 on x86_64 hardware, but you can't install x86_64 on i686 hardware! Keep that in mind!