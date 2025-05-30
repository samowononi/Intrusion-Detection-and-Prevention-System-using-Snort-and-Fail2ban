# Intrusion Detection and Prevention System using Snort and Fail2ban



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


## **🔐 Fail2Ban Configuration**


**Step 1: Installation**

Fail2Ban was installed and enabled to start on boot.

![Screenshot 2025-03-26 183854](https://github.com/user-attachments/assets/483408b8-d030-499c-9a65-e2502a4dbd26)

Terminal output confirming Fail2Ban installation

![Screenshot 2025-04-10 130004](https://github.com/user-attachments/assets/aa584840-158a-453f-9d99-74ba23ecaecd)

Terminal output confirming Fail2Ban active status

##

**Step 2: SSH Brute-Force Protection**

Configured a jail in /etc/fail2ban/jail.local to monitor SSH and ban IPs after 3 failed login attempts.

![Screenshot 2025-04-10 131007](https://github.com/user-attachments/assets/02c6d00a-62db-45ae-ac6f-ef7d4d556dac)

SSH jail configuration in jail.local

##

Summary of Fail2ban Prevention capability

| Attack Type | Source	| Can Fail2Ban Block? |	How? |
|-------------|---------|---------------------|------|
| SSH Brute Force |	var/log/auth.log | Native | Already built-in |
| Port Scanning	| Snort | Yes | Parse Snort alerts |
| Ping Flood (ICMP) |	iptables / syslog |	Yes	| Log + custom jail |

This table highlights Fail2Ban’s flexibility in blocking different types of attacks by showing the log source, detection method, and whether native or custom configurations are required.

##

**Step 3: Preventing Port Scanning with Fail2Ban**

Snort’s preprocessor sfPortscan was enabled in snort.conf to detect scanning behavior such as SYN and NULL scans. Once detected, Fail2Ban reads Snort's alerts and bans the offending IP via iptables.


- **Snort Configuration**

Enabled sfPortscan in snort.conf.

![Screenshot 2025-04-19 135515](https://github.com/user-attachments/assets/220cb182-9be6-46db-b98e-b8183f9ce495)

Snort port scan detection configuration


- **Fail2Ban Jail Setup**

Created /etc/fail2ban/jail.d/snort-portscan.local to monitor Snort logs.

![Screenshot 2025-04-19 142712](https://github.com/user-attachments/assets/e4882862-3d05-4566-a438-34aee7aebc3c)

Fail2Ban jail for Snort port scanning alerts


- **Custom Filter**

Defined a matching rule in /etc/fail2ban/filter.d/snort-portscan.conf.

![Screenshot 2025-04-20 012226](https://github.com/user-attachments/assets/9e82bc7e-49da-4e3d-b4dd-7312af298577)

Custom Fail2Ban filter for Snort portscan alerts


- **Activation**
Restarted Fail2Ban and confirmed the jail was active.

![Screenshot 2025-04-20 014919](https://github.com/user-attachments/assets/17fcebe2-292f-4d0d-9bcd-b56e0a278f5a)

Fail2Ban active jail for port scanning

##


**Step 4: Blocking Ping Floods with Fail2Ban**

Since Fail2Ban can’t parse ICMP directly, iptables was configured to log excessive ping requests:

sudo iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/second -j LOG --log-prefix "PING FLOOD: "

- **Logging Setup**

Logged frequent ICMP echo-requests with a unique prefix.

![Screenshot 2025-04-20 024019](https://github.com/user-attachments/assets/0a17874c-3c30-443e-bd8b-50b366d75567)

ICMP flood logging rule using iptables

- **Fail2Ban Filter & Jail**

Created /etc/fail2ban/filter.d/ping-flood.conf to match the log prefix, and /etc/fail2ban/jail.d/ping-flood.conf for the jail config.
  
![Screenshot 2025-04-20 024232](https://github.com/user-attachments/assets/82aceac0-85aa-4b82-91c9-e6f7aa3f2062)

Fail2Ban filter for ping flood detection

![Screenshot 2025-04-20 024721](https://github.com/user-attachments/assets/11960446-4d58-4907-816d-43cac42e3585)

Fail2Ban jail for ping flood detection


- **Activation**

Reloaded Fail2Ban and verified the ping-flood jail is working.

![Screenshot 2025-04-20 032913](https://github.com/user-attachments/assets/2e551b70-344c-4d86-826e-ea4be3517f2e)

Ping flood jail status and bans in Fail2Ban


## **🔗 Snort & Fail2Ban Log Integration**

To unify detection and logging, Snort and Fail2Ban were integrated into a single pipeline with persistent service control.

**📁 Combined Log System**

A custom script (/usr/local/bin/combine_logs_script.sh) merges:

/var/log/snort/alert

/var/log/fail2ban.log

into a shared file: /var/log/snort_fail2ban.log.

![image](https://github.com/user-attachments/assets/6cfc46a2-c1a4-455f-b52e-2cffe1c79a49)


Each entry is tagged by source for easier parsing and analysis.

-Screenshot Caption: Combined log script merging Snort and Fail2Ban outputs.-

**🛠️ Systemd Service Setup**

A custom systemd service was created to auto-start Snort, Fail2Ban, and the log combiner at boot.

![Screenshot 2025-04-07 160442](https://github.com/user-attachments/assets/705a5b19-9049-4436-bf72-6b67aeee3506)

Terminal output confirming the custom IDPS service is enabled and running.













