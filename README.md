# 🛡️ Cloud-Based Wazuh SIEM with Automated SSH Attack Mitigation

## 📌 Project Overview

This project demonstrates the implementation of a Security Information and Event Management (SIEM) system using Wazuh on an AWS EC2 instance. The system detects SSH brute-force attacks and automatically blocks malicious IPs using firewall rules.

---

## ⚙️ Technologies Used

* AWS EC2 (Ubuntu 22.04)
* Wazuh SIEM
* Linux (Ubuntu)
* iptables (Firewall)
* SSH

![aws dash](screenshots/2.png)

---

## 🚀 Setup Process

### 1. Connect to EC2

```
chmod 400 wazuh-server.pem
ssh -i wazuh-server.pem ubuntu@YOUR_IP
```

---

### 2. Install Wazuh

```
sudo apt update && sudo apt upgrade -y
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a -i
```
![installing](screenshots/installing.png)

---

### ⚠️ Challenges & Fixes

#### ❌ Issue 1: Low RAM

* EC2 instance had only 1GB RAM
* Wazuh requires 4GB (recommended)

![error1](screenshots/fixing_error_1.png)

✅ Solution:

* Ignored requirement using `-i`
* Added 2GB swap memory

![error1](screenshots/fixed_error_1.png)

---

#### ❌ Issue 2: Disk Space

* Default 8GB storage was insufficient


✅ Solution:

* Increased volume to 20GB
* Resized partition using `growpart` and `resize2fs`

![volumeadd](screenshots/volume.png)
![done](screenshots/installed.png)
---

## 🔥 Attack Simulation

* Performed multiple failed SSH login attempts
* Wazuh detected brute-force behavior

![attack](screenshots/attack.png)
![attack](screenshots/ssh-log.png)
![attack](screenshots/rule.png)


---

## 🤖 Automated Response (SOAR)

```
<active-response>
  <command>firewall-drop</command>
  <location>local</location>
  <rules_id>5760</rules_id>
</active-response>
```
![ruleadd](screenshots/rules.png)
---

## 📊 Results

* Detected SSH brute-force attacks
* Triggered rule-based alerts
* Automatically blocked attacker IP using iptables

![ruleadd](screenshots/finalresult.png)

---

## 🧠 Key Learnings

* SIEM implementation and log analysis
* Cloud security using AWS EC2
* Automated incident response (SOAR)
* Troubleshooting real-world system issues

---

## 📌 Conclusion

Successfully built a cloud-based SIEM system capable of detecting and mitigating SSH brute-force attacks in real-time.

---
