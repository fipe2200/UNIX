
# 2024-01-08
![[Pasted image 20250104115140.png]]

What it is:
- **A container is an instance of an image,** 
	  The Docker image is a collection of files that constitute a tiny component of the operating system necessary to execute the Docker container as a standalone unit on any host.
	
- **A container is an enviorment for isolated processes, the container have its own filesystem** 
- **The container shares the host kernel**


How it works:


### Compared to a virtual machine:
* Both VM's and Containers look similar on the surface, they are portable, isolated execution environments with root filesystems.
	* **VM's** 
		* Has it's own OS kernel, ``init`` process, & drivers that interact with hardware.
		* More resource intensive.
		* Higher level of isolation.
	* **container** 
		* A facade/imitation of an operating system. It's packages an executable with its dependencies needed to run.
		* More lightweight & portable

Usage examples:

---
# 2024-06-05
![[Pasted image 20250104115333.png]]

---
# 2024-08-27
![[Pasted image 20250104115351.png]]