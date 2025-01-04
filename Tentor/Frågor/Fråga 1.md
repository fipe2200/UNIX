
# 2024-01-08
![[Pasted image 20250104115140.png]]
### What it is
- A **container** is an *isolated* *instance* of an *image*, and uses the *hosts* *kernel* features to isolate processes in the container root filesystem.
	- Container processes *cannot* reach outside of the container, similar to *chroot*
	- The *Docker* *image* is a collection of files that constitute a tiny component of the operating system necessary to execute the Docker container as a standalone unit on any host.
### How it works
You need a container engine (**docker**) to manage containers, the **dockerd** deamon process works as an interface to manage the containers. Docker creates a read/write layer to the union filesystem of an image that the container can update (*Copy-on-write* *strategy*).

Docker engine uses several *kernel* *features* that are essential for *isolating processes*. Example:
- **namespaces**
	- UserID, Filesystem mounts.
- **control groups** (**cgroups**)
	- Limits use of system resources, prioritizes processes over others.
- **Capabilities**
	- Allows processes to execute sensitive kernel operations & system calls.
- **Secure computing mode** (**seccomp**)
	- Restricts access to system calls, more fine-grained than **Capabilities**.
### Compared to a virtual machine
* Both VM's and Containers look similar on the surface, they are portable, isolated execution environments with root filesystems.
	* **VM's** 
		* Has it's own OS kernel, ``init`` process, & drivers that interact with hardware.
		* More resource intensive.
		* Higher level of isolation.
	* **Container** 
		* A facade/imitation of an OS. It packages an executable with its dependencies needed to run.
		* More lightweight & portable
### Usage examples
**Containers**
* *Web development*:  Containers are a great choice since they are *lightweight* and are easy to deploy in a variety of environments such as development staging and production. 
* *Cloud computing*: Are easy to scale up and scale down to meet the demand. 
* *Continuous integration and delivery (CI/CD)*: Containers are used for *automate* the process of building, testing, and *deploying* applications.

**VM**
* *Testing*: Virtual machines are great to test new software in a safe environment if the software breaks the system you can restart the VM or just start a new VM. Since VM are isolated it won't risk it's surroundings.

![[Pasted image 20250104131953.png]]

---
# 2024-06-05
![[Pasted image 20250104115333.png]]

ls -l /dev/sda /dev/tty

List of what the first character can be:
- -  = Regular file  
* b = Block device file  
* c = Character device file  
* d = Directory  
* l = Link - Symbolic link  
* p = Pipe or First-In First-Out special file  
* s = Socket file

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
- The ‘at’ is a command that allows the users to schedule one-time tasks or recurring jobs at a specific time and date.
	
	#Example 
	Answer:
	- Schedules a one-time task to restart the system at 01:00
		```sudo restart | at 01:00```
	
	More:
	* Schedules a one-time task to echo “Backup complete” at 09:00
		```echo "echo 'Backup complete'" | at 09:00```
		
	- Schedules a one-time task to echo “Backup complete” at 09:00
		```echo "echo 'Backup complete'" | at 9am```
		
	- Schedules a one-time task to echo “Backup complete” at 09:00
		```echo "echo 'Backup complete'" | at 012624```
		

## **Choice 2**: *"crontab"*
- The 'crontab' file is containing the schedule of various cron entries that run scripts or Linux Commands at specified times and intervals. It is ideal for repetitive tasks such as system maintenance, backups, and updates.
	
	```
	MIN	HOUR DOM MON DOW CMD
	30 08 26 01 * CMD
	```
	
	MIN = Minute
	HOUR = Hour
	DOM = Date
	MON = Month
	DOW = Day Of Week
	CMD = Command
	
	#Example 
	Answer:
	- Restarts the machine every date, month, year and day of the week at 01:00. (Using root's crontab, as then you have sudo/root privileges)
		```00 01 * * * /sbin/reboot ```
	
	More:
	- Executes the Full backup shell script (full-backup) on 10th of June, every day of the week at 08:30.
		```30 08 10 06 * /home/maverick/full-backup```


	![[Pasted image 20250104140455.png]]

