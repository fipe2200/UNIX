# 2024-01-08

![[Pasted image 20250104115407.png]]

1. ``sudo apt install <necessary packages>`` Installs essential tools to build the kernel.
2. ``wget <link to kernel.org kernel>`` Downloads a stable kernel from kernel.org.
3. ``make menuconfig`` To configure what modules you want installed in the kernel.
4. ``make fakeroot`` Simulates root privileges for compatibility reasons to compile the kernel.
5. ``sudo make modules install`` Install the kernel modules.
6. ``sudo make install`` Install the kernel.
7. Before rebooting I made sure the **GRUB** bootloader menu shows up so I can select the new kernel.
	1. ``sudo vim /etc/default/grub`` -> comment out *GRUB_HIDDEN_TIMEOUT=0*
8. ``sudo update-grub`` & ``sudo reboot`` 
---
# 2024-06-05 
![[Pasted image 20250104115423.png]]
## **Crontab-File**:
```
MIN HOUR DOM MON DOW CMD
00 03 * * 2 CMD
```

Related:
[[Fråga 1#**Choice 2** *"crontab"*]]

---
# 2024-08-27
![[Pasted image 20250104115441.png]]

- **Numbers**: Must define every user access permission.
	-  ``chmod 774 file`` Gives *user*/*group*/*other* rwx/rwx/r-- permissions.
		- May be bad as it could sever access to processes you might not be aware of.
- **Letters**: May define specific users access permission.
	- ``chmod u+rwx file`` Gives user (owner) rwx permissions.
		- **ugoa** - **u**ser, **g**roup, **o**ther, **a**ll
	- Resolves the potential issue of defining wrong access for a user.

The numbers are 3 *octagonals* 0-7 representing *read*, *write*, & *execute*
* 0 = ---
* 1 = --x
* 2 = -w-
* 3 = -wx
* 4 = r--
* 5 = r-x
* 6 = rw-
* 7 = rwx

**Umask** is an *inverted* permission mask for ``chmod`` 
* *Umask 022* = ``chmod 755`` 
* *Umask 475* = ``chmod 302`` 