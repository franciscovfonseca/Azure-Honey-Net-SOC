# ☁️🔐 Azure Honeynet & SOC: Cyber Attacks in Real Time 🔐☁️
![Cloud Honeynet / SOC](https://github.com/franciscovfonseca/Azure-Honey-Net-SOC/assets/172988970/c9efb972-1bf8-4c33-a8d4-510a792a27b6)

 <br />
 
## Introduction

In this project I built a honeynet in **Microsoft Azure** to simulate real-world cyber attacks.

The main objective of this project was to showcase optimal security measures, effective incident response strategies, and the impact of fortifying our Azure environment. 

This was achieved by [setting up virtual machines in Azure that were intentionally vulnerable](https://github.com/franciscovfonseca/Setting-Up-Vulnerable-VMs-in-Azure/blob/main/README.md), lacking safeguards against the public internet.

This helped me to better understand the tactics and techniques used by cyber attackers, while also showcasing my ability to respond quickly and effectively to any identified issues.

 <br />


 
## Methodology

### 🟢 <b>*Creating the honeynet*</b>:

- I began by [deploying multiple vulnerable virtual machines](https://github.com/franciscovfonseca/Setting-Up-Vulnerable-VMs-in-Azure/blob/main/README.md) in Azure, simulating an insecure environment.

### 🟢 <b>*Monitoring and analysis*</b>:

- Azure was configured to ingest log sources from various resources into a log analytics workspace.
- Microsoft Sentinel was then used to build attack maps, trigger alerts, and create incidents based on the collected data.

### 🟢 <b>*Security metrics measurement*</b>:

- I observed the environment for 24 hours, recording key security metrics while it was insecure.
- This provided a baseline to compare against after implementing remediation measures.

### 🟢 <b>*Incident response and remediation*</b>:

- After addressing the incidents and identifying vulnerabilities, I began the process of hardening the environment by applying security best practices and Azure-specific recommendations.

### 🟢 <b>*Post-remediation analysis*</b>:

- I re-observed the environment for another 24 hours to measure security metrics again, comparing the results with the initial baseline.

 <br />

## Technologies, Regulations, and Azure Components Employed:

- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Virtual Machines (2x Windows, 1x Linux)
- Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Azure Key Vault for Secure Secrets Management
- Azure Storage Account for Data Storage
- Microsoft Sentinel for Security Information and Event Management (SIEM)
- Microsoft Defender for Cloud to Protect Cloud Resources
- Windows Remote Desktop for Remote Access
- Command Line Interface (CLI) for System Management
- PowerShell for Automation and Configuration Management
- [NIST SP 800-53 Revision 5](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final) for Security Controls
- [NIST SP 800-61 Revision 2](https://www.nist.gov/privacy-framework/nist-sp-800-61) for Incident Handling Guidance

 <br />






## Architecture BEFORE Implementing Hardening Measures and Security Controls
 <br />
 
<p align="center">
<img src="https://github.com/franciscovfonseca/Azure-Honey-Net-SOC/assets/172988970/5cf1c278-756a-4bcb-a08f-271078a8bcba" height="70%" width="70%" alt="9"/><br />

 <br />

<b>Before Hardening Measures and Security Controls:</b>

- In the "BEFORE" stage of the project, all resources were initially deployed with public exposure to the internet.

- This setup was intentionally insecure to attract potential cyber attackers and observe their tactics.
 
- The Virtual Machines had both their **Network Security Groups (NSGs)** and built-in **Firewalls** wide open, allowing unrestricted access from any source.

- Additionally, all other resources, such as **Storage Accounts** and **Databases**, were deployed with public endpoints visible to the internet, without utilizing any **Private Endpoints** for added security.

 <br />
 <br>

 
 

## Architecture AFTER Implementing Hardening Measures and Security Controls
 <br />
 
<p align="center">
<img src="https://github.com/franciscovfonseca/Azure-Honey-Net-SOC/assets/172988970/5789d984-10bc-4ada-8dc7-763722ad9b67" height="70%" width="70%" alt="9"/><br />

 <br />

<b>For the "AFTER" stage, I implemented a series of hardening measures and security controls to improve the environment's overall security posture. These improvements included:</b>

<h4>1️⃣ Network Security Groups (NSGs)</h4>
 
 - I hardened the NSGs by blocking all inbound and outbound traffic, with the sole exception of my own public IP address.
 - This ensured that only authorized traffic from a trusted source was allowed to access the virtual machines.
 
<h4>2️⃣ Built-in Firewalls</h4>

- I configured the built-in firewalls on the virtual machines to restrict access and protect the resources from unauthorized connections.
- This step involved fine-tuning the firewall rules based on the specific requirements of each VM, thereby minimizing the potential attack surface.

<h4>3️⃣ Private Endpoints</h4>

- To enhance the security of other Azure resources, I replaced the public endpoints with Private Endpoints.
- This ensured that access to sensitive resources, such as storage accounts and databases, was limited to the virtual network and not exposed to the public internet.
- As a result, these resources were protected from unauthorized access and potential attacks.
<br />

<h3>✅ Result:</h3>
 
- By comparing the **Security Metrics** *Before* and *After* implementing these **Hardening Measures** and **Security Controls**, I was able to demonstrate the effectiveness of each step in improving the overall **Security Posture** of the **Azure Environment**.
<br />

<br />



## Attack Maps BEFORE Hardening Measures and Security Controls
<br />

This attack map demonstrates the consequences of leaving the **Network Security Group (NSG)** open, as it allowed for malicious traffic to flow unimpeded.

This visualization underscores the importance of implementing proper security measures, such as **Restricting NSG Rules**, to Prevent Unauthorized Access and Minimize Potential Threats.

<br>

![NSG Allowed Inbound Malicious Flows](https://github.com/franciscovfonseca/Azure-Honey-Net-SOC/assets/172988970/49108ae2-03f1-4e14-ab9c-0d634631d949)<br>

 <br />
 <h2></h2>
 <br />
 
This attack map highlights the numerous **Syslog Authentication Failures** experienced by the **Linux Server** I deployed, indicating that unauthorized access attempts were made from outisde.

This serves as a reminder of the importance of securing Linux servers with **Strong Authentication Mechanisms** and **Monitoring System Logs** for signs of intrusion attempts.

<br>

![Linux Syslog Auth Failures](https://github.com/franciscovfonseca/Azure-Honey-Net-SOC/assets/172988970/71ba5813-06ac-43a4-942b-997d10f839a5)<br>

 <br />
 <h2></h2>
 <br />
 
This attack map showcases numerous **RDP and SMB Failures**, illustrating the persistent attempts by potential attackers to exploit these protocols.

The visualization emphasizes the need for **Securing Remote Access** and **File Sharing Services** to protect against unauthorized access and potential cyber threats.</b>
 
<br>

![Windows RDP/SMB Auth Failures](https://github.com/franciscovfonseca/Azure-Honey-Net-SOC/assets/172988970/7646c9c6-a01d-4905-ad87-97f8afaf202f)<br>
<br />

<br />


## Attack Maps AFTER Hardening Measures and Security Controls

 <br />

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

<br />
<br />
<br />

 
## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
- Start Time: 2024-02-02 17:02:00 PM
- Stop Time: 2024-02-03 17:02:00 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 21182
| Syslog (Linux VM)                   | 4877
| SecurityAlert (Microsoft Defender for Cloud            | 0
| SecurityIncident (Sentinel Incidents)        | 343
| NSG Inbound Malicious Flows Allowed | 969

<br />
<br />


## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
- Start Time: 2024-02-18 15:37
- Stop Time:	2024-02-19 15:37


| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 783
| Syslog (Linux VM)                   | 23
| SecurityAlert (Microsoft Defender for Cloud            | 0
| SecurityIncident (Sentinel Incidents)        | 0
| NSG Inbound Malicious Flows Allowed | 0

<br />
<br />
 
## Approach to Handling High-Priority Incidents with NIST Guidelines and Security Controls
For effective management of high-priority incidents I:

➡ **Adhered to NIST 800-61 (Revision 2) Guidelines**.<br />
➡ **Implemented Security Controls specified in NIST SP 800-53 (Revision 5)**.

The approach involved:

- Initiating preparations by establishing a log analytics workspace, configuring Azure Sentinel, and setting up alerts for incident detection. The implementation of NIST SP 800-53 security controls ensured a robust and secure environment.

- When incidents occurred, I categorized and assessed their severity, conducting thorough investigations into logs to distinguish false from true positives. The incident response procedures outlined in NIST 800-61 (Revision 2) guided this process, evaluating the scope of impact.
 
- To streamline incident response, I employed an incident response playbook aligned with NIST 800-61 (Revision 2), documenting incident details comprehensively. Relevant security controls from NIST SP 800-53 (Revision 5) guided the execution of incident response activities.
  
- Post-resolution, meticulous documentation of findings, steps taken, and analyses performed was undertaken for each incident. Closure involved indicating the resolution and any necessary follow-up actions while ensuring compliance with NIST SP 800-53 (Revision 5) security controls.

<br />
<br />
 
 
## Conclusion

🔹 In this project, a small-scale honeynet was set up in Microsoft Azure, and log sources were integrated into a Log Analytics workspace.
  
🔹 Microsoft Sentinel was utilized to generate alerts and incidents based on the processed logs.
  
🔹 Furthermore, metrics were assessed in the initially insecure environment, both before and after the implementation of security controls.
  
🔹 The substantial decrease in security events and incidents post the application of security measures underscores their efficacy in fortifying the environment.
<br />
<br />

It's important to note that if the network's resources were heavily utilized by regular users, there could have been a likelihood of generating more security events and alerts in the 24-hour period following the implementation of security controls.

<br />
<br />
<br />
<br />






