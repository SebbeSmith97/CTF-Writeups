# Everybody's Favourite

Category: Linux

## Description
There's no rule that says you can't make silly challenges, right? I asked the person who lives in my walls, the monster which chases me up the stairs when the lights are turned off, and the entity which appears when I lay in bed without moving for too long. They all said it's OK!

Author's note: This is not one of my proudest challenges. You have been warned.

ssh user1@138.68.105.97 -p 2222

PW is: d31f00a7feb2b69e20dff9f47a6f3c1c
## Solution

Unfortunately the challengepage and subdomain are down, so I cannot replicated the challenge with screenshots. I will walk through the steps I took to solve the challenge in text.

Connect to the remote SSH enviroment with the following credentials

```
ssh user1@138.68.105.97 -p 2222
password: d31f00a7feb2b69e20dff9f47a6f3c1c
```

Once connected we are greeted by the MOTD which contains the flag O24{C4nt_all_be_w1nners}.

```
cb@ctf:~$ ssh user1@138.68.105.97 -p 2222
user1@138.68.105.97's password: 
Last login: Mon Dec 16 10:34:14 2024 from 194.47.12.115
Welcome to Ubuntu 22.04.4 LTS (GNU/Linux 5.15.0-113-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Thu Oct 17 12:53:49 UTC 2024

  System load:  0.09               Processes:             135
  Usage of /:   43.0% of 24.05GB   Users logged in:       1
  Memory usage: 58%                IPv4 address for eth0: 207.154.111.15
  Swap usage:   0%                 IPv4 address for eth0: 10.19.0.10

Expanded Security Maintenance for Applications is not enabled.

46 updates can be applied immediately.
9 of these updates are standard security updates.
What you are looking for is probably: C4nt_all_be_w1nners
To see these additional updates run: apt list --upgradable

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


*** System restart required ***
Last login: Thu Oct 17 10:30:28 2024 from 87.191.60.244
user1@917ee237bfd5:~$ 
```
