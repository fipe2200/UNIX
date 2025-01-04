
# 2024-01-08
![[Pasted image 20250104115140.png]]

What it is:
- **A container is an instance of an image,** 
	  The Docker image is a collection of files that constitute a tiny component of the operating system necessary to execute the Docker container as a standalone unit on any host.
	
- **A container is an enviorment for isolated processes, the container have its own filesystem** 
- **The container shares the host kernel**


How it works:
You need a docker engine (docker) to manage containers, the docker deamon process manages the containers. 

Docker engine uses several kernel features that are essential for isolating processes. Example:
- **namespaces**:
	  
- **control groups**:
  
- **capabilities**:
  
- **secure computing mode**:
  



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
b rw- rw- --- 1 root disk 8, 0 okt 12 08:18 sda
* "b" means that this is a block device file that handles data in blocks, like a hard drive.
* The first rw- means that the owner has read and write privileges, but no execution rights.
* The second rw- means that groups have read and write privileges, but no execution rights.
* The remaining --- means that other users have no rights to the file. 
* "1" indicates that there is one hard link referring to this file. 
* root is the owner
* disk is the group owner
* 8 is the major device number
* 0 is the minor device number
* "okt 12 08:18" is the date and time of when it was last modified
* sda is the device file name 

c rw- rw- rw- 1 root tty 5, 0 okt 12 08:08 tty
* "c" means that this is a character device file that handles data as streams of characters, like a terminal. 
* The first rw-- means that the owner has read and write privileges, but no execution rights.
* The second rw-- means that groups have read and write privileges, but no execution rights.
* The last rw- means that other users have read and write privileges, but no execution rights.
* This file has "1" hard link referring to it
* root is the owner
* tty is the group owner
* 5 is the major device number
* 0 is the minor device number
* "okt 12 08:08" is the date and time of when it was last modified
* tty is the device file name



---
# 2024-08-27
![[Pasted image 20250104115351.png]]
## **Choice 1**: *"at"*
- 
	The ‘at’ is a command that allows the users to schedule one-time tasks or recurring jobs at a specific time and date.
	
	#Example 
	- Schedules a one-time task to restart the system at 01:00
		```sudo restart | at 01:00```
		
	* Schedules a one-time task to echo “Backup complete” at 09:00
		```echo "echo 'Backup complete'" | at 09:00```
		
	- Schedules a one-time task to echo “Backup complete” at 09:00
		```echo "echo 'Backup complete'" | at 9am```
		
	- Schedules a one-time task to echo “Backup complete” at 09:00
		```echo "echo 'Backup complete'" | at 012624```
		

## **Choice 2**: *"crontab"*
- 
	The 'crontab' file is containing the schedule of various cron entries that run scripts or Linux Commands at specified times and intervals. It is ideal for repetitive tasks such as system maintenance, backups, and updates.
	![[Pasted image 20250104140455.png]]
	#Example 
		MIN	HOUR DOM MON DOW **CMD**
		```30 08 10 06 * /home/maverick/full-backup```