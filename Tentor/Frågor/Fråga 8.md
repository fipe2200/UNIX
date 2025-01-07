# 2024-01-08
![[Pasted image 20250104115928.png]]
### Manual boot from GRUB
* Enter the *GRUB* boot menu by either configuring *grub.cfg* first or hold *Esc* key during boot.
* Press "*c*" to enter *GRUB* command line while in the *GRUB* menu.
* Select the *root* *partition*
* Select & load *kernel* 
* Load *ramdisk*
* Run ``boot`` 

---
# 2024-06-05
![[Pasted image 20250104115940.png]]
* *Load averages* are the amount of *computational work* a system performs in different *time* *intervals*.
	* It's useful to figure out if the *CPU* is working *over* its capacity *or* *not*.
		* #Example If you have *performance* *issues*, if any load average number is *higher* than the amount of cores in your system, that means the *CPU* is working *over capacity*.
			* If *higher* than core *amount*, investigate & possibly replace that hardware bottleneck.
	* The 3 values are *1 minute*, *5 minute*, and *15 minute* time intervals of load averages, representing the % of *CPU* *capacity* in each interval.

---
# 2024-08-27
![[Pasted image 20250104115953.png]]

* The purpose of *ramdisk* is to *improve* performance on the the boot process by acting as a *temporary storage* with high-speed data access utilizing *RAM*, instead of a regular HDD or SSD.  
* #### Related info but not for this question
* *ROM* (Read-only-memory)
	* Is where firmware like *BIOS*/*UEFI* and the *GRUB* bootloader is stored and loaded first on boot (in our *VM's* they were typically stored in */dev/sda1* or *sda2*).
		* After *GRUB* loads the kernel, the *kernel* may use ``initrd`` (using *ramdisk*) to load temporary files faster this way.