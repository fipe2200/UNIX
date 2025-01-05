# 2024-01-08
![[Pasted image 20250104115556.png]]
### How to seamlessly transition users from an old server to a new server without downtime
* ????????
* **complete guess**: 
	* Make a *backup* of your environment into the new server using ``rsync``
	* Run it there to make sure everything works as intended
	* Migrate users little by little as to not overwhelm the server.
	* something something 
#### (inte klar)


---
# 2024-06-05
![[Pasted image 20250104115609.png]]

* ### Building directly into kernel
	* Installed during kernel *configuration* / *building*.
		* #Example ``make menuconfig`` To select modules -> ``make modules install`` To install modules into kernel before building the kernel.
	* #### Pros
		* Modules are included in the kernel binary *on boot*.
			* *Always* available, not too complicated.
			* Good for devices like *networking* *drivers* & *storage* for root filesystems, that are *required* on boot.
	* #### Cons
		* *Not* *flexible*, replacing/updating the driver module requires *recompiling* the kernel.
		* *Harder* *to* *debug* than a loaded driver as it is *part* *of* the kernel binary.
			* Larger kernel *size*.
* ### Manually loading a driver as a module
	* Can be loaded/removed from the kernel during *runtime*.
		* Loadable modules are in ``/lib/modules/<linux version>``
		* #Example ``sudo modprobe <module>`` to load / ``sudo modprobe -r <module>`` to remove
	* #### Pros
		* Modules can be loaded/unloaded at runtime *without rebooting*.
			* Good for *testing*.
		* *Non-essential* modules can be loaded *as* *needed* rather than always present in the kernel.
			* Smaller kernel *size*.
	* #### Cons
		* Only last *until* next reboot.
		* Requires *dependency* *management* of modules.
		* Potential *security* *risk*, must trust the module vendor.

---
# 2024-08-27
![[Pasted image 20250104115626.png]]
- #### Följande 3 exempel är nog overkill för denna fråga, men det är bra att färska upp minnet om en specifik labb-fråga kommer istället.
* **SAMBA** is best used to share files from *UNIX* to a *windows* computer. Although *FTP* and *NFS* **can** work, *samba* is *designed* to share between UNIX and windows, as windows uses the **SMB** **protocol** (*Server Message Block*) for file and printer network sharing, which a samba server also implements.
- #Example 
	- In lab 3 we assigned *samba* *passwords* to the users that will access the share ``smbpasswd -a <user>`` then validated them ``smbpasswd -e user``.
	- We defined the *share* *name*, *user* *access* and further *restrictions* to the server in the */etc/samba/smb.conf* configuration file.
	- Then connect to the samba server ``smbclient //<server ip>/<name of share>``.

- **FTP** is a protocol for sending files over a network, and is compatible over different filesystems.
	- Is best used for *big-* or *plain-file* transfers
	- *Fast* and efficient.
- #Example 
	- In lab 3 I used *vsftpd*, which uses the configuration file */etc/vsftpd* for user access.
	- You connect *directly* to a server using ``ftp <serverip>``, and may use for instance ``put`` to *copy* a file from your working directory into the server directory, or ``get`` to download from the server.

- **NFS** Is for *sharing* *filesystems* to different computers over networks, you *mount* a filesystem to a mountpoint making it accessible to navigate into.
	- Useful when *groups* want to share the *same* *files*.
- #Example 
	- For *nfs* you must define which filesystems to export in */etc/exports* 
	- Both the *nfs* client and server run an *identity* *mapping* *daemon* to check that *UID*/*GID* are *congruent* over the different systems using the */etc/passwd* file, for *share access*.
		- Mapping is configured in the */etc/ipmapd.con* file (*nfsv4*).
	- Then you *export* the shared filesystem using ``sudo exportfs -a``
	- Finally you run ``sudo mount -t nfs -o nfsvers=4 <server ip>:/<shared dir> /mountpoint`` making the share freely accessible to whoever is permitted to enter the mountpoint.
