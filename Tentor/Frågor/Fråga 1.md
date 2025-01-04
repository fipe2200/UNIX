
# 2024-01-08
![[Pasted image 20250104115140.png]]

What it is:
- **A container is an instance of an image,** 
	  The Docker image is a collection of files that constitute a tiny component of the operating system necessary to execute the Docker container as a standalone unit on any host.
	
- **A container is an enviorment for isolated processes, the container have its own filesystem** 
- **The container shares the host kernel**


How it works:
You need a docker engine (like docker) to manage containers, the docker deamon process manages the containers,  


### Compared to a virtual machine:
* Both VM's and Containers look similar on the surface, they are portable, isolated execution environments with root filesystems.
	* **VM's** 
		* Has it's own OS kernel, ``init`` process, & drivers that interact with hardware.
		* More resource intensive.
		* Higher level of isolation.
	* **Container** 
		* A facade/imitation of an operating system. It's packages an executable with its dependencies needed to run.
		* More lightweight & portable

Usage examples:



![[Pasted image 20250104131953.png]]

---
# 2024-06-05
![[Pasted image 20250104115333.png]]



---
# 2024-08-27
![[Pasted image 20250104115351.png]]

- **Choice 1**: *"at"*
	The ‘at’ is a command that allows the users to schedule one-time tasks or recurring jobs at a specific time and date.
	
	#Eample 
		Schedules a one-time task to echo “Backup complete” at 09:00
		`echo "echo 'Backup complete'" | at 09:00
		`
		Schedules a one-time task to echo “Backup complete” at 09:00
		`echo "echo 'Backup complete'" | at 9am
		`
		Schedules a one-time task to echo “Backup complete” at 09:00
		`echo "echo 'Backup complete'" | at 012624
		`
		

- **Choice 2**: *"crontab"*
	The 'crontab' is a file containing the schedule of various cron entries that should be run at specified times.
	
	#Eample 
		MIN	HOUR DOM MON DOW **CMD**
		`30 08 10 06 * /home/maverick/full-backup
		`
		