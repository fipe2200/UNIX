# 2024-01-08
![[Pasted image 20250104120056.png]]
I forgot to make sure the disks are *persistently* *mounted* on boot in the */etc/fstab* file. To fix this I'll go ahead and ``mount`` the disks again, then use ``blkid`` to find the *UUID* of each filesystem, as it's recommended to use the *filesystem ID* (*UUID*) rather than the *path* to it. I enter this in the */etc/fstab* along with further options: ``<UUID> <mountpoint> <filesystem type> <access permissions> <whether to dump it or not> <boot order>`` 

---
# 2024-06-05
![[Pasted image 20250104120112.png]]
* **Grub** (Grand Unified bootloader).
	* Is a second stage boot loader application of BIOS/UEFI whose main job is to *select* and *load* the OS *kernel*.
		* Can be configured from a plain text file *grub.cfg*.
	* *Grub* also responsible for *assembling* *configurations* for the *kernel*.
		* May also run a *grub* command line at boot time.
		* #Example 
			* *-s* for *single user* mode instead of normal boot process.
* **Kernel** 
	* [[Fråga 3#What does the kernel do?]]
	* [[Fråga 3#What can be found in the kernel space?]]
* **Shell**
	* A shell is a command line interpreter program that provides users an interface to control the OS *kernel*.
	* #Example *bash*, *sh*. 
		* *bash* is an interactive shell mainly used to start programs.
		* *sh* is mainly used to run *sh* shell scripts efficiently.
* **GUI** (Graphical User Interface)
	* A *GUI* lets users interact with devices using graphical icons.
	* #Example 
		* In lab 1, when we ran ``make menuconfig``, the *menu* we interface with is a *GUI*
	* #Example 
		* The *Terminal* application is a shell *GUI*

---
# 2024-08-27
![[Pasted image 20250104120126.png]]
### To find a runaway process
* Run ``top`` and look for *high* CPU utilization.
* When running ``top``, press *f* and navigate to the *DATA* column & press *space bar*. Look for *unexpected* growth over time & absolute size.
* Run ``uptime`` for *unexpectedly* *high* or *spiking* load averages.
	* Load averages should be less than the total amount of *cores* in the CPU.
### Suspending and later starting a process up again
* After confirming the behaviour in unexpected, run ``kill -STOP`` to *suspend* the process. 
* After addressing the issue, run ``kill -CONT`` to let the process *continue* executing again.




# 2018-01-16
![[Pasted image 20250109134704.png]]
Related: [[Administration av UNIX-lika system 1#ch 2.1 boot process overview]]
# 2018-03-21
![[Pasted image 20250109134735.png]]
Samma som [[Fråga 9#2024-08-27]]
# 2018-10-30
![[Pasted image 20250109134815.png]]
**When changing runlevels:
- **Unnecessary services** are stopped.
- **Required services** for the new runlevel are started.
- The system’s overall kernel state remains unchanged.
- The process ensures the system transitions smoothly to the desired operational mode.