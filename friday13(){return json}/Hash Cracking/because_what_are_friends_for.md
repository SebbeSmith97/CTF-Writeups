# Because What Are Friends For

Category: Hash Cracking

## Description

The person in your walls has come before you seeking help. They have forgotten their password! Due to their high status on a particular website, they were able to convince the database admin to find the hashed password of their account (using the argument which essentially boils down to "I am needed to keep the spirit of the website alive"). They have the hash, and luckily some information about the likely password. After being instructed to try to remember the structure of the password, they came up with the following:

It definitely starts with a capital letter, followed by some lowercase letters. It ends with a 2 digit number which I THINK is 12 but not 100% sure. The number at the end is definitely smaller than 20 though. Inbetween this number and the final lowecase letters are 1-2 special characters. I think it was just an underscore but I don't remember. I'm also pretty sure the length of the password is 10, I usually aim for that length with all my passwords. I really need this password recovered, how else am I gonna access my high rep Stack Overflow account and comment snarky remarks to other users who made a slight error in a long and otherwise very helpful answer?

Oh and btw, I don't know if this helps, but here is what the DB admin said: "Excuse the outdated hashing we have here. 1990 was a good year for motorcycles, not so much for hashing algorithms." I figured that could give you a clue as to what the hashing algorithm is.

All this person wants is to continue contributing to the SO ecosystem. Help the world regain its balance - help your friend in the walls recover their password.
Hash: bfe85af6a5012498d325db63aac5dd4a

## Solution

After reading the challenge we got some clues regarding the password:

- Starts with a capital letter.
- Followed by lowercase letters.
- Ends with a 2-digit number (less than 20, possibly 12).
- 1-2 special characters (likely _).
- Total length is 10 characters.

The hint about 1990 suggests an outdated hashing algorithm, likely MD4, which was used during that era. MD4 was developed by Ronald Rivest in 1990 and later replaced by MD5 in 1991. Running hashid and hashcat auto detect also confirms it's most likely one of them.

Hashcat has a built-in function for [mask attacks](https://hashcat.net/wiki/doku.php?id=mask_attack) where we can perform a more specified brute-force attack on the password.
