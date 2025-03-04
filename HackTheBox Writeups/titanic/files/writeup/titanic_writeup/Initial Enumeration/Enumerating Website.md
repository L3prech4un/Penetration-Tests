![[http.titanic.htb..png]]
- Nothing to note other than book your trip button:

![[Book Your Trip.png]]
- Intercepting the packet using burpsuite reveals the following:
	![[Burpsuite.png]]
	- Location: /download?ticket=72ef56cd-0aaf-4947-98c6-69b69a9e4a4d.json
		- Possible Local File Inclusion vulnerability

**Next:** [[Directory Busting]]