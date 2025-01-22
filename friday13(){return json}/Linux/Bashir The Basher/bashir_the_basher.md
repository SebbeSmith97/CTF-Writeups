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
