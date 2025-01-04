
# 2024-01-08
![[Pasted image 20250104115140.png]]

What it is:
- **A container is an instance of an image,** 
	  The Docker image is a collection of files that constitute a tiny component of the operating system necessary to execute the Docker container as a standalone unit on any host.
	
- **A container is an enviorment for isolated processes, the container have its own filesystem** 
- **The container shares the host kernel**


How it works:


Compared to a virtual machine:


Usage examples:

---
# 2024-06-05
![[Pasted image 20250104115333.png]]
b rw- rw- --- 1 root disk 8, 0 okt 12 08:18 sda
* "b" means that this is a block device file like a hard drive.
* The first rw- means that the owner has read and write privileges, but no execution rights.
* The second rw- means that groups have read and write privileges, but no execution rights.
* The remaining --- means that other users have no rights to the file. 
* "1" indicates that there is one hard link referring to this file. 
* root is the owner
* disk is the group owner
* 8 is the major device number
* 0 is the minor device number
* "okt 12 08:18" is the date and time of when the file was last modified
* sda is the name of the file

c rw- rw- rw- 1 root tty 5, 0 okt 12 08:08 tty
* "c" means that this is a character device file like a terminal. 
* The first rw-- means that the owner has read and write privileges, but no execution rights.
* The second rw-- means that groups have read and write privileges, but no execution rights.
* The last rw- means that other users have read and write privileges, but no execution rights.
* This file has "1" hard link referring to it
* root is the owner
* tty is the group owner
* 5 is the major device number
* 0 is the minor device number
* It was last modified okt 12 08:08
* tty is the name of the file

---
# 2024-08-27
![[Pasted image 20250104115351.png]]