Odds are that the developer has an easier to crack password so we will start with him.
1. After briefly searching online I found a python script that automatically converts gitea password hashes into hashcat-crackable formats:
	- `sqlite3 gitea.db 'SELECT salt,passwd FROM user;' | python3 gitea2hashcat.py`![[Format hash.txt.png]]
		- Then proceeded to output it to hash.txt (as seen above)
2. Next step is to run hashcat with the following command:
	  `hashcat -a 0 -m 10900 hash.txt /usr/share/wordlists/rockyou.txt`
	- After waiting about 15 seconds hashcat had finished cracking the hash:![[hash-cracked.png]]
3. Hashcat cracked our hash giving us the developer password: `25282528`


Now that we have gained valuable login information we need to think about how to use it. When scanned our target ip address with nmap earlier we discovered that port 22 was open, meaning that the host has **OpenSSH** running.

**Next step:** [[Logging in]]