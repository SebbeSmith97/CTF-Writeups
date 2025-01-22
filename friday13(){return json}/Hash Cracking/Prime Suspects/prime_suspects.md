# Prime Suspects
Author: Mikael Svall

Category: Hash Cracking

## Description
Json's notorious ransomware gang has unveiled what they claim to be an uncrackable hashing algorithm, derived from the digits of the largest known [prime number](M136279841.zip). Mocking the world, they have publicly shared the hash of their master password, confident no one can break the encryption.

Crypto analysts believe the password is composed of digits only, sourced from this massive prime. For maximum security, the gang ensured the password is at least 10 digits long, hidden deep within the prime’s vast expanse.
If you manage to crack the hash, you also found the flag, wrap it in the format O24{cracked_hash_here}
The answer lies in the prime.

Hash: $2y$05$tJ5qkcBGrjiRfZZAlkSsP.kcVStH7oCzsery3nN1sgXk02xThNck6

## Solution

We got the following information about the password:
- Only consist of numbers [0-9]
- At least 10 characters long
- Can be found in the largest known Mersenne prime number [M136279841](M136279841.zip)


After some research online and with [hashid](https://pypi.org/project/hashID/) I discovered that the [hash](hash.txt) is a **bcrypt**-hash with the **cost** of **05** and **salt tJ5qkcBGrjiRfZZAlkSsP.**


```bash
cb@ctf:~/ctf$ hashid hash.txt 
--File 'hash.txt'--
Analyzing '$2y$05$tJ5qkcBGrjiRfZZAlkSsP.kcVStH7oCzsery3nN1sgXk02xThNck6'
[+] Blowfish(OpenBSD) 
[+] Woltlab Burning Board 4.x 
[+] bcrypt 
```

I need to extract all of the substrings from the prime number as potential password candidates. I started out by assuming the password's length consists of 10 characters, planning on expanding it further. I saved the prime number as m136279841.txt and divided it up in a new textfile candidates.txt by using awk.

```
awk '{ 
    prime=$0; 
    for (i=1; i<=length(prime)-9; i++) { 
        print substr(prime,i,10) 
    } 
}' m136279841.txt > candidates.txt
```

Running the mode 3200 for Bcrypt with wordlist on the hash (with disabled potfile to re-run) got me the following sequence of numbers and flag O24{9999903898}.

```
cb@ctf:~/ctf$ hashcat -m 3200 -a 0 --potfile-disable hash.txt candidates.txt

$2y$05$tJ5qkcBGrjiRfZZAlkSsP.kcVStH7oCzsery3nN1sgXk02xThNck6:9999903898

Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 3200 (bcrypt $2*$, Blowfish (Unix))
Hash.Target......: $2y$05$tJ5qkcBGrjiRfZZAlkSsP.kcVStH7oCzsery3nN1sgXk...ThNck6
Time.Started.....: Wed Jan 22 15:46:23 2025 (18 mins, 17 secs)
Time.Estimated...: Wed Jan 22 16:04:40 2025 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (candidates.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:    10117 H/s (3.05ms) @ Accel:16 Loops:4 Thr:1 Vec:1
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 11070464/37742368 (29.33%)
Rejected.........: 0/11070464 (0.00%)
Restore.Point....: 11070208/37742368 (29.33%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:28-32
Candidate.Engine.: Device Generator
Candidates.#1....: 8988830636 -> 8867018436
Hardware.Mon.#1..: Temp: 68c Util:  0%

Started: Wed Jan 22 15:46:16 2025
Stopped: Wed Jan 22 16:04:42 2025
