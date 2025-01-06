# 2024-01-08
![[Pasted image 20250104120011.png]]
### Assess unusual behaviour
* Figure out if the highest load average number ever reaches *above* the *amount of cores* on the system CPU by running ``cat /proc/cpuinfo``. 
	* If there are *more* than 4 cores on the processor, the load averages are still in the *normal range* of the hardware.
	* If there are *less* or *equal* to 4 cores, the hardware should be upgraded as the output of 4.35 *exceeds* the CPU's *capacity*.
### What hardware to replace
* Assess the *bottleneck* and learn the reason for it. High load averages doesn't necessarily mean replace the CPU. Performance is affected by *CPU utilization*, *Memory*, *Storage I/O*, & *Network I/O*.
	* Run ``top`` and ``vmstat`` to figure out what causes the issue and upgrade hardware accordingly.
		* *High CPU utilization*: Replace the CPU.
		* *High swap usage*: Add more RAM. 
		* *High I/O wait time*: Replace storage.
		* *High latency / packet loss*: Upgrade network service or replace network card.

---
# 2024-06-05
![[Pasted image 20250104120026.png]]

* #Example In lab 2 we used ``nohup ./script.sh`` and ``./script.sh&`` 
	* ``nohup ./script.sh``
		* Ignores *HUP* signals. A *HUP* signal terminates processes *attached to a terminal*.
		* #### Use case
			* Running ``nohup`` is useful if you want to *keep the process running* even if the terminal is *closed* or the *user logs off*. This effectively makes the process run in the *background*.
	* ``./script.sh&``
		*  Runs the script in the *background*.
		* #### Use case
			* Useful if you want to *keep using the terminal* after running a script.
	* **Comparison**: ``&`` runs the process in the background *without* having to close the terminal first as with ``nohup``. If you want to log off with the script continuing to run, use ``nohup``. 

---
# 2024-08-27
![[Pasted image 20250104120043.png]]
* ### Purpose of nice / renice
	* The commands change a process' *niceness* number, which represents a numerical hint for the *kernel* about the process' *priority* for accessing the *CPU*.  
* ### Differences & examples
	* ``nice`` sets the *niceness* of a process when it starts, and ``renice`` changes it as a process is running.
		* #Example ``nice -n -20 /bin/task`` 
			* ``nice`` is necessary if you want to *start* the process with a specific priority. If you want to run something really important *asap* you'd give it a low nice value.
		* #Example ``sudo renice -3 <PID>``
			* ``renice`` is necessary if you want to change the priority *without* *terminating* and restarting the process, perhaps something important *relies* on this process running. 
* ### Limitations: 
	* To decrease the *niceness* of a process you need to be a *super user* (*sudo*), non-privileged users can only increase the *niceness*. A a new process inherits the priority of its parent. This is to *prevent* *low priority* processes from bearing *high priority* children. 
		* If possible this could lead to other processes *starving* as processes could *unfairly* occupy the *CPU*. This is therefore limited to privileged users.