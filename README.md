# LAB-4-Active-Reconnaissance

**Name:** NUR NAJIHAH ABHAR
**Class:** L01-B04

## Part 1: Lab Setup
*   **Attacker VM:** Kali Linux running in VirtualBox
*   **Network Adapter Mode:** NAT
*   **Target Setup:** DVWA (Damn Vulnerable Web Application) running as a Docker container inside the Kali VM.
*   **Assigned CIDR:** The Docker bridge network uses `172.17.0.0/16`.

## Part 2: Own Host & Discovered Hosts
*   **Attacker IP (Kali eth0):** `10.0.2.15` *(update this with your actual IP from `ip -br addr`)*
  
  <img width="560" height="292" alt="Screenshot 2026-11-19 134118" src="https://github.com/user-attachments/assets/0c0d45da-afab-4438-b8c2-2cd266adca5b" />


*   **Target IP (DVWA Docker Container):** `172.17.0.2` *(update this with your actual IP from `docker inspect`)*

<img width="507" height="180" alt="Screenshot 2026-11-19 135049" src="https://github.com/user-attachments/assets/2e6abaa2-2113-4302-835a-07d7a5126060" />



**Evidence - Attacker IP & Route:**

<img width="513" height="122" alt="Screenshot 2026-11-19 134158" src="https://github.com/user-attachments/assets/636f4d75-4ff9-4a5a-9566-fc82caf222f6" />


**Evidence - Target Discovery:**

<img width="505" height="188" alt="Screenshot 2026-11-19 134627" src="https://github.com/user-attachments/assets/f8741eac-439f-42e6-9dc0-0dddfcd59237" />


## Part 3: Services & Interpretation
**Nmap Service Scan Results:**
*   **Port 80/TCP:** Open, HTTP (Apache httpd 2.4.x)
*   **Port 443/TCP:** Closed/Filtered
**Evidence - Nmap Scan:**
<img width="503" height="106" alt="Screenshot 2026-11-19 134444" src="https://github.com/user-attachments/assets/e1db8986-046d-4c9e-b448-7b27d8548188" />
**Interpretation:**
The Nmap scan reveals that port 80 is open and running an Apache web server. The version detection (`-sV`) suggests Apache 2.4.x is running. This indicates a web application is hosted on the target. While the version is visible, this does not confirm the presence of a specific CVE without further validation. 

## Part 4: Limitations / Risks
*   **False Negatives:** Host discovery (`-sn`) may yield false negatives if ICMP is blocked, though local Docker networks usually respond.
*   **Service Detection Limits:** Nmap's `-sV` relies on service banners. A banner may be spoofed or outdated, meaning we cannot guarantee the exact software version is accurate just from this scan.
*   **Filtered Ports:** If any ports returned as "filtered", we cannot confirm whether a service is actually listening behind them.
*   **Scope Limitation:** The scan was strictly limited to the local Docker bridge network inside the VM; no public IPs were scanned. No exploitation or brute-forcing was attempted.
