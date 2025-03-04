Visited http://dev.titanic.htb: ![[http.dev.titanic.htb.png]]

Clicking **Explore** leads us to the following page: ![[Repository.png]]
- Discovered a list of the developers **repositories**:
	1. **docker-config** - Which contains information related to Docker Compose![[Docker Compose.png]]
		- Several bits of information can be gathered from this:
			- Target is running ==SQL== (Possibly Exploitable)
			- Reading the README.md file gives is insight into Docker Compose, a program used for running multi-container Docker applications. Additionally, ==Docker Compose has Read/Write Permissions== over certain files, as they would be required to "Manage a Gitea instance" as the document states.
		- Further Enumeration of the folders **/gitea** and **/mysql** reveals they both contain configuration files:
			1. **gitea/docker-compose.yml**:![[docker-config.png]]
				- Reveals **/home/developer/gitea/data**
			2. **mysql/docker-compose.yml**:![[mysql-docker-compose.png]]
				- If it wasn't evident by the folder name, our target is running mySQL and this file contains the following login credentials:
				  `MYSQL_ROOT_PASSWORD: 'MySQLP@$$w0rd!'`
				  `MYSQL_DATABASE: tickets`
				  `MYSQL_USER: sql_svc`
				  `MYSQL_PASSWORD: sql_password`
		- Now that we have established that the Gitea repository service is running on docker I decide to further research the program. Clicking on the **Help** button leads us to the official documentation for the service. ![[Installation-documentation.png]]
			- Briefly scanning through it I noticed instructions for installation with the docker service. Reading this section reveals the default location of the configuration file **app.ini**
				  `/data/gitea/conf/app.ini`
			- Combining this with the path we discovered before **home/developer/gitea/data** exposes the full path to the configuration file:
				  `/home/developer/gitea/data/gitea/conf/app.ini`
			- Unable to find any more useful information on this site I return to the developers Gitea page to explore the other repository for more information
	2. **flask-app** - Contains information and code related to the ticket "booking system" and download button we discovered on http://titanic.htb.
		- Briefly reading the README.md reveals the programs function:![[flask-app.png]]
			1. The user fills out a form to book a trip with their details
			2. The program generates a ticket and saves it as a .json file
			3. Then it sends the generated file to the user via a download
		- This piqued my interest, as early I had thought that path traversal or LFI could be a potential gateway to gain a foothold. 
		- Further analysis of the programs code **app.py** reveals the following: ![[app.py.png]]
			- **app.py** is the source code for the ticket generator discovered on the site
			- Analyzing the code reveals that LFI/Path Traversal appears to indeed be a vulnerability on this website. This was determined by the fact that the code doesn't sanitize the download path. In other words, the ==code doesn't check to verify that the file being downloaded is actually the ticket==. ==Rather, it just checks if the path of the file that is requested for download exists on the hosts machine.== This means that **as long as we have a valid path to a file, we can download it from the host.** 
- Now that we have discovered an exploitable vulnerability, it is time we move on to gaining an initial foothold:

**Next:** [[Local File Inclusion Exploitation]] 