# Intrusion-Detection-and-Prevention-System-using-Snort-and-Fail2ban
This project demonstrates the integration of Snort (a Network Intrusion Detection System) and Fail2Ban (a log-based Intrusion Prevention tool) for real-time detection and automated banning of malicious IP addresses in a simulated environment.


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


    
