Ran ffuf scan to search for :
`ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u http://titanic.htb/ -H "HOST:FUZZ.titanic.htb" -fc 301 -o ffuf_scan`
![[FFuF.png]]
- Scan exposed http://dev.titanic.htb

I still need to gather more information before I can attempt to gain a foothold.

**Next:** [[Enumerating dev.titanic.htb]]