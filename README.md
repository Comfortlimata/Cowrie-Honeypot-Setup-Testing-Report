# Cowrie-Honeypot-Setup-Testing-Report

Author: Comfort K Limata.
Date: 20-06-25
Environment: Kali Linux, Cowrie Honeypot

1. Introduction
This report outlines the steps taken to install, configure, and test the Cowrie SSH honeypot on a Kali Linux machine. Cowrie is an interactive honeypot designed to simulate an SSH (and Telnet) server, primarily used to monitor and log brute-force attacks and shell interaction by malicious users.

2. Environment Setup
Operating System: Kali Linux

User:Mrenter.

Software Used: Cowrie Honeypot

Python Version: Python 3.x

3. Installation Steps
Cloning the Cowrie Repository
bash
Copy
Edit
git clone https://github.com/cowrie/cowrie.git
cd cowrie
Setting Up Python Virtual Environment and Dependencies
bash
Copy
Edit
python3 -m venv cowrie-env
source cowrie-env/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
4. Starting Cowrie
From inside the cowrie directory, Cowrie was started with:

bash
Copy
Edit
bin/cowrie start
This command initiates the honeypot server, listening on port 2222 by default.

Cowrie logs all activity into var/log/cowrie.log.

5. Testing the Honeypot
Simulating an Attacker
A second terminal was used to simulate an attack:

bash
Copy
Edit
ssh root@localhost -p 2222
Multiple login attempts were tested using different usernames and passwords.

Common commands such as ls, whoami, and exit were executed to verify interaction.

Monitoring Logs
To view real-time activity:

bash
Copy
Edit
tail -f var/log/cowrie.log
All login attempts and commands executed were captured in the log, confirming Cowrie was functioning as expected.

6. Troubleshooting Notes
Issue: "Another twisted server is running"
Fix:

bash
Copy
Edit
ps aux | grep twisted
sudo kill <PID>
rm -f var/run/cowrie.pid
Issue: Missing log files
Fix: Ensure Cowrie was started correctly and log permissions were properly configured.

Issue: Permission problems using sudo
Fix: Confirm user privileges and correct password input.

7. Recommendations for Future Work
Configure Cowrie to start automatically on system boot.

Set up alert mechanisms (email or Telegram notifications) for login attempts or suspicious activity.

Forward logs to a centralized logging solution like the ELK Stack or Splunk.

Safely expose Cowrie to the internet (via a VPS or router port forwarding) for real-world data collection.

Regularly update Cowrie and review logs for continued monitoring and defense.

8. Conclusion
A functional SSH honeypot using Cowrie was successfully deployed on Kali Linux. This setup provides valuable insight into attacker behavior in a controlled, secure environment. The project serves as an educational and practical experience in honeypot deployment, cybersecurity monitoring, and incident analysis.

