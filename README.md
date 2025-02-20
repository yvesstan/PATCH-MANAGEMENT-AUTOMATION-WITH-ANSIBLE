# PATCH-MANAGEMENT-AUTOMATION-WITH-ANSIBLE
Ansible playbook that automates security audits using Lynis on one or multiple Ubuntu hosts. The playbook scans for vulnerabilities and generates actionable remediation steps, which can then be automated using another playbook.

# Patch Management with Ansible

![Patch Management](https://img.shields.io/badge/Patch%20Management-Automation-blue)

## 📌 Introduction

In enterprise environments, vulnerability management typically follows this workflow:
- A vulnerability scanner (Tenable, Qualys, Rapid7, OpenVAS) performs scans on infrastructure.
- The results are collected in an Excel format (usually a template proposed by the CISO) where findings are organized by severity level, CVSS score, plugin, and other relevant factors.
- Prioritization is then carried out from critical to less critical vulnerabilities, enabling teams to apply patches accordingly using tools like Microsoft WSUS or other enterprise-level solutions.

To streamline this process, I developed an **Ansible playbook** that automates security audits using Lynis on one or multiple Ubuntu hosts. The playbook scans for vulnerabilities and generates actionable remediation steps, which can then be automated using another playbook.

---

## 🛠 Step 1: Security Audit Scan Playbook

The first step involves creating an **Ansible playbook** to automate **CVE discovery** on a Linux system using the **Lynis tool**. This playbook is designed for enterprise environments, ensuring professionalism and efficiency.

### 📜 Playbook: `vul_scan_automation.yml`

### 🔄 Workflow:
1. **Update the package list**: Ensures all repositories and packages are up to date.
2. **Install required packages**: Installs Lynis and other necessary tools for CVE scanning.
3. **Run CVE scan using Lynis**: Executes a system scan with Lynis and captures the results.
4. **Save CVE scan results to a file**: Logs scan results for later review.
5. **Notify the administrator**: Sends an email notification with scan completion details and log file location *(not yet implemented)*.
6. **Clean up unused packages**: Removes unnecessary packages and dependencies.
7. **Reboot the system if required**: Applies updates and reboots the system if necessary.

This playbook ensures automated CVE discovery and logs results for administrators to review.

### 📂 Log File Location
In my setup, scan results are stored at:
```
/home/master/lynis_cve_scan.log
```
on both the Ansible master and slave nodes.

---

## 📊 Viewing Scan Results

To review the CVE scan results, you can use various methods:

### 🔍 Terminal Commands:
- **Using `cat`**: 
  ```sh
  cat /home/master/lynis_cve_scan.log
  ```
- **Using `less`**:
  ```sh
  less /home/master/lynis_cve_scan.log
  ```
  (Use arrow keys to navigate, press `q` to quit.)
- **Using a text editor**:
  ```sh
  nano /home/master/lynis_cve_scan.log
  ```
  or
  ```sh
  vim /home/master/lynis_cve_scan.log
  ```

### 🌐 Remote Access:
- **Using `scp` to transfer the file to your local machine**:
  ```sh
  scp user@remote_host:/home/master/lynis_cve_scan.log /path/to/local/directory
  ```

- **Viewing in a web browser**:
  ```sh
  sudo mv /home/master/lynis_cve_scan.log /var/www/html/
  ```
  Then access: `http://your_server_ip/lynis_cve_scan.log`

### 🖥 Converting Scan Results to HTML
If you prefer an HTML format, install `aha` (ANSI-to-HTML converter):
```sh
sudo apt-get install aha
```
Convert the scan results:
```sh
cat /home/master/lynis_cve_scan.log | aha > /home/master/lynis_cve_scan.html
```

---

## 🛠 Step 2: Automating Security Remediation

Once vulnerabilities are identified, we can automate the remediation process by writing another playbook.

### 📜 Playbook: `automatelynis.yml`
Check the contents of this file in the repository for the remediation steps implemented.

### ⚠️ Possible Errors & Fixes
If you encounter an error in the task **`Install OSSEC`**, you will find a separate playbook named **`ossec.yml`** that resolves this issue.

---

## 🎯 Conclusion
This project demonstrates how **Ansible** can be leveraged to **automate security audits and vulnerability remediation** in an enterprise environment. By integrating these playbooks into your security workflow, you can enhance **efficiency, consistency, and response time** in patch management.

Feel free to **contribute, suggest improvements, or reach out** for discussions! 🚀

---

## 📌 Connect with Me
[![GitHub](https://img.shields.io/badge/GitHub-Profile-black?logo=github)](https://github.com/yourusername) [![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://linkedin.com/in/yourprofile)

---

**Happy SecOps!** 🎯🚀


