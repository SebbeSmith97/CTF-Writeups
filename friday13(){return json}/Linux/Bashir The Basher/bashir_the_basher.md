# Bashir the Basher

Category: Linux

## Description
Bashir "the Head Basher", a notorious figure in both the criminal underworld and the hacking community. Once an infamous serial killer known for killing by bashing his victim's head in, Bashir's skillset has taken a dark, digital turn. After escaping a lifetime sentence from a maximum-security prison through sheer cunning, he's now applying his talents to the blackhat hacker trade.

Known for his unmatched ability to break out of even the most restrictive shells. Whether it's a highly locked-down server or a poorly configured honeypot, Bashir relentlessly hammering away at any restrictions until he’s free.

He's now looking for a disciple and have setup various training environments scattered all over the internet where he can evaluate methods executed by his prospects. Only those with the sharpest minds and deepest knowledge of shell environments will prevail. Do you have what it takes to become the next Bashir the Basher? Find the flag and prove your at least as good as Bashir himself!

Message from the Author: There is at least three ways to solve this challenge (seven, counting methods prevented by the author). How many can you find?

Password: bAsh-b4sher-nUmba-0ne!

ssh bashir@bashbashing.appsec.nu -p 24222

## Solution

Unfortunately the challengepage and subdomain are down, so I cannot replicated the challenge with screenshots. I will walk through the steps I took to solve the challenge in text.

Connect to the remote SSH enviroment with the following credentials

```
ssh bashir@bashbashing.appsec.nu -p 24222
password: bAsh-b4sher-nUmba-0ne!
```

Once connected we run the following command to check if we're in a restricted Bash shell.

```
1d53a90cb73:~$ echo $0
rbash
```

Running the following commands indicates that the PATH environment variable is set to /tmp/bin, which means only commands located in /tmp/bin are accessible for use.

```
1d53a90cb73:~$ echo $PATH
/tmp/bin
```

Listing the contents of /tmp/bin to see the accessible commands.

```
1d53a90cb73:~$ ls -l /tmp/bin
total 2376
-rwxr-xr-x  1 bashir  bashir  808712 Dec 13 10:42 echo  
-rwxr-xr-x  1 bashir  bashir  808712 Dec 13 10:42 ls
-rwxr-xr-x  1 bashir  bashir  808712 Dec 13 10:42 pwd
```

While listing the contents we can see the restrited-section where the flag probaly is located.

```
1d53aa90cb73:~$ ls -la
total 32
drwxr-sr-x    1 bashir   bashir        4096 Dec 14 17:10 .
drwxr-xr-x    1 root     root          4096 Dec 13 10:42 ..
----------    1 bashir   bashir        6498 Dec 14 17:10 .bash_history
-rw-r--r--    1 root     bashir         893 Dec 13 12:26 .bash_profile
-rw-r--r--    1 bashir   bashir         893 Dec 13 12:26 .bashrc
drwxr-sr-x    1 root     bashir        4096 Dec 13 12:29 restricted-section
```

Let's see what's in there.

```
1d53aa90cb73:~$ ls -l restricted-section/
total 4
-rw-r--r--    1 root     root            49 Dec 13 12:29 flag.txt
```

Now we only need to use the command echo to read the flag.

```
1d53aa90cb73:~$ echo $(<restricted-section/flag.txt)
O24{R3StRIC7iOn_!$_tH3_M0TheR_7O_4lL_Cr3@TiVITY}
```
