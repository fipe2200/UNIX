
# 2024-01-08
![[Pasted image 20250104115140.png]]
### What it is
- A **container** is an *isolated* *instance* of an *image*, and uses the *hosts* *kernel* features to isolate processes in the container root filesystem.
	- Container processes *cannot* reach outside of the container, similar to *chroot*
	- The *Docker* *image* is a collection of files that constitute a tiny component of the operating system necessary to execute the Docker container as a standalone unit on any host.
### How it works
* You need a container engine (**docker**) to *manage* containers, the **dockerd** deamon process works as an interface to manage the containers. Docker *creates* a read/write layer to the *union filesystem* of an image that the container can update (this is called a *Copy-on-write* *strategy*).

* Docker engine uses several *kernel* *features* that are essential for *isolating processes*. 
* #Example
	- **namespaces** - UserID, Filesystem mounts...
	- **control groups** (**cgroups**) - Limits use of system resources, prioritizes processes over others.
	- **Capabilities** - Allows processes to execute sensitive kernel operations & system calls **instead of full sudo privilege**
	- **Secure computing mode** (**seccomp**) - Restricts access to system calls, a more fine-grained *Capabilities*.
### Compared to a virtual machine
* Both VM's and Containers look similar on the surface, they are both *portable*, *isolated* & *execution* *environments* with root filesystems.
* **Differences** 
* #### note man behöver nog inte memorera allt detta, men det är nog bra att få en överblick och förstå skillnaderna mellan dem
	* **VM's** 
		* Has it's own OS *kernel*, ``init`` process, & drivers that *interact* *with* *hardware*.
		* *Requires* full boot procedure; starts in 1-2 min
		* *Long-lived*.
		* Has *dedicated* virtual disks through hypervisor.
		* Images measured in *GB*.
		* *Complete isolation* among guests.
		* More *resource* intensive.
		* May run *multiple* independent OS *side by side*.
	* **Container** 
		* Is a *facade*/*imitation* of an OS. It packages an executable with its dependencies needed to run.
		* *No boot required*; processes run directly by the kernel; starts in <1 sec.
		* *Frequently* *replaced*.
		* Filesystem is a *layered construct* defined by the container engine (**docker**).
		* Images measured in *MB*.
		* More *lightweight* & *portable*.
		* Must run the *same kernel as host* (OS may differ).
### Usage examples
* **Containers**
	* *Web development*:  Containers are a great choice since they are *lightweight* and are easy to deploy in a variety of environments such as development staging and production. 
	* *Cloud computing*: Are easy to scale up and scale down to meet the demand. 
	* *Continuous integration and delivery (CI/CD)*: Containers are used for *automate* the process of building, testing, and *deploying* applications.
* **VM**
	* *Testing*: Virtual machines are great to test new software in a safe environment if the software breaks the system you can restart the VM or just start a new VM. Since VM are isolated it won't risk it's surroundings.

![[Pasted image 20250104131953.png]]

---
# 2024-06-05
![[Pasted image 20250104115333.png]]
``ls -l /dev/sda /dev/tty``

List of what the *first* *character* can be:```
```
- = Regular file  (text file)
b = Block device file  (hard drive)
c = Character device file  (terminal)
d = Directory  (/home)
l = Link / Symbolic link
p = Pipe or First-In First-Out special file  (intermediary file between processes)
s = Socket file (data exchange through socket, opendkim.sock)
```

* ``b rw- rw- --- 1 root disk 8, 0 okt 12 08:18 sda``
	* "**b**" means *block device file*, it handles data in *blocks*. #Example *hard drive* (sda).
	* The *first* **rw-** means that the *owner users* has read and write privileges, but no execution rights.
	* The *second* **rw-** means that *group users* have read and write privileges, but no execution rights.
	* The *last* **---** means that *other* *users* have no rights to the file. 
	* "**1**" indicates that there is one *hard link* referring to this file. 
	* **root** is the *owner user*.
	* **disk** is the *owner group*.
	* **8** is the *major* device number
	* **0** is the *minor* device number
	* "**okt 12 08:18**" is the *date* and *time* of when it was *last modified*
	* **sda** is the device *file name* 
 
* ``c rw- rw- rw- 1 root tty 5, 0 okt 12 08:08 tty``
	* "**c**" means *character* *device file*, it handles data as *streams of characters* #Example *terminal* (tty). 
	* The *first* **rw-** means that the *owner users* has read and write privileges, but no execution rights.
	* The *second* **rw**- means that *group users* have read and write privileges, but no execution rights.
	* The *last* **rw**- means that *other users* have read and write privileges, but no execution rights.
	* This file has "**1**" *hard link* referring to it.
	* **root** is the *owner user*.
	* **tty** is the *owner group*.
	* **5** is the *major* device number.
	* **0** is the *minor* device number.
	* "**okt 12 08:08**" is the *date* and *time* of when it was *last modified*.
	* **tty** is the device *file name*.

---
# 2024-08-27
![[Pasted image 20250104115351.png]]
## **Choice 1**: *"at"*
- The ‘at’ is a command that allows the users to schedule one-time tasks or recurring jobs at a specific time and date.
	
	#Example 
	Answer:
	- Schedules a one-time task to restart the system at 01:00. Detta måste man göra som root-användare! Detta genom:
		```sudo su```
		Sedan:
		```echo "reboot" | at 01:00```
	
	More:
	* Schedules a one-time task to echo “Backup complete” at 09:00
		```echo "echo 'Backup complete'" | at 09:00```
		
	- Schedules a one-time task to echo “Backup complete” at 09:00
		```echo "echo 'Backup complete'" | at 9am```
		
	- Schedules a one-time task to echo “Backup complete” at 26th of January, 2024.
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


# 2018-01-16
![[Pasted image 20250109131905.png]]
Samma som [[fråga 3#2024-08-27]] 
# 2018-10-30
![[Pasted image 20250109131620.png]]
Samma som [[Fråga 2#2024-01-08]]
# 2018-03-21
![[Pasted image 20250109131820.png]]
### How to check this?
* ``stat <file>`` or ``find`` using ``-mtime``, ``-ctime``, ``-atime``
### Differences
* *Modification time* is when the file *content* was last modified.
* *Access time* is when the file was *last read*.
* *Change time* is when the file *metadata* (name, ownership, permissions) was last changed.
	* *meta-information* such as Inode, Blocks, file type, Size, creation date, device.
