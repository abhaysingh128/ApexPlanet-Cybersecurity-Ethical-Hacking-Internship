System Hardening: Defense Implementation

Apply Security Patches (Conceptual)
The vsftpd exploit succeeded because the software was extremely outdated.
Action to Document: You would first perform a system update to refresh the package lists and then a full system upgrade.
sudo apt update
sudo apt upgrade
Action for vsftpd: Specifically, you would remove or upgrade the vulnerable service.
# To remove the vsftpd service (the ultimate fix for that specific exploit)
sudo apt remove vsftpd

Disable Unused Services
Reducing the attack surface is a critical security measure. The Nmap scan revealed many unnecessary services running (like Telnet, NFS, rlogin).
Action to Document: You would stop and disable services that are not strictly necessary for the system's function.
# Example: Disabling the insecure Telnet service
sudo update-rc.d telnetd disable
sudo /etc/init.d/openbsd-inetd restart

Configure Firewall to Block Malicious Traffic
This is the most crucial hands-on step for defense. You will configure the iptables firewall to prevent future unauthorized network access.
A. Set Deny-by-Default Policy (Most Secure)
Flush Existing Rules: Clear any existing firewall rules.
sudo iptables -F
sudo iptables -X
Set Default Policy to DROP: Set the default rule to drop all incoming packets that aren't explicitly allowed.
sudo iptables -P INPUT DROP

Allow Essential, Secured Services
Now, explicitly allow the few services the system must run (e.g., SSH and HTTP).
Allow Established Connections: Allow returning traffic for legitimate connections that have already been opened.

sudo iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT

Allow SSH (Port 22):
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

Allow HTTP (Port 80):
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
