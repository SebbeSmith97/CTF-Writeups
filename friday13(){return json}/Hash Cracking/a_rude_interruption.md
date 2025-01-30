# A Rude Interruption

Category: Hash Cracking

## Description
"Here's a beginner challenge for you: crack this hash. The correct password can be found in rockyou.txt, no rules needed. Super easy, right? Oh and the hash type is..."

*gets stabbed from behind*

Hash: 605428f352781542abeafe5c1832d4aa

## Solution

After running hashid and identifying with hashcat I got the following:

```
Analyzing '605428f352781542abeafe5c1832d4aa'
[+] MD2 
[+] MD5 
[+] MD4 
[+] Double MD5 
[+] LM 
[+] RIPEMD-128 
[+] Haval-128 
[+] Tiger-128 
[+] Skein-256(128) 
[+] Skein-512(128) 
[+] Lotus Notes/Domino 5 
[+] Skype 
[+] Snefru-128 
[+] NTLM 
[+] Domain Cached Credentials 
[+] Domain Cached Credentials 2 
[+] DNSSEC(NSEC3) 
[+] RAdmin v2.x 

The following 11 hash-modes match the structure of your input hash:

      # | Name                                                       | Category
  ======+============================================================+======================================
    900 | MD4                                                        | Raw Hash
      0 | MD5                                                        | Raw Hash
     70 | md5(utf16le($pass))                                        | Raw Hash
   2600 | md5(md5($pass))                                            | Raw Hash salted and/or iterated
   3500 | md5(md5(md5($pass)))                                       | Raw Hash salted and/or iterated
   4400 | md5(sha1($pass))                                           | Raw Hash salted and/or iterated
  20900 | md5(sha1($pass).md5($pass).sha1($pass))                    | Raw Hash salted and/or iterated
   4300 | md5(strtoupper(md5($pass)))                                | Raw Hash salted and/or iterated
   1000 | NTLM                                                       | Operating System
   9900 | Radmin2                                                    | Operating System
   8600 | Lotus Notes/Domino 5                                       | Enterprise Application Software (EAS)
```
After trying out all of them, the hash was cracked by using mode 4300 (md5(strtoupper(md5($pass))). This means that the password was first hashed with MD5, then converted to all uppercase and lastly hashed again with MD5. The flag obtained was O24{gr1mreaper}.

```
cb@ctf:~/ctf$ hashcat -m 4300 -a 0 --potfile-disable hash.txt rockyou.txt
hashcat (v6.2.6) starting

OpenCL API (OpenCL 3.0 PoCL 5.0+debian  Linux, None+Asserts, RELOC, SPIR, LLVM 16.0.6, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
==================================================================================================================================================
* Device #1: cpu-skylake-avx512-AMD Ryzen 7 8845HS w/ Radeon 780M Graphics, 12876/25816 MB (4096 MB allocatable), 16MCU

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Optimizers applied:
* Zero-Byte
* Early-Skip
* Not-Iterated
* Single-Hash
* Single-Salt

ATTENTION! Pure (unoptimized) backend kernels selected.
Pure kernels can crack longer passwords, but drastically reduce performance.
If you want to switch to optimized kernels, append -O to your commandline.
See the above message to find out about the exact limits.

Watchdog: Temperature abort trigger set to 90c

Host memory required for this attack: 4 MB

Dictionary cache hit:
* Filename..: rockyou.txt
* Passwords.: 14344384
* Bytes.....: 139921497
* Keyspace..: 14344384

605428f352781542abeafe5c1832d4aa:gr1mreaper               
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 4300 (md5(strtoupper(md5($pass))))
Hash.Target......: 605428f352781542abeafe5c1832d4aa
Time.Started.....: Thu Jan 30 09:58:24 2025 (1 sec)
Time.Estimated...: Thu Jan 30 09:58:25 2025 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:  9006.8 kH/s (0.66ms) @ Accel:1024 Loops:1 Thr:1 Vec:16
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 7815168/14344384 (54.48%)
Rejected.........: 0/7815168 (0.00%)
Restore.Point....: 7798784/14344384 (54.37%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: gracias1960 -> gooooal
Hardware.Mon.#1..: Temp: 60c Util: 24%
```


