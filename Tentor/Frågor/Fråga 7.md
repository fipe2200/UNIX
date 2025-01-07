# 2024-01-08
![[Pasted image 20250104115830.png]]

---
# 2024-06-05
![[Pasted image 20250104115842.png]]
### Why reverse?
* For the DNS system *to* *manage* DNS names (most significant info to the *right*: google.**com**) and IP addresses (most significant info to the *left*: **192**.161.1.15), the *IP* branch of the namespace is inverted by listing the octets backwards for *reverse* *DNS* *queries*.
	* #Example **10**.4.1.5 -> 5.1.4.**10**.in-addr.arpa
### If you have a limited amount of networks in a subnet
* You have to make a *pointer* *record* (in the reverse zone file) for *each* IP address the organization has.
* Each pointer *must* *match* a corresponding A record in the forward zone file (*mcduckcorp.db*).
	* #Example If you have say 5 ip's spanning 10.4.1.1->10.4.1.5
		* *1.1.4.10.in-addr.arpa* zone file must have a pointer for each of the 5 IP addresses in it.

---
# 2024-08-27
![[Pasted image 20250104115909.png]]

- **Stateful inspection firewalls** keeps track and monitors the state of active network connections while analyzing incoming traffic and looking for potential traffic and data risks. 
	- *Downsides*:
		They can be fooled into allowing a harmful connection to the network.
		An attacker could intercept a communication between two people to either spy on the traffic or make changes to it.