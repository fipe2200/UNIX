# 2024-01-08
![[Pasted image 20250104115503.png]]
### What does the kernel do?
The **kernel** acts as a "central government" of a UNIX/Linux system. It's responsible for *enforcing rules*, *sharing* *resources*, and *providing* *core* *services* that user processes rely on.
* Acts as a high-level interface for the systems *hardware*.
	* Similar to an *API* in programming.
* #Example In lab 2 we changed the niceness of processes using ``nice`` & ``renice``, a process' *niceness* represents a numerical hint for the kernel about the process' priority for accessing the *CPU*. 
### What can be found in the kernel space?
* Management & abstraction of **hardware** **devices**.
* **Processes** & **threads** (and ways for them to communicate)
* Management of **memory** (virtual memory & memory-space protection)
* **I/O** facilities (filesystems, network interfaces, serial interfaces...)
* Housekeeping **functions** (startup, shutdown, timers, multitasking...)
* #Example In lab 2 we accessed kernel summary statistics about *threads*, *memory*, *paging*, *interrupt* activity and more using ``vmstat``. 
* #Example In lab 2 we ran ``dmesg`` to access the *kernel ring buffer*, which contains logs of the kernel boot process & console output.

---
# 2024-06-05
![[Pasted image 20250104115521.png]]
If we have the default permissions 777, and apply these umasks, we get:

777 - 755 = 022 
777 - 500 = 277 
777 - 110 = 667 
read, write and execute privileges are determined using the octadecimal system.
Users Groups Others
rwx      rwx       rwx 
000      000      000 (or any other combination of one's and zero's) 



Related:
[[Fråga 2#2024-08-27]]

---
# 2024-08-27
![[Pasted image 20250104115539.png]]
## **ls**
- List files
	  
	#Example
	Will list all files including hidden files (files with names beginning with a dot)
	`ls -a`
	  
	List files with more info
	`ls -l` 
	 ```
	 drwxr-xr-x   6 eva        users         1024 Jun  8 16:46 sabon
	 -rw-------   1 eva        users         1564 Apr 28 14:35 splus
	 ``` 
	Related:
	[[Fråga 1#2024-06-05]]
## **cd**
- change directory
	
	#Example
	changes directory to Desktop
	`cd Desktop`
	
	Goes back in directory path
	`cd ..`
## **cat**

## **nano**

## **chmod**

## **chown**
