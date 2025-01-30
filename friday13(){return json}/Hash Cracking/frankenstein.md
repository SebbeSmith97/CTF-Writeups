# Frankenstein

Category: Hash Cracking

## Description

Good ole [rockyou.txt](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt) and MD5, the perfect beginner cracking challenge.

But wait, something isn't right... there's blood coming out of the hash. It looks like someone has... oh god, what is this abomination?!

Hash: 3d31ef4df92e0f21db3f3946ba271882

## Solution

As the challenge suggests the hash is "cut" in some sort of way - leaking blood and looking like an abomination. If we reference to the name of the challenge, Frankenstein, we might suspect that the hash is truncated and stitched together. 

When trying to identify the hash, it looks like a MD5 containing 32 hexadecimal characters. Since we suspect it might contain two truncated hashes, we try to split it up into two hashes containing 16 characters each.

**First half:** 3d31ef4df92e0f21
**Second half:** db3f3946ba271882

```
cb@ctf:~/ctf$ echo "3d31ef4df92e0f21" > first_half.txt
cb@ctf:~/ctf$ echo "db3f3946ba271882" > second_half.txt
```

Hashcat supplies a mode 5100 to crack half/truncated MD5 hashes. Let's run the first half!

```
cb@ctf:~/ctf$hashcat -m 5100 first_half.txt rockyou.txt --potfile-disable
hashcat (v6.2.6) starting

...

Dictionary cache hit:
* Filename..: rockyou.txt
* Passwords.: 14344384
* Bytes.....: 139921497
* Keyspace..: 14344384

3d31ef4df92e0f21:stitch@                                  
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 5100 (Half MD5)
Hash.Target......: 3d31ef4df92e0f21
Time.Started.....: Thu Jan 30 11:31:55 2025 (0 secs)
Time.Estimated...: Thu Jan 30 11:31:55 2025 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........: 17197.1 kH/s (0.17ms) @ Accel:1024 Loops:1 Thr:1 Vec:16
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 3538944/14344384 (24.67%)
Rejected.........: 0/3538944 (0.00%)
Restore.Point....: 3522560/14344384 (24.56%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: stlome2 -> stefy06
Hardware.Mon.#1..: Temp: 55c Util: 18%

```
... and the second half!

```
cb@ctf:~/ctf$hashcat hashcat -m 5100 second_half.txt rockyou.txt --potfile-disable
hashcat (v6.2.6) starting

...

Dictionary cache hit:
* Filename..: rockyou.txt
* Passwords.: 14344384
* Bytes.....: 139921497
* Keyspace..: 14344384

db3f3946ba271882:together                                 
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 5100 (Half MD5)
Hash.Target......: db3f3946ba271882
Time.Started.....: Thu Jan 30 11:32:05 2025 (0 secs)
Time.Estimated...: Thu Jan 30 11:32:05 2025 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:  8941.9 kH/s (0.50ms) @ Accel:1024 Loops:1 Thr:1 Vec:16
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 16384/14344384 (0.11%)
Rejected.........: 0/16384 (0.00%)
Restore.Point....: 0/14344384 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: 123456 -> christal
Hardware.Mon.#1..: Temp: 53c Util: 10%

```
This gives us the following to words from rockyou.txt to combine into our obtained flag O24{stick@together}.
