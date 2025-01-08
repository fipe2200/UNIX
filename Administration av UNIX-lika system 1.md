## To read: 
 - [x]  [Lab 0](http://ver.miun.se/courses/DT149G/labs/lab_assgn0.pdf): Ch. ~~1~~, ~~6.1-6.4, 6.6~~
 - [x]  [Lab 1](http://ver.miun.se/courses/DT149G/labs/lab_assgn1.pdf): Ch. ~~11.1~~-~~11.4, 11.6-11.9~~ ~~and 24~~ 
	 - [x] Send in report by 28/11
 - [x]  [Lab 2](http://ver.miun.se/courses/DT149G/labs/lab_assgn2.pdf): Ch. ~~4~~, 10, ~~29~~
	 - [x] Send in report by 1/12
 - [x]  [Lab 3](http://ver.miun.se/courses/DT149G/labs/lab_assgn3.pdf) Ch. ~~2~~, ~~3~~, 5, 8, ~~21, 22, 27,8~~, consult listed documents
	 - [x] Send in report by 8/12
 - [x]  [Lab 4](http://ver.miun.se/courses/DT149G/labs/lab_assgn4.pdf) Ch. ~~16, 25~~, consult listed documents
	 - [x] Send in report by 15/12
 - [x]  [Lab 5](http://ver.miun.se/courses/DT149G/labs/lab_assgn5.pdf) Ch. 18, consult listed documents
	 - [x] Send in report by 29/12
 - [x]  [Lab 6](http://ver.miun.se/courses/DT149G/labs/lab_assgn6.pdf) Ch 27.6, 27.8, 16.10, also read [core concepts & building](https://docs.docker.com/build/concepts/overview/)
	 - [x] Send in report by 5/01

 [Study guide](http://ver.miun.se/courses/DT149G/Documents/studyguide.pdf)

**Questions**: 
* eth0 vs enp0s3
* authoritative vs master server
	* parent vs child (ns1?)  
* *tentafråga*: migrate users to a new server with *no* downtime
	* ``rsync``? 
	* redirect (point) the new *DNS* 
* lånedator
* **upstart** 
	* old
### Tentagenomgång
Förstå tillämpning av labbarna
* pros/cons
* när saker används
## [Tentaplugg](https://elearn20.miun.se/moodle/pluginfile.php/1747159/mod_resource/content/2/DT149G_20210109.pdf)

### Lärandemål
• Knowledge on how to customize the kernel of your system.
* **Steps to customize kernel**
	* [[Fråga 2#2024-01-08|Steps to customize kernel]] 
• Become familiar with process handling, priorities and scheduling.
* **Process handling**
	* [[Fråga 8#2024-06-05|load averages]], [[Fråga 9#2024-01-08|finding bottleneck/replace hardware]] 
	* [[Fråga 9#2024-06-05|background/foreground]]
* **Priorities**
	* [[Fråga 9#2024-08-27|nice/renice]]
* **Scheduling**
	* [[Fråga 1#2024-08-27|at vs cron]] 
• Knowledge how logging works in a UNIX-like system.
* **Syslog**
	* [[Fråga 5#2024-01-08|infrastructure/how it works/what it contains)]]
	* [[Fråga 5#Problems|Problems with syslog]]
• Become familiar with upstart, init and boot scripts.
* **the upstart process**
	* [[Administration av UNIX-lika system 1#Timeline of boot process|Timeline of boot process]]
* **init**
	* [[Administration av UNIX-lika system 1#ch 2.6 system management daemons|System management daemon]]
* **Boot scripts** (*/etc/init.d*)
	* syslog, udev, mount, ssh, Runlevels/target.
		* #Example As we saw in lab 2(?), runlevel directories (*/etc/rc.*d*) are symlinked to */etc/init.d*. 
			* The runlevel *dictate* which *boot scripts* to run.
• Know how to administrate user accounts.
* #Example ``sudo adduser <username>`` 
	* prompts *user* *information* and *password* to assign (*enter* to skip).
• Knowledge how to partition and format new hard drives for your system.
* #Example Labb 3 
• Be able to set up storage backup on your system.
* 
• Have the knowledge of setting up an IPTables firewall.
• Be able to setup and administer docker containers.
• Be able to correctly set up and administrate your own domain using
BIND.
• Have basic understanding of DNSSEC.
• Have the knowledge to set up an SMTP server process.
• Be able to set up the necessary security measures so that an email
sent from your SMTP server will not be regarded as spam and
cannot easily be used by spammers.
• Know how to correctly set up your DNS to handle email and related
mechanisms.
• Be able to install and configure software for delivering emails using
either POP3 or IMAP.
• Have the knowledge of creating your own docker image.
• Have a better insight into how containers can be created and used.

- [Permissions](https://unix.stackexchange.com/questions/94212/chmod-by-letters-vs-numbers "https://unix.stackexchange.com/questions/94212/chmod-by-letters-vs-numbers")
	- **Numbers**: Must define every permission (*user+group+other*: ``chmod 774 file``)
	- **Letters**: Defines specific permission (*user*: ``chmod u+rwx file``)
		- **ugoa** - user, group, other, all
- **Scheduling**: Usable for backups, database maintenance, or nightly batch jobs
	- ``at``: One time use command 
		- *reboot at 02:00*: ``echo "sudo reboot" | at 2AM``  
			- #### must be ran in root shell (``sudo su``)
	- ``cron``: Uses ``crontab`` for repeating tasks
		- *Run an update on Monday at 01:30 every week of the year*: `30 1 * * MON /bin/update.sh` 
- **fsck** checks the given filesystem(s) for issues and to make sure a fresh system works as intended (see lab 3)
- To best **share files with a windows** computer, **SAMBA** would be preferable. Although **ftp** and **nfs** _can_ work, SAMBA is designed to share between UNIX and windows as windows uses the SMB (Server Message Block) protocol for file and printer network sharing (check book for better wording). To set it up one must just install SAMBA, assign samba passwords to the user that will share, and ... (see lab)
	- **FTP** Is best used for big or plain file transfers, you connect to a server and ``put``/``get`` directly to it.
	- **NFS** Is for sharing filesystems, you mount a filesystem to a mountpoint making it accessible to navigate. 

* **Backups** ``tar`` vs ``cpio`` vs ``cp`` vs ``rsync``
	* Both ``tar`` and ``cpio`` archive many files to a *single* *stream*
		* ``tar`` can read direct inputs while ``cpio`` needs a ``find`` operation
			  ``cpio`` maintains hard links & more, better suited for backing up *filesystems*
	* ``rsync`` is used to **synchronize** for example a source with a backup. If you have a backup of your home directory, ``rsync`` will only send the changes made in your home directory rather than the entire **/home** to the backup location. May also be used over networks with **ssh**.
	* ``cp`` is used mainly for quick and small backups or transfers. It's fast but doesn't take into account environment such as links (?).

### A. Bushan (FTP) A file transfer protocol
**Introduction**
* *Computer network usage*: 2 categories
	* *Direct*: Network user logged into a *remote host*
		* Must know how to use remote systems
	* *Indirect*: no login *nor* knowledge of system required
		* *intermediate process* homogenizes convention differences
		* assumes *network file transfer process* at host using common protocol
**Objective**
* Promote *indirect* use of computers on the network
	* user/program needs *uniform interface* to network filesystem
		* through standard protocol
* *Reliably transfer* binary or ASCII files 
	* & data (defined as attributes in file headings)
* *Shield* user from host file storage systems

* FTP includes "execute" *request*
**Transactions**
* Entity of info communicated between processes
	* 72-bit field: descriptor, var length, data, and filler fields
	* 
### Genomgång labb 4
note: cali. zone file must be **recursive** in *lab*
* cali zone file: sub domains -> duckberg, who subs mcduckcorp
	* if cali is recursive we can make sure links work
* **DNS**
*  *Maps IP-numbers to domain names* (192.214.22.148 -> www.google.com)
	* **improves routing**
		* ex. netflix
	* **email auth**
	* används med *kerberos*
		* färdiga DNS poster finns *definierade*
	* **protocol**
	* *hierarchic* namespace
		* used *to ID* host or domains
			* domain is delmängd of tree
				* ex. 
		* *structure*: root -> top level domain -> main domain -> sub domain ->node
			* *root*: 13 in the world, 11 mirrors in sweden
			* *top level domain*: administered by **IANA**
				* Registry (country, .se) -> registrator (org, reseller) -> registrant (user)
			* *main*: can be purchased
			* *sub*: our server
			* *node*: pc?
		* *limitations*: 
			* limited to ASCII
				* 255 char
			* came 2003 to allow non ASCII char
				* (*resolver* converts åäö to xn-)
					* problem: open to attacks
						* ex. IDN homograph attack (paypal link)
	* **resolver**: contact DNS server
		* we will use `dig`
			* tool to query DNS servers
				* does DNS search and show result
					* useful for troubleshoot / auth
						* ex. `dig @server remote.netlab.miun.se A`
							* we **need** an answer section (returned or written?)
		* resolver **uses** layer 3->5 (similar to ARP)
		* search tech:
			* *iterative*
				* router send request to root, cant give all way, but can give to .se
					* router send to .se, can't give all way but can give .miun
						* etc
			* *recursive*
				* root ask .se, se ask miun, etc and back to root 
					* (almost never happens fully,)
			* *Inverted*
				* in_addr.arpa (Root) -> 255 per level
				* *important*: given netlab.miun.se
					* many are under se., then fewer and fewer as it goes up
						* for ip its *inverted* (193.24.5.12)
							* from IP -> DNS, it'll be  alot of posts at top
								* 12.5.24.193.in_addr.arpa
			* For lab: we do a *reverse DNS*: make new domain, we only write the domain (subnet)
			* *what usually happens*: our router -> ISP DNS -> does iterative search, then back to us
				* info cached on router (multiple users benefit)
	* *distributed database*
		* alla ansvarar för sin domän
		* most using **BIND**
* Config of **BIND**
	* name.conf
		* "what zones does this DNS administer"
		* *forwarders*: this "DNS contact this server"
		* *allow*: access limitation (privacy)
		* *file*: path to DNS database
			* relativ eller specifik
			* add DNS posts (for *lab*)
				* **SOA**: defines DNS zone
					* **zone file**:
						* *macros* may help
						* *origin*: base domain (not needed if we use **SOA**)
							* rec 1 fil 1 zon for *lab*
						* **SOA**
							* *date + version in last numbers*: serial
							* *minimum*: if negative response in time
					* **Glue record**: @ IN NS ns1.netlab.miun.se
						* *name server*, @ means our zone
							* *NS* record type
							* *ns1.netlab.miun.se.* (must know IP address to get) ()
								* to get IP, we must have a record under it
								*  **last dot important**
							* (origin is just relative, name server is specific
					* sub domain **needs Glue** too
					* **Reverse** zone file:
						* **SOA** + **glue** *always* 
						* **ptr** *instead* of A record
				* *ns*: 
				* vi lägger till **ptr**, inte alla A'n
					* translates address to name
				* *cname* alias
				* *srv* record (kerberos) not used
					* *txt* record used instead

## Ch 1 Where to start
### Essential Duties of a System Administrator
* Controlling access
* Adding Hardware
* Automating Tasks
* Overseeing Backups
* Installing & Upgrading Software
* Monitoring
* Troubleshooting
* Maintaining Local Documentation
* Vigilantly Monitoring Security
* Tuning Performance
* Developing Site Policies
* Working With Vendors
* Fire Fighting

### Suggested Background
* Vim
	* text editor
	* vimtutor command
* bash/python
	* Scripting projects
	* chapter 7 for important things about scripting
* expect
	* front end for driving interactive programs

### Notation & typographical conventions (in this book)
* **cp** *file directory*
	* bold = literal, italic = change, so file -> actual file, directory -> actual directory



## Ch 2 booting and system management daemon 
Booting consists of
	Finding, loading n running bootstrap code
	FLR os kernel
	Run startup script run os kernel
	Maintain hygiene manage system state transition
All that continues while system is up

### ch 2.1 boot process overview 
*Systemd* streamlines boot process
* Adds dependency management 
* Support concurring startup processes 
* Comprehensive logging
today we use image management apis and ctrl panels
During bootstrapping, kernel loads into memory and executes initialization tasks
#### Timeline of boot process
* **Power on**
* Load firmware (*BIOS*/*UEFI*) from *NVRAM*
	* NVRAM = *Non-volatile RAM*, retains data without power (good for *firmware*)
* Identify/probe for *hardware*
	* #Example CPU, RAM, Storage, I/O devices, network interfaces
* Select *boot device* (*disk*)
* Identify *EFI* system partition
	* Contains *GRUB*
* Load boot loader (*GRUB*)
* Determine *kernel* to boot
* Load *kernel*
* Instantiate *kernel data structures* 
	* #Example Process table, page table, memory zones, inodes, and much more
* Start *init*/*systemd* as *PID1*
	* System & service *manager*, responsible for *booting* the system.
* Execute startup scripts 
	* System unit files (daemons, sockets, mounts,...)
* **Running system**
### ch 2.2 system firmware 
When power on, cpu hardwired to run boot code in ROM
FIRMWARE knows about devices in the mobo
Firmware lets you expose or disable to hide to the os
**Bios, now UEFI** 
Bios starts with a first stage boot loader mbr 
	Os agnostic 
To read fs, it needs second stage (grub)
	Can be stored in between mbr and first disk partition
	Volume boot record
Uefi understands fat, file allocation sys
	Communicates with gpt partition table to identify system partition and executes from there.
	No boot loader required 
		but it’s still good to use for management 
	like a Mini os as it defines api to access HW
		means uefi variables can be modified 
			ex. Change boot order
### ch 2.3 boot loaders
Identifies os kernel
Can send config arguments to kernel

### ch 2.4 grub grand unified boot loader
Default for linux
	grub can read txt cuz it can navigate root fs
	Config with grub-mkconfig and update-grub
	C in grub boot screen for cmd line to for ex. Edit config on boot time (temporary )
	tab for cmds 
### ch 2.6 system management daemons
**Init**
	Uses *sequential* scripts based on *runlevel*
	maintains *mode* of system 
		*Single user*
			Minimal fs no services
		*Multiuser* 
			All fs mounted, network services, window system and graphical login manager on console
		*Server*
			Similar multiuser, no gui on console 
	*Starts* and *stops* services as needed to bring system state in line with current active mode
	*init* has startup chores it runs commands or scripts 

Traditional init runs things in sequence, so later scripts won’t run until everything before it is finished

**Systemd** *formalizes* *init* into unified theory of how things should be configured, accessed, and managed
	Robust dependency model
	Manages targets, processes in parallel, network connections, kernel log entries, logins
Critiqued for being *overengineered* but it’s very useful for admins 

Init still useful for small installations that don’t need advanced process management 

### ch 2.7 Systemd in detail
Systemd tries to standardized config and control of system services
	Reaches further into system operations than init
Is a collection of programs, daemons, libs, techs, kernel components 

A unit is a service, socket, device, etc controlled by Systemd 
	Their behavior are defined in their unit files
		Structured similar to MS-dos .ini files 
		To edit don’t go to lib, to go etc
		Etc highest priority 
	Units use suffix 
		Services use .service etc…
		[unit] applies to all 
Systemctl
	Investigates status of Systemd and used to change its configs
	ran by default shows all units 
	systemctl link for symbiotic link from a Systemd system directory to a unit elsewhere in the fs
		Such units can be addressed by commands or named as dependencies
		Linking not well documented, book recommends making copies Instead 
	Rule of thumb , turn off enabled or linked with systemctl disable and reserve systemctl mask for static units
	units can declare relationships : Wanted by says if the system has a multi-user.target, that unit should depend on this one (the unit being read)

	Systemctl isolate 
To change systems operating mode
	activates Target and dependencies and deactivates all other units
		Init has telinit to change run lvls
			Run lvls are mapped to certain targets on systemd
				Ex. Multi-user is run lvl 2-4 ( cuz of options)
Systemd Dependencies knowledge is important to diagnose n fix dep problems
	Not all dependencies are explicit
		ex. Systemd knows which network port connection points a service will use, listens to requests without starting the service 
	Systemd assumes the normal behavior of most units kinds
		Ex. assumes the avg units are addons and shouldn’t run on early system initialization 
	explicit dependencies in the [unit] Section of unit files
		wants is pref
			Can extend this by creating a unit.wants dir in Systemd/system
Execution order
If one unit depends on another , the start order is still independent of this
	Parallelism 
	this is read from Systemd before state changes and sorted according to before/after clause of unit files
complex unit file example
	Forking service type
		means startup cmd is expected to terminate even if daemon keep running in background, PIDFile is recorded
	Exec are commands to be run under circumstances 
		Before service starts
		start the service
		How to read its config file
	Private temp
		Increase security out of the /tmp directory that’s shared by all users and processes 

Rule of thumb 
	Don’t edit unit files u didn’t create 
		Make a config did in system/unitfile.d
			and file called xxx.conf
				Override is standard name
					are read before unit file
		To remove existing entries, assign the option value as empty before adding your own, both inside your conf
			Systemctl restart unit.service to take effect 
		overrides can’t modify [install], for that add dependencies systemctl add-wants / requires
iptables-config won’t allow you to modify iptables rules (firewall), just provides way to load more modules like NAT
	FOR CONFIGURING IPTABLES SEE PAGE 440

Systemd logging
	Journald facility logs kernel, read with journalctl 

### ch 2.9 reboot and shutdown 
Don’t shutdown cloud services, halt or reboot

Halt or power off in vm?

### ch 2.10 strategy for a non booting system
Three basic approaches 
	Don’t debug 
		Restore to good state
			Most common for cloud
	Run shell and debug 
		like Single user mode, minimum prep to run shell , for network related stuff you need physical access so this is not used for cloud
	Boot a separate system image, mount sick systems fs and investigate
Single user mode
	They boot loader command interface run service or -s
		Running system can be brought to single by running telinit or systemctl 
	only root partition is mounted
		must mount other fs to access programs not living in root
	Fstab 
		 for available file systems 
		fdisk -l for systems local disk partitions
	Starts in read only 
		To write u must remount single user
			Mount -o rw,remount /
	With grub press e to edit boot options of kernel
	









## Ch 3 Access control and rootly powers
the mechanical details of how the kernel and its delegates make security-related decisions
	recently has become more modular with advent of kernel APIs
		still, the traditional system remains the standard for unix/linux

**man** **notes**:
* `telinit` changes *runlevel* on system (`init`) 
	* **runlevel**: system mode
		* obsolete, use `systemctl isolate` 
			* **systemd** maps runlevels onto *targets*
				* **target**: 
	* `runlevel` prints previous & current *runlevel*
### Ch 3.1 Standard UNIX access control
The **model** has remained unchallenged
	**Access** **control** depends on *user* or *group*
	**Objects** have *owners* with broad control over them
	**You** own your *objects*
	**su** "root" can act as owner of *any* object
	only **root** can perform sensitive admin operations
certain **syscalls** are *root* only
	`settimeofday` 
while others involve ownership and special root provisions.
	`kill` 
**filesystems** have their own access control systems
	implemented together with kernels VFS layer
		more likely to make use of *groups* for access control
**filesystem access control**
every file has an *owner* and a *group*
	owner can *specify* what the group owners can do with it
	kernel and fs track owners and groups as *numbers* (**UID**, user identification number)
		mapped to usernames in `etc/passwd` file
		**UID / GID** are only for human readability
**process ownership**
**owner** can send processes *signals* and *reduce* priority
**process** have multiple identities
	real, effective, saved **UID** 
		**real** for accounting, **effective** for permission access
			same number
		**saved** allow program to leave/enter privileged mode
			reduce risk of unintended misbehavior
	real, effective, saved **GID**
	filesystem **UID**
		file access permissions
		implementation detail of **NFS**, usually same number as *effective*
**root account**
super user
	**UID** 0
		allowed to perform *and* valid operation on *any* file or process
			obvious *caveat* like you cannot execute file without its execute bit
		you can change name or grant **UID** 0 to more users but it's not good for system security
	ex.
		process owned by root can change its **UID** and **GID**
		**login** is ran through root
			if usr/pw is correct, the login program changes its UID and GID to yours and starts up your shell or GUI environment
**setuid and setgid execution**
Traditionally, access control is complemented by an **identity substitution system** 
	implemented by kernel and filesystem together
		allows marked executable files to run with elevated permission (*root*)
	lets devs and admins set up *structured* ways for users to perform privileged operations
		When kernel runs executable files with *setuid* or *setgid*
			it changes *effective* **U**/**GID** from *user* to that of the *file* containing the program image
				thus user "promoted"
	Programs running **setuid** are prone to security issues
		minimize number of **setuid** programs
			never use such programs unless explicitly written with **setuid** in mind
		can be *disabled* on individual filesystems with `nosuid` option to `mount`
### Ch 3.2 Management of the root account
**root account login**
	Ubuntu forbids it by default
		it's a bad idea because:
			root logins *leave no record*
				hard to figure out *what* you did and *when* if you broke something some day (or *who* if more users have root account access)
			for these reasons, most systems allow root login to be disabled on *terminal*, *window* systems or across *network*, everywhere **except** system console
				suggested to use these features -> PAM on page 590 for guide	
**su: substitute user identity**
	*better way* is to use `su`
		root shell after pw prompt
		`su` doesn't record commands, but it creates log entry of *who* became root and *when*
		can be used to **substitute** identities other than root
			good for debugging in *specific environments* of users
				`su - username` + their password spawns shell in login mode
					helps to reproduce their login environment as closely as possible
						get in habit of using full pathname to `su` to avoid sneaky programs called **su**
		Largely **superseded** by `sudo`
**sudo: limited su**
takes as its argument a command line to be executed as *root* or other *restricted user*
	``/etc/sudoers`` *lists* people authorized to use `sudo` and the commands run on each host
		**sudoers** file designed so a *single* version can be used on *different* hosts
	if the command is permitted, `sudo` prompts the *user's* password and executes
		5 minute idle timer before password prompts again
`sudo` keeps log of 
	**commands**
		*hosts* on which they were run
		the *people* who ran them
		*directories* used
		*times* invoked
	recommend using `syslog` to forward log entries to *secure central host*
advantages of `sudo`
	Accountability (*logs*)
	Users can do chores *without* unlimited root privilege
	*Real* root pw can be known to 0,1,2 people 
	*faster* than `su`
	revoking privileges *without* having to change root pw
	*list* of users with root privileges maintained
	less chance of *unattended* root shell
	a *single* file can control access for an entire network
disadvantages of `sudo`
	breaching sudoers account is *equivalent* to breaching root account
		ensure good passwords
			regularly run password cracker to ensure
	logs are easily *subverted* with shell escapes from within allowed program 
			shell escape: allow user to run shell cmd without having to exit program first
				ex. cmd mode in vim
		or by `sudo sh`
			shows up in logs at least
	*Not safe* to define limited domains of autonomy or to place certain operations out of bounds
		don't attempt this, if you need this functionality see page 83 drop in access control systems
**environment management**
	`sudo` by default passes minimal environment to the commands it runs, addition can be whitelisted by adding them to **sudoers** files env_keep list
		if not listed, can be *explicity* preserved in ``sudo`` cmd line
	for *remote* configuration/execution that needs no password on `sudo`
		replace manually entered passwords with authentication through `ssh-agent`
			and forwarded SSH keys. 
				configured through PAM on the server `sudo` will run
					`pam_ssh_agent_auth` package for the *module*
			has its own security issues but better than no auth at all
**precedence** 
	Order of **sudoers** file is important
		if a user is covered by several lines, some requiring passwords others don't
			 `sudo` always obeys the *last* matching line
				in the example of page 75, the last has NOPASSWD
					if reversed order, she'd have to enter password for every command

**sudo without controlling terminal**
	unattended execution of `sudo`
		*!requiretty* option in **sudoers** file to turn off

**site-wide sudo configuration**
- One **master sudoers** file throughout *domain*
	- **Advantage**: centralized *permission* tracking. 
		- Example: If an *admin* leaves, just modify master file
	* Share **sudoers** via *UNIX groups*
		* If *user*, %wheel ALL = ALL doesn't reveal much
		* *Big scale* orgs:
			* Use system config management (Ch. 23)
		* *Small scale*: Use "pull" *script* via `cron`
			* Copy **sudoers** with `scp`
					* Validate with `visudo -c -f file` *before* install
	* `sudo` **hostname** matching
		* Can be subtle (if no domain present)
			* Use `fqdn` option in **sudoers** to normalize
		* Use naming scheme in the **cloud**
			* Or match by *IP* (requires VN features)

**Disabling the root account**
* set pw to `*`
* `passwd -l` "*locks*" account (Linux)
	* Either of these *disable* attempts to verify pw
* `sudo` & software that *don't require* root pw still runs
* **Pros**: Mainly convenient
* **Cons**: Needed to *rescue* on physical computers
* Locked by default (Ubuntu)
  
**System accounts other than root**
* *Pseudo-users & groups*
	* Typically low **UID** (<10)
	* A custom to `*` these passwords
		* Set shells to `/bin/false`
			* Protects other pw *exploits* (SSH key)
	* **Pro**: Safer than root (providing *resource* access)
		* Examples: `mysql`, **NFS** "nobody"

### Ch 3.3 Extensions to the standard access control model
* Current **status quo**:
	* Standard model
	* *Extensions* to it
		* Some became UNIX standards (e.g., **PAM**)
	* Kernel extensions (Implement alternative approaches)
  
**Drawbacks of standard model**
* *root* = single point of failure
	* All `setuid` programs are potential targets
* Bad *network* *security*
	* Unprivileged user + physical access -> change process ownership
* Group definition = *privileged*
* Embedded in *daemons* and *commands* code
	* Ex. `passwd`
	* Cannot redefine *system* without modifying *source*
		* *Error prone*
* Little/no *logging* support
	* Can see UNIX group, not user *permissions*

**PAM: pluggable authentication modules**
* Wrapper for **auth** libraries
	* "Middle man" validating admin defined *authentication* *methods* with programs (2FA)
* Not access control tech; **authentication** control
	* "Is this `user`?"

**Kerberos: network cryptographic authentication**
* Authentication *method*
	* Wraps in **PAM**
* Performs *entire network* authentication
	* You **ID** with Kerberos, not your machine
		* Gives you *crypto ID* for other services
		  
**Filesystem access control lists**
* f
* f
## Ch 4 Process control
A process represents a running program
	An abstraction through which *memory*, *processor time*, and *I/O resources* can be managed and monitored.
	Axiom of UNIX: have as much as possible running in processes rather than from kernel
### Ch 4.1 Components of a Process
Consists of
* **address space**
	* memory pages that kernel has marked for the process's use
		* consists of:
			* code and libraries that a process executes
			* the process's variables
			* its stacks
			* various extra info needed by kernel while process runs
		* its virtual address space is laid randomly in phys memory, tracked by kernels page tables (pages are units in which memory is managed)
* **set of data structures within kernel** with following info about each process:
	* the process address space map
	* status of process (sleeping, stopped, runnable...)
	* execution priority of process
	* info about the resources the process has used (CPU, memory...)
	* info about the files and network ports the process has opened
	* its signal mask (record of which signals are blocked)
	* owner of the process
A **Thread** is an execution context within a process, each proc have at least 1
* has its own stack and CPU context but operates within address space of process
* can run simultaneously on different cores
	* multithreaded apps like BIND or Apache benefit from this
		* lets them farm out requests to individual threads
**PID** - process ID number
* Kernel assigns unique ID to processes
* **system calls** & commands specify the PID when manipulating a process
	* A **system call** is a mechanism used by programs to request services from the operating system (OS)
**namespaces** 
	further restricts processes' ability to see and affect each other
	notably used in **containers**
		side effect: a process might appear with different PID depending on observer
**PPID** - parent **PID**
	in order to initiate a new process running a particular program you need two steps:
		 - existing process must clone itself to create a new process
		 - clone then exchange its program for a different one
	when cloned, the original clone is know as a **PID**, parent PID, and the copy is a "child"
	the **PPID attribute** = **PID** from the parent which it was cloned 
	good to trace for example unrecognized/misbehaving processes
**UID & EUID** - real and effective user ID
	A process **UID** is the number of person who created it, or a copy of it
	**EUID** determines resources and files a process has permission to access
		Most of the time these numbers are the same except programs that are **setuid**
			**setuid** - allows a user to execute a program with the permission of another user
	Why have both?
		to identify between *identity* and *permission*
		a **EUID** can be set and reset to enable or restrict the permissions it grants
	For *kernel usage* mainly, there's a **FSUID** that controls the determination of filesystem permissions
**GID** or **EGID** - real and effective group ID of a process
	largely vestigial, only significant when a process creates new files, depending on the filesystem permissions, new files might default to adopting the GID of the creating process
**Niceness** 
	A process' scheduling priority determines the CPU time it receives by the kernel
	**Niceness** is the value which the kernel sets and pays attention to, in order to determine how "nice" you are planning to be to other users in the system.
**Control Terminal** 
	associated with most nondaemon processes
	Antiquated term for the actual terminals used in the past, now meaning basically the terminal window where you run shell commands aka pseudo terminals

### Ch 4.2 The life cycle of a process
To create a new process, a copies itself with the **fork** system call, the new copy has a unique **PID**
	**Fork**'s unique property is returning two different values. 
		From a childs POV it returns zero
		parent receives PID of child
		both must examine the return value to figure out their role
After a fork, the child often use the **exec** family of routines to begin executing the new program
When a system boots the kernel automatically creates and installs several processes, notably **init** or **systemd**. All processes besides what the kernel creates are descendants from **init**. 

When a process is ready to die it calls `_exit` to notify the kernel, the parent is required to be notified with its child's exit code through `wait`.

If the parent dies before the child, the kernel notices no ``wait`` is coming, and `init` takes over as parent.

**Signals**
	process level interrupt requests, ~30 of them and can be used as follows:
		can be used to communicate among processes
		can be sent by terminal driver (ctrl-c)
		can be sent by admin (kill)
		can be sent by kernel (eg when process performs division by zero)
		can be sent by kernel to notify process of "interesting" condition like death of child process or data availability on I/O channels
	Programs can prevent signals by ignoring or blocking, which makes them queued for delivery by the kernel, but it'll only act when the signal is unblocked
	Processes catch and handle signals by running signal handler routines
	**Signals** every admin should know:
		1. HUP - hangup | Termination
		2. INT - interrupt | Termination
		3. QUIT - quit | Termination
		4. KILL - ... | Termination
		5. BUS - bus error | Termination
		6. SEGV - Segmentation fault | Termination
		7. TERM - software termination | Termination
		8. STOP - ... | stop
		9. TSTP - keyboard stop | stop
		10. CONT - continue after stop | Ignore
		11. WINCH - window changed | Ignore
		12. USR1 - user-defined #1 | Termination
		13. USR2 - ... #2 | Termination
	A kill signal without it's signal number (`kill PID` instead of `kill -9 PID`), doesn't guarantee termination, as it can be caught blocked or ignored. -9 guarantees kill as it cannot be caught. Only use if a polite request fails.
	`sudo killall httpd` kills all Apache server processes
	`sudo pkill -u ben` sends TERM signal to all processes running as user ben
**Processes and thread states**
	As processes can be suspended and returned to duty with **STOP** and **CONT**, the state of suspended and runnable applies to entire process including threads.
	Threads waiting for kernel to arrange disk blocks to processes' address space, the requesting thread is in a **sleep state** unable to execute, while other threads in the process can run.
	A **process** is reported as sleeping when **all threads** are asleep.
	A process with **uninterruptible sleep** state cannot be killed, so underlying issue must be fixed or reboot. **Usually involves** server problems on **NFS filesystem** mounted with the `hard` option.
	**Zombie processes** are ones that finished executing without parents to collect their status. To fix, find the PID and where they come from to collect.
	
### Ch 4.3 PS: Monitor processes
**ps** is the system administrators best tool for monitoring processes
	**ps** **aux** - info about all processes running in a system
		**a** shows all, **x** show processes even without terminal, **u** selects user oriented output format
		the *COMMAND* names in [brackets] are not commands but kernel threads scheduled to process
			Programs can modify the *COMMAND* info, so its not necessarily an accurate representation of the actual command line
	**ps** **lax** - gives "longer" output formats
		more efficient as it wont translate every UID to username, good in bogged down system
	To identify PID of a process you can run `ps aux | grep <process>` , `pidof <process>`  or `pgrep <process>`

### Ch 4.4 Interactive monitoring with top
while **ps** show you a snapshot, **top** is a real-time version of it updating every 1-2 seconds
	while running `top`, press 1 to see individual cores CPU usage
	root can run `top -q` to make it highest priority, useful to track process that brought system to its knees already

### Ch 4.5 Nice and renice: Influence scheduling priority
Niceness is a numerical hint to kernel at how a process stands in relation to other processes contending for CPU usage
	`nice` manages only CPU scheduling prio, for I/O prio use `ionice`
	Manually setting prio is unusual today
	High value = low prio, Low value = high prio
		range from -20 to +19
	child processes inherit niceness
	owner can increase but now lower niceness
		restricts low prio processes from bearing high prio children
		superuser can set niceness arbitrarily

### Ch 4.6 The /proc filesystem
`ps` and `top` read from the `/proc` filesystem, a pseudo fs that the kernel exposes information to about the systems state
	to read more obscure info you must read directly from `/proc` 
		you have to `cat` or `less` the contents to see what they have
			beware some files are binary data that can confuse terminal
		`/proc/1` is the directory with info about `init`

### Ch 4.7 Strace and truss: Trace signals and system calls
First step to figure out what a process does is guessing based on indirect data from the filesystem, logs, and tools like `ps`. Powerful debugging tool for Administrators
`strace` is used when the above is insufficient, used for lower level snooping. (`truss` is for FreeBSD)
	displays every system call a process makes and every signal it receives.
	you can attach `strace` to a process, snoop, then detach without disturbing it.
		`strace` can interrupt system calls, but its not always observed as of standard UNIX software hygiene
	Not only does it show the name of system calls, it decodes the arguments and show the result code the kernel returns
	System call output can reveal errors not reported by the process itself
		example: **filesystem** **permission** **errors** or **socket** **conflicts** are quite obvious in the output of `strace`, look for return error indications and nonzero values

### Ch 4.8 Runaway processes
**Runaway processes** soak up more CPU, disk, or network resources than they would lead you to expect.
	example: a process may attempt the same failing operation over and over, flooring the CPU.
		or it could also just be a greedy implementation with the resources
	This merits investigation by system admins as it may also interfere with other processes running.
	the *DATA* column in `top` is a more direct measure to check this, type `f` when `top` is running and select *DATA* with space bar.
		look for growth over time and absolute size.
	killing a misbehaving process loses the evidence available, so test it first with the live example

### Ch 4.9 Periodic processes
Periodic scripts executed without human intervention, usable for backups, database maintenance, or nightly batch jobs
	The `cron` daemon is a traditional tool for running predetermined scheduled commands. 
	The "crontabs" are the files containing the commands and are stored in `/var/spool/cron`, **at most** one per users
	`crontab` helps maintain efficiency as it notifies `cron` when the files have changed
		shouldn't edit crontab files directly, as changes might not get notified.
		Suggests fully qualified PATH or set environment variable on the top of the crontab
			PATH=/bin:/usr/bin 
			*Page 111* about **email** example from crontab, more info on *page 118*
			Make sure to `chmod +x` to make it executable
**Crontab** **management**

## Ch 10 Logging
Operational data from daemons, kernel, applications is stored on your disk, called **logging**.
**syslog** was the system that used to manage logs, fairly robust but limited.
**systemd** journal is a second attempt to make logging better, in time expected to overtake syslog
	**journalctl** is that easiest way to view logs with **systemd**
		**-f** for real time (kinda like **tail -f**)
**rsyslog** is an updated version o

## ch 11 drivers and kernel

### ch 11.3 devices and their drivers

Drivers accessed thru dev

Sysfs - virtual in memory filesystem by kernel to provide organized info about the devices, their configs, and state in the file system

Udevadm - queries device info, triggers events, controls udevd daemon, monitors udev and parent devices

sda is first device, sdb etc

Device rules are not changed in default rules.d, changes are made in local rules at etc/udev/rules.d

Rules are made up of match and assignment clauses, rules are applied when match clauses are fulfilled. Assignment clauses specify actions udevd should take, they both share similar formats

Most important assignment key is name, specifying how udevd should name a device

Mount attaches file system storage device into specified directory 

### ch 11.4 Linux kernel configuration 

Hooks - allows parameters in kernel to be modified, accessed through interface in the /proc filesystem aka procfs 

/proc/sys allows options of kernel in runtime, back door to kernel
* documentation/sysctl
Permanent changes through sysctl command

### ch 11.6 LKM
Learnable kernel modules lkm - allows a device driver or other kernel components to be linked or removed while kernel runs
* not 100% safe, risk kernel panic
* OS dependent 
Stored in /lib/modules/*version*
Version aka uname -r

Inspect modules with lsmod 

Modprobe semi automatic wrapper of insmod 
It understands dependencies , installation, options and removal procedures. Can be configured

### ch 11.7 booting 
Chapter goes over the boot messages 

### Ch 11.8 booting alt kernels in the cloud
Cloud services avoids boot loaders like GRUB or use their own 
Requires you to interact with clouds API or web console

Goes over how AWS works 

### ch 11.9 Kernel Errors
Linux has 4 kernel failures
Panic soft lockup hard lockup and oops
* soft lockup occurs when in kernel mode for more than 10 sec, configurable, it can prevent user level tasks from running
* hard lockup same as soft but processor interrupted go unserviced. Quickly detected unlike soft
	*  in both cases stack trace and cpu registers are dumped in console showing the function calls that caused the problems, usually…
	* Typically the system freezes, sometimes preferable to just panic and reboot as you can configure there into safe kernel
		* Configured with sysctl 
* oops - panic after any anomaly. Can lead to panic but don’t have to. If a process can be killed for example it will do that instead.
	* Viewable with dmseg command
		* you might not debug kernels but capturing this info is appreciated
		* Most valuable info at top
		* 1280 x 1024 is adequate to capture info
			* Modified in grub config or kernel command line from grub boot menu screen. Latter better for testing 


## ch 24 Virtualization 
Virtualization makes it possible to run multiple instances of OS concurrently on same physical hardware
It dynamically allocates memory, io among guests OS , virtual server appears as physical to users
Pros:
* more flexible servers
* Portable and can be managed programmatically
* More efficient use of hardware
* Underpins cloud computing and containers 

Hypervisors aka VM are examples of this

Full virtualization simulate entire pc, resource costly
Paravirtualization cooperates with VM for hardware, improves performance
Hardware-assisted virtualization - cpu and memory controller virtualized by hardware aka accelerated virtualization. Good performance and guest os don’t know it’s virtualized . Assumed baseline today 
Paravirtualized drivers 
Modern virtualization cpu reliant paravirtualized guest os drivers and some code in guest kernels
Optimal performance but low requirement on guest kernels 
Type 1 VM - runs directly on HW without supporting os 
Type 2 VM - user space applications running on top another general purpose os
Oracles vbox is type 2

Live migration - move between VMs running in different HW. The VM Copies changes form source to destination then migrates when identical

Virtual machine images - v servers are created from images aka templates of conf os that VM load and execute, can snapshot VM to create image, for backup. Images are portable cuz VMs presented HW are standardized.

Containerization - os level virtualization, doesn’t use VM. Instead uses kernel features to isolate processes from system. Each process container has private root fs and process namespace

Process Namespace partition processes with resources 

A container is a facade of an os. Common to use with a VM. Bin packing is running applications in containers on a VM as the VM SUBDIVIDES phys servers in to manageable chunks
## Ch 29 Performance Analysis
dd
### 29.3 Factors that affect performance
Only following have much affect:
	*CPU utilization*
	*Memory*
	*Storage* *I/O*
	*Network* *I/O*
Time spent waiting is the most basic measure of perf degradation
CPU resources are assumed the most important factor, but actually relatively unimportant
	*Disk* *Bandwidth* common perf bottleneck
		Mechanical hard disk slower vs SSD
		*Virtual Memory* can be directly related to this
			if phys memory demand too high it often result in memory pages written to disk to be reclaimed and reused for another purpose.
			Make sure you have enough physical memory!
	*Network Bandwidth* similar to disk, latency.
		susceptible to HW problems and overloaded servers
### 29.4 Stolen CPU cycles
Resource contention
CPU most commonly affected, 2 ways
	Hypervisor using CPU quota based on contracted CPU power., addressed by allocating more resources at hypervisor level.
	Physical HW oversubscribed, not enough CPU cycles available.
		on cloud, restart instance to reassign new phys HW
		on data center of your own, may require upgrading virtualization environment with more resources
On linux, visualizes stolen CPU with the *ST* metric in `Top, vmstat and mpstat`
	shows CPU being diverted by hypervisor

### 29.5 Analysis of performance problems
Use scientific method:
	*Formulate the question*
		be specific to a defined area, or state a tentative conclusion/recommendation you are considering
			Specific about technology, components involved, alternatives you consider, outcomes of interest
	*Gather and classify evidence*
		Conduct systematic search of documentation, issues, papers, forums etc.
	*Critically appraise the data*
		Review for relevance and critique the validity. Abstract key info and source quality.
	*Summarize the evidence bot narratively and graphically*
		Combine findings into narrative, if possible graphically.
	*Develop a conclusion statement*
		State conclusions (I.E. answers to question) concisely. Assign grade of overall strength and weakness of evidence that support it.

### 29.6 System performance checkup
Specific tools and areas of interest
**Taking stock of your equipment**
Start inquiry with inventory of phys and virtual hardware (CPU / memory resources)
	`/proc` filesystem to find overview of hardware your OS thinks you have
	`/proc/cpuinfo`
		contain one entry for each core
			*processor* identifies each core
			*physical id* values are unique per CPU socket
			*core id* unique per core within a CPU socket
	`/proc/meminfo`
	`/proc/diskstats`
	`dmidecode` dumps SMBIOS data (`-t type`)
	`ip a` IP and MAC info for each configured interface
**Analyzing CPU data**
CPU data to analyze:
	**overall utilization**
		identify systems on which CPU speed is a bottleneck
	**load averages**
		profile overall system performance
	**per-process CPU consumption**
		identify specific processes hogging resources
	*Obtained with* 
		`vmstat` (2 args: *seconds* to monitor for each line of output,  *number* of reports to print)
			ex: `vmstat 5 5`
				if no args it runs until interrupt
			General *rule of thumb*:
				System should spend ~50% non idle time in user space and 50% in system space. Overall idle should be nonzero
			high *cs* or *in* (context switch / interrupts) indicate misbehaving/configured HW device
		`mpstat` presents avg processor stats for each processor
			`-P` specifies processor (`-P ALL` shows all simultaneously)
			useful to *debug symmetric multiprocessing*
			not very useful for *one user workstations*, generally CPU is idle most of the time, then uses a lot for a short period (open browser)
		`uptime` checks load averages
			3 values are given: 1, 5, 15-minute averages
				the higher the load value, the more important the systems aggregate performance becomes
				A good metric to *track system baseline*. If you know the systems load avg normally, and it *doesn't change on a bad day*, its a hint to look elsewhere.
					load vg *above expected norm* suggest taking look at running processes
		`ps -aux` way to view CPU usage of each process.
			*Deferring the execution* of CPU hogs or *reducing their priority* makes CPU more available to other processes.
		`top` is an excellent alternative to `ps`, same info but *live*
			use judiciously, as refreshing its output too rapidly can be a CPU hog
**Understanding how the system manages memory**
Kernel manages pages (memory units ~4KiB)
	allocates *virtual pages* to processes as they request memory
		each page is *mapped to real storage* (RAM or "backing store" on disk)
	Kernel keeps track of *mapping* between real and made up virtual pages using a **page table** 
		Kernel can allocate as much memory as asked for by augmenting real RAM with *swap space* (disk area designated for **paging**).
			Kernel *shuffling* *pages* between RAM and swap as different pages are accessed is called **paging**
			Can tune into kernels "swappiness" parameter with `/proc/sys/vm/swappiness`
				don't modify, probably buy more ram if you want to modify this
**Analyzing memory usage**
Two numbers summarize memory usage:
	*# of active virtual memory*
		Total demand for memory
	*Current paging rage*
		suggests proportion of *that* memory that is actively used
	Your goal is to reduce activity or increase memory *until paging level is acceptable*
		`swapon -s` to determine amount of paging (swap) space in use
			reports in KiB
			**VM** = size of real memory + swap space used
**Analyzing disk I/O**
`iostat` to monitor disk performance, has optional args like `vmstat`
	First line is summary since *boot*
	*Cost of seeking* is the most important factor affecting mechanical disk drive performance.
	To maximize performance regardless of disk type, you should put filesystems that are used together on separate disks
		ex: Often worthwhile to segregate frequently accessed web server data and web server logs onto different disks.
			presumably because separate disks can handle read/write independently, which is preferable over switching between reading and writing on the same disk. You can access server data while writing to logs without affecting each other performance wise
		Especially important to *split up paging area* if possible as paging slows the system
	`lsof` lists open files and `fuser` shows processes using a filesystem.
		Helpful for *isolating* disk I/O performance issues
		Shows interaction with processes and filesystems, some may be unintended.
			ex: if an app is writing its log to the *same device* used for database logs, possible disk bottleneck may result.
**fio: testing storage subsystem performance**
(github.com/axboe/fio), 
**sar: collecting and reporting statistics over time**





![[Pasted image 20250106160943.png]]