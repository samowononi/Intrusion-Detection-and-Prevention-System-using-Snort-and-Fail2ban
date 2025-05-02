# Intrusion-Detection-and-Prevention-System-using-Snort-and-Fail2ban



## **📖 Overview**
This project focused on building a lightweight intrusion detection and prevention system using Snort and Fail2Ban in a controlled virtual environment. Snort was configured to monitor network traffic for signature-based attacks, while Fail2Ban was set up to parse logs and automatically block malicious IP addresses. The two tools were integrated into a single logging workflow to provide a multi-layered defense mechanism against brute force, port scanning, and ICMP flood attacks. All simulated and tested using Kali Linux. The setup emulates how open-source tools can be combined to detect and mitigate network threats in real time.

---

## **🧠 Skills Learned**

  🛠️ Snort Configuration & Rule Writing
    Developed and tested custom Snort rules to detect ICMP, SSH, and port scan attacks.

  🔒 Fail2Ban Setup & Jail Configuration
    Created and managed multiple Fail2Ban jails, filters, and bans for different attack vectors.

  📜 Log Management and Parsing
    Merged and structured logs from multiple sources into a unified format for easier monitoring.

  💻 Linux System Administration
    Managed Ubuntu servers, IPTables rules, and automated services with systemd.

  🧪 Penetration Testing Basics
    Simulated real-world attacks (brute force, port scanning, and flooding) using Kali Linux tools like Nmap and hping3.

  🧰 Virtual Lab Deployment
    Set up and isolated multiple VMs on VirtualBox for secure, reproducible testing.

---

## **📦 Tools & Technologies**

● Snort 2.9.20 — Signature-based network traffic analyzer.

● Fail2Ban 1.0.2 — Host-based IP banning system.

● Ubuntu 22.04 LTS — Host OS for Snort and Fail2Ban.

● Kali Linux — Attack simulation machine.

● Metasploitable 2 & Windows 11 — Targets in attack scenarios.

● Oracle VirtualBox (v7.1.4) — Virtual lab environment.

---

## **🏗️ Lab Environment Setup**

All components were installed on virtual machines running in Oracle VirtualBox under a bridged network to simulate realistic conditions. The Ubuntu VM hosts both Snort and Fail2Ban, while Kali Linux is used to simulate attacks.

![Screenshot 2025-04-04 133351](https://github.com/user-attachments/assets/79a9b939-3c0f-41a9-9ae8-c40ff254aaba)

VirtualBox interface showing all configured VMs (Ubuntu, Kali, Metasploitable, Windows).

---

## **⚙️ Snort Configuration**

**Step 1: Installation**

Snort was installed on the Ubuntu Server virtual machine to function as a signature-based Intrusion Detection System.

![Screenshot 2025-03-25 170619](https://github.com/user-attachments/assets/225f362d-703d-4fdf-bd67-52cf4f6a865f)

Terminal showing Snort installation

##

After installation, the version of Snort was verified using the snort -V command (Alternative to --version). This confirmed the system was running Snort version 2.9.20, which aligned with the project’s compatibility requirements.


![Screenshot 2025-03-25 173407](https://github.com/user-attachments/assets/0340bdac-ea73-474f-b63f-8cdfad8e020d)

Terminal showing Snort version
    
##
Configuration continued with editing the /etc/snort/snort.conf file. The HOME_NET variable was set to reflect the IP range of the internal virtual environment (192.168.1.0/24).
##

**Step 2: Custom Snort Rules**

Custom rules were added to local.rules to detect malicious behavior such as ICMP floods, port scans and many more.

![Screenshot 2025-04-16 152243](https://github.com/user-attachments/assets/6927f18f-875f-4353-b771-3d8f8dde8de2)

Snort local.rules file with custom rule entries.

 ##

**Step 3: Validation**

The configuration was validated using sudo snort -T -c /etc/snort/snort.conf

![Screenshot 2025-03-25 175743](https://github.com/user-attachments/assets/2de2d2d6-80a8-4770-b2f9-6b6b37714ee1)

Snort output confirming successful configuration with no errors.

##

















