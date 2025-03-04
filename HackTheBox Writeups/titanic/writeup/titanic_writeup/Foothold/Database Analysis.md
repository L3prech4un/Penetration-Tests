Breaking this down into smaller steps will help:
- I run the command: `SELECT * FROM user;` ![[Table dump.png]]
	- There is a lot to look at here, so instead I will run a more specific command using the column names I found before to better understand what information is what:
		- `SELECT name, email, passwd, salt, passwd hash_algo;`![[table login credentials.png]]
			- We can see that there are 2 users:
			  1. **administrator:**
				  1. email: root@titanic.htb
				  2. passwd: cba20ccf927d3ad0567b68161732d3fbca098ce886bbc923b4062a3960d459c08d2dfc063b2406ac9207c980c47c5d017136
				  3. salt: 2d149e5fbd1b20cf31db3e3c6a28fc9b
				  4. passwd_hash_algo: pbkdf2
			  2. **developer:**
				  1. email: developer@titanic.htb
				  2. passwd: e531d398946137baea70ed6a680a54385ecff131309c0bd8f225f284406b7cbc8efc5dbef30bf1682619263444ea594cfb56
				  3. salt: 8bf3e3452b78544f8bee9400d6936d34
				  4. passwd_hash_algo: pbkdf2
 We have now successfully acquired login credentials. The next step logically is to decrypt the password with the hash and algorithm.

**Next:** [[Password Cracking]] 