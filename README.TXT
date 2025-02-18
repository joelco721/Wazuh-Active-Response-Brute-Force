🛡️ SIEM Wazuh - Brute Force Detection & Auto-Blocking

📌 Overview

This project sets up Wazuh SIEM to detect brute force SSH login attempts and automatically block the attacker's IP for 10 minutes after 5 failed login attempts.

Why?

Prevent unauthorized access attempts.

Automate threat response.

Gain hands-on experience with SIEM monitoring & active response.

🔧 Configuration

🛠️ Tools & Technologies Used

Wazuh SIEM – Open-source security monitoring

Linux (Ubuntu) – Host system for Wazuh Manager & Agent

Active Response (host-deny) – Automatic IP blocking for attackers

⚙️ Wazuh Active Response Configuration

Located in /var/ossec/etc/ossec.conf, this configuration ensures automatic IP blocking:

<active-response>
  <command>host-deny</command>
  <location>server</location>
  <rules_id>2502</rules_id>
  <timeout>600</timeout>
</active-response>

📌 Screenshot 1: Add a screenshot of your ossec.conf file showing this configuration.

![Screenshot 1 - Wazuh Configuration](https://raw.githubusercontent.com/your-username/your-repo/main/screenshot1.png)

🚀 How It Works

Wazuh monitors SSH logs (/var/log/auth.log) for multiple failed login attempts.

Rule 2502 triggers when 5 failed attempts are detected.

Wazuh adds the attacker's IP to /etc/hosts.deny, blocking further access for 10 minutes.

Logs are stored in Wazuh Alerts (/var/ossec/logs/alerts/alerts.json).

📌 Screenshot 2: Add a screenshot showing failed SSH login attempts in /var/log/auth.log.

![Screenshot 2 - Failed SSH Attempts](https://raw.githubusercontent.com/your-username/your-repo/main/screenshot2.png)

📷 Logs & Screenshots

🔍 Log Entry Example

When an attacker is detected, Wazuh logs it as follows:

{ "timestamp": "2025-02-18T00:26:23", "rule": "Brute Force Attack Detected", "src_ip": "192.168.1.100", "action": "Blocked via /etc/hosts.deny" }

📌 Screenshot 3: Add a screenshot of your Wazuh alerts log (alerts.json) showing the blocked IP entry.

![Screenshot 3 - Wazuh Alert Log](https://raw.githubusercontent.com/your-username/your-repo/main/screenshot3.png)

🖼️ Screenshot of Wazuh Alert

📌 Screenshot 4: Add a screenshot of your Wazuh web interface (if applicable) showing the brute force alert.

![Screenshot 4 - Wazuh Web UI Alert](https://raw.githubusercontent.com/your-username/your-repo/main/screenshot4.png)

🏗️ Installation & Setup

1️⃣ Install Wazuh

Follow the official Wazuh installation guide to set up Wazuh Manager & Agent.

2️⃣ Configure Active Response

Edit the /var/ossec/etc/ossec.conf file and add the Active Response configuration shown above.

3️⃣ Restart Wazuh

Apply the changes:

sudo systemctl restart wazuh-manager

4️⃣ Test Brute Force Detection

Simulate a brute force attack using Hydra or manual SSH attempts:

hydra -l root -P passwords.txt ssh://<target-ip>

After 5 failed attempts, Wazuh should block the attacking IP automatically.

📌 Screenshot 5: Add a screenshot of a test brute-force attack attempt.

![Screenshot 5 - Brute Force Test](https://raw.githubusercontent.com/your-username/your-repo/main/screenshot5.png)

🔍 Verification

🛠️ Check Blocked IPs

To confirm that the attacker is blocked, run:

cat /etc/hosts.deny

You should see the blocked IP address listed.

📌 Screenshot 6: Add a screenshot of /etc/hosts.deny showing the blocked IP.

![Screenshot 6 - Hosts Deny List](https://raw.githubusercontent.com/your-username/your-repo/main/screenshot6.png)

📄 Check Wazuh Logs

sudo cat /var/ossec/logs/alerts/alerts.json | grep "2502"

📌 Screenshot 7: Add a screenshot of the command output confirming the IP block.

![Screenshot 7 - Log Confirmation](https://raw.githubusercontent.com/your-username/your-repo/main/screenshot7.png)

🔄 Future Improvements

✅ Extend blocking time beyond 10 minutes✅ Integrate with Suricata or FirewallD for additional security✅ Enable email alerts when an attack is detected

🔗 References

Wazuh Documentation

OSSEC Active Response

💼 Author

👤 Your Name🔗 GitHub: your-username📧 Contact: your-email@example.com
