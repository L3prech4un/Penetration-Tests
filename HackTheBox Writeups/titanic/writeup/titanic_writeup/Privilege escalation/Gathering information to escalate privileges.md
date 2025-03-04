After trying to run root commands I quickly determine that I lack the privileges necessary to access the root folder. This means I will have to do a little digging to find some weaknesses in the system.

Digging around a bit I decide to check for scripts owned by the root:![[scripts owned by root.png]]
- The first file `/opt/scripts/identify_images.sh` looked a little out of place, so I decide to start there.
- Attempting to run **identify_images.sh** with `./identify_images.sh` returns the following error:![[metadata.log.png]]
	- **identify_images.sh** is owned by a privileged user. Wanting to know more I concatenated the file to see its source code:![[cat identify_images.png]]
		- **identify_images.sh** seems to be a script that runs `/usr/bin/magick` to execute the unknown command `identify` then sends the output to **metadata.log**
		- This means `/usr/bin/magick` has permissions to execute console commands.
	- Navigating to `/usr/bin/` we do indeed find a program called **magick** ![[Magick.png]]
		- Investigating the program further we discover **magick** is short for a program called **ImageMagick**
		- Navigating to the **ImageMagic** website reveals that it is a program used to edit images![[image magick.png]]
			- The version of **ImageMagick** on this computer is vulnerable to several exploits and is documented under several CVEs

**Next:** [[Exploiting ImageMagick]]