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
cb@ideapad:~/Documents/CTF$ hashid hash.txt 
--File 'hash.txt'--
Analyzing '$2y$05$tJ5qkcBGrjiRfZZAlkSsP.kcVStH7oCzsery3nN1sgXk02xThNck6'
[+] Blowfish(OpenBSD) 
[+] Woltlab Burning Board 4.x 
[+] bcrypt 
```
