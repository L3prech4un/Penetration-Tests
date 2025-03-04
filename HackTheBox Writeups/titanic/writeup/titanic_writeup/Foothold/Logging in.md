Ran the following command:
![[ssh.png]]
- `ssh`- ssh command
- `developer` - username
- `titanic.htb` - host
I am subsequently asked to enter `developer@titanic`'s password, to which I input our cracked password: `25282528`
![[Successful Login.png]]
- Voila! I'm successfully logged in as developer@titanic.htb via SSH, a very stable shell, so no need to upgrade to a stable-shell

Running `ls` immediately shows us the following:
1. `gitea`- a folder we know all too well
2. `mysql`- what appears to be a folder containing files pertinent to the SQL database
3. `user.txt`- a file containing our **user flag**

With all this we conclude our foothold as we have now successfully gained a foothold on our target.

**Next Step:** [[Gathering information to escalate privileges]]