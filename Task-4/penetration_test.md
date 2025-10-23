Reconnaissance (Information Gathering)
This phase is about gathering initial information without actively probing the system, though in practice (as in your Task 2), it transitions quickly to active measures.

Activity	Focus	Documentation
Target Identification	Confirming the scope of the assessment.	State the target: Metasploitable2 VM with IP address 192.168.56.4
System Check	Determining if the target is live.	Document using the ping command to confirm the host is reachable on the Host-Only network.
Passive Info	Gathering general OS knowledge.	Note that the system is running a Linux operating system (confirmed later by OS fingerprinting).

Scanning (Discovering the Attack Surface)
This phase actively maps the network and host to discover vulnerabilities.

Activity	Focus	Tools Used	Documentation
Port & Service Scan	Finding open ports and software versions.	Nmap (-sS -sV -O flags)	Document the Nmap output (from Task 2): List the open ports (21, 22, 23, 80, etc.), services, and the crucial vulnerable version: vsftpd 2.3.4.
Vulnerability Scan	Automated search for known weaknesses.	Nessus Essentials (or OpenVAS)	Document the finding of the vsftpd 2.3.4 Backdoor vulnerability, noting its Critical severity.
OS Fingerprinting	Determining the Operating System.	Nmap (-O flag)	Confirm the OS is Linux 2.6.x, which is necessary for selecting the correct exploits.

Exploitation (Gaining Access)
This phase involves leveraging a discovered vulnerability to gain unauthorized access to the system.

Activity	Focus	Tools Used	Documentation
Vulnerability Selection	Choosing the most reliable exploit.	Research (Based on Nmap)	Select the vsftpd 2.3.4 Backdoor.
Exploit Configuration	Setting up the payload and target.	Metasploit Framework	Document the exact steps: use exploit/unix/ftp/vsftpd_234_backdoor, set RHOSTS 192.168.56.4, and set PAYLOAD cmd/unix/interact.
Execution and Shell	Running the exploit and connecting.	Netcat (nc)	Document the successful connection (nc -nv [IP] 6200). Include a screenshot showing the successful execution sequence.

Post-Exploitation (Proving Impact and Maintaining Access)
This phase is about demonstrating the severity of the compromise and gathering intelligence.

Activity	Focus	Commands Used	Documentation
Proof of Root Access	Establishing the highest privilege.	whoami	Critical: Must show the command returning root.
System Enumeration	Mapping the compromised system.	uname -a (Kernel) and netstat -tuln (Internal ports).	Document the system details gathered from these commands.
Credential Harvesting	Stealing sensitive user data.	cat /etc/shadow	Crucial: Document the extraction of password hashes (needed for the John the Ripper task). Include a screenshot showing the shadow file content.
Password Cracking	Proving the hashes are usable.	John the Ripper	Document the tool usage and the successful cracking of the weak msfadmin password.