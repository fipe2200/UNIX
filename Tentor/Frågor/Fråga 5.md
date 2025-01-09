# 2024-01-08
![[Pasted image 20250104115642.png]]
### Infrastructure of syslog
* *Syslog* is a logging system and standard logging protocol for devices to record and send data.
* Was created to remove the need for programmers to *write* log files, and to give administrators *control* of logging.
	* *Flexible*, allows admins to *sort*, *route*, *examine* *attributes* of logs.
	* *Centralizes* network logging.
### How syslog works 
* *syslog* uses the *syslogd* daemon (now *rsyslogd*) to manage and store log messages from various *applications*, *services* and the *kernel* that are "*syslog aware*".
* #Example In lab 2 I ran ``tail -f var/log/syslog`` to monitor and make sure that ``cron`` was running properly when setting up a *cronjob*.
### What information can be found there?
* Log messages contain various detailed information such as *timestamps*, *hostname*, *facility*, *severity* *level*, *IP*, & *error messages*, which is useful to for example troubleshoot services that don't work as they should.
* #Example In lab 2, we used ``logger -p lpr.notice <message>`` to send a log message into the *syslog* *stream* using the facility *lpr* and severity level *notice*.
### where can the log files by default be found?
Log files can be found at */var/log/*

---
# 2024-06-05
![[Pasted image 20250104115656.png]]
### Resource records (RR)
* **NS** (name server) 
	* Identifies the *authoritative* *servers* for a zone and delegate *subdomains*.
* **A** (Address)
	* Maps hostnames to IP addresses
* **GLUE**
	* Consists of a *NS* record for the main domain and an *A* record for it.
	* A *glue* record is required to avoid circular referencing in a dependency structure.
		* #Example From lab 4: The name server *ns1.duckburg.cali.* depends on the parent *duckburg.cali.* , but the *DNS* *resolver* won't be able to resolve *duckburg.cali.* without knowing the IP address of *ns1.duckburg.cali.* , this causes a circular reference loop as it includes *duckburg.cali* in it. Unless a *glue* is provided in the parent zone stating the *IP address* of *ns1.duckburg.cali.* , this cannot be resolved.
* **MX** (Mail exchanger)
	* Routes mail more efficiently by *pre-empting* the destination of the sender to a hub (in most cases to the recipients host).
* **SPF** (Sender Policy Framework)
	* Specifies what *hosts* / *IP's* are allowed to send email *from your domain* (*anti-spoofing*/junk mail)
* **DKIM** (DomainKeys Identified Mail)
	* Ensures the email has not been tampered with while *in the process of delivery* by detecting email *spoofing*.
	* Uses a private key to add a *signature* in the header of email sent *from* *your domain*.
* **DS** (Delegation signer)
	* Links together the *parent* and *child* zones in *DNSSEC*.
	* Verifies the *DNSKEY* of the child to the *resolver*.
		* *Chain of trust*
* **PTR** (pointer)
	* Used in the reverse-zone file (``<inverse-ip of subnet>``.in-addr.arpa)
		* ``10.2.4.0 => 4.2.10.in-addr.arpa``
	* The reverse of an *A* record, pointing the IP address to the hostname.
* **Chain of trust**
	* *verification* *process* in **DNSSEC**
		* Public key of a child zone is *signed* by its parent zone
			* #Example We did this in our lab by signing our keys using ``dnssec-keygen`` & ``dnssec-signzone``, then two files *mcduckcorp.db.signed* and *dssec-mcduckcorp.duckburg.cali* were created. The *dssec* file contains the **DS** *RR* that must be placed / sent into the parent zone file (*duckburg.db*) to *verify* the *mcduckcorp* signature.
* **RRSIG**
	* Contain signatures of the other records in the zone


---
# 2024-08-27
![[Pasted image 20250104115710.png]]

[[Fråga 5#How syslog works]]
[[Fråga 5#Infrastructure of syslog]] 
* Includes *good* *qualities* 
### Problems
* No *authentication* features or *encryption*, so it's not very secure.
* Uses *UDP*, could mean a potential *data* *loss* in high latency environments.


# 2018-01-16
![[Pasted image 20250109134838.png]]
Samma som [[Fråga 6#2024-08-27]]
# 2018-03-21
![[Pasted image 20250109134900.png]]
Samma som [[Fråga 6#2024-01-08]]
# 2018-10-30
![[Pasted image 20250109134924.png]]
Samma som [[Fråga 7#2024-06-05]]