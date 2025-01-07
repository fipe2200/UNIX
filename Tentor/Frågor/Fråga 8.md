# 2024-01-08
![[Pasted image 20250104115928.png]]

---
# 2024-06-05
![[Pasted image 20250104115940.png]]

---
# 2024-08-27
![[Pasted image 20250104115953.png]]

* The purpose of *ramdisk* is to *improve* performance on the the boot process by acting as a *temporary storage* with high-speed data access utilizing *RAM*, instead of a regular HDD or SSD.  
* #### Related info but not for this question
* *ROM* (Read-only-memory)
	* Is where firmware like *BIOS*/*UEFI* and the *GRUB* bootloader is stored and loaded first on boot (in our *VM's* they were typically stored in */dev/sda1* or *sda2*).
		* After *GRUB* loads the kernel, the *kernel* may use *initrd* (using *ramdisk*) to load temporary files faster this way.