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


---
# 2024-08-27
![[Pasted image 20250104115441.png]]