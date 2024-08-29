<br />

<h1 align="center">☁️🔐 Azure Honeynet & SOC: Cyber Attacks in Real Time 🔐☁️</h1> 

<br />

![Cloud Honeynet / SOC](https://github.com/user-attachments/assets/ff20f83b-0270-445d-8fda-b7f235235de3)

 <br />
 
## Introduction

<br>

In this project I built a honeynet in **Microsoft Azure** to simulate real-world cyber attacks.

The main objective of this project was to showcase:
- optimal security measures
- effective incident response strategies
- the impact of fortifying our Azure environment

<br>

This was achieved by [Setting Up Virtual Machines in Azure](https://github.com/franciscovfonseca/Setting-Up-Vulnerable-VMs-in-Azure/blob/main/README.md) which were **Intentionally Vulnerable**, lacking safeguards against the public internet.

Subsequently, by incorporating log sources into a **Log Analytics Workspace**, I used **Microsoft Sentinel** to Generate Attack Maps, Trigger Alerts, and Create Incidents.

Overall, this project helped me to better understand the tactics and techniques used by cyber attackers, while showcasing my ability to respond quickly and effectively to any identified issues.

<br>

<br>

## Methodology

<details close> 
<summary> <h3> 1️⃣ Create the Honeynet</h3> </summary>

- I began by [Deploying 2 Vulnerable Virtual Machines](https://github.com/franciscovfonseca/Setting-Up-Vulnerable-VMs-in-Azure/blob/main/README.md) in Azure, simulating an Insecure Environment.

- I then [Disabled the Windows VM's Internal Firewall & Installed a SQL Server Database](https://github.com/franciscovfonseca/Disable-Windows-Firewall-Install-SQL-Server-and-Create-Vulnerabilities/blob/main/README.md) inside of it, in order to give bad actors a chance to Discover our VMs and Generate Logs.

- Finally I [Created a 3ʳᵈ Virtual Machine](https://github.com/franciscovfonseca/Disable-Windows-Firewall-Install-SQL-Server-and-Create-Vulnerabilities/blob/main/README.md) called ```attack-vm``` to Perform Actions against our Environment & Observe the Logs Generated from those Actions.

  </details>
  
<details close> 
<summary> <h3> 2️⃣ Logging & Monitoring</h3> </summary>

- I started by [Setting up Log Analytics Workspace](https://github.com/franciscovfonseca/Geo-IP-Data-Ingestion-and-Log-Analytics-and-Microsoft-Sentinel-SIEM-Setup/blob/main/README.md) as our Central Log Repository.

- I then [Enabled Microsoft Defender for Cloud](https://github.com/franciscovfonseca/Enable-Microsoft-Defender-for-Cloud/blob/main/README.md) to gives us a highlevel view of our Azure Environment in terms of Security and Secure Score.

- After that I [Configured the Logs from the Virtual Machines & NSGs](https://github.com/franciscovfonseca/Enable-Log-Collection-for-VMs-and-NSGs/edit/main/README.md) to be sent into our Log Analytics Workspace.

- The next step was to [Ingest the Logs from Microsoft Entra ID](https://github.com/franciscovfonseca/Microsoft-Entra-ID-Logging/blob/main/README.md) into our Log Analytics Workspace.

- In the next lab I continued Configuring Logging, in this case by [Bringing the Activity Logs](https://github.com/franciscovfonseca/Activity-Log-Subscription-Level/blob/main/README.md) into our LAW.

- And then finally I worked on [Enabling Logging for our Azure Storage Account & Key Vault](https://github.com/franciscovfonseca/Data-Plane-Logs-Resource-Level/blob/main/README.md)

  </details>

<details close> 
<summary> <h3> 3️⃣ Security Metrics Measurement</h3> </summary>

- I observed the environment for 24 hours, recording **Key Security Metrics** while it was insecure.

- This provided a baseline to compare against after **Implementing Remediation Measures**.

  </details>

### 4️⃣ <b>Incident Response and Remediation</b>

- After addressing the incidents and identifying vulnerabilities, I began the process of hardening the environment by applying **Security Best Practices and Azure-specific Recommendations**.

<br>

### 5️⃣ <b>Post-Remediation Analysis</b>

- I re-observed the environment for another 24 hours to measure security metrics again, **Comparing the Results** with the initial baseline.

<br>

<br>

## Technologies, Regulations, and Azure Components Employed

<br>

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

<br>

<br>

## Architecture BEFORE Implementing Hardening Measures and Security Controls

<br>
 
<p align="center">
<img src="https://github.com/franciscovfonseca/Azure-Honey-Net-SOC/assets/172988970/5cf1c278-756a-4bcb-a08f-271078a8bcba" height="70%" width="70%" alt="9"/><br />

 <br />

### Before Hardening Measures and Security Controls:

- In the "BEFORE" stage of the project, all resources were initially deployed with public exposure to the internet.

- This setup was intentionally insecure to attract potential cyber attackers and observe their tactics.
 
- The Virtual Machines had both their **Network Security Groups (NSGs)** and built-in **Firewalls** wide open, allowing unrestricted access from any source.

- Additionally, all other resources, such as **Storage Accounts** and **Databases**, were deployed with public endpoints visible to the internet, without utilizing any **Private Endpoints** for added security.

<br>
 
<br>

 
 

## Architecture AFTER Implementing Hardening Measures and Security Controls

<br>
 
<p align="center">
<img src="https://github.com/franciscovfonseca/Azure-Honey-Net-SOC/assets/172988970/5789d984-10bc-4ada-8dc7-763722ad9b67" height="70%" width="70%" alt="9"/><br />

 <br />

### For the "AFTER" stage, I implemented a series of hardening measures and security controls to improve the environment's overall security posture.

<br>

These improvements included:

<h4> ❶ Network Security Groups (NSGs)</h4>
 
 - I hardened the NSGs by blocking all inbound and outbound traffic, with the sole exception of my own public IP address.
 - This ensured that only authorized traffic from a trusted source was allowed to access the virtual machines.
 
<h4> ❷ Built-in Firewalls</h4>

- I configured the built-in firewalls on the virtual machines to restrict access and protect the resources from unauthorized connections.
- This step involved fine-tuning the firewall rules based on the specific requirements of each VM, thereby minimizing the potential attack surface.

<h4> ❸ Private Endpoints</h4>

- To enhance the security of other Azure resources, I replaced the public endpoints with Private Endpoints.
- This ensured that access to sensitive resources, such as storage accounts and databases, was limited to the virtual network and not exposed to the public internet.
- As a result, these resources were protected from unauthorized access and potential attacks.
<br />

<br>

<h3>✅ Result:</h3>
 
- By comparing the **Security Metrics** *Before* and *After* implementing these **Hardening Measures** and **Security Controls**, I was able to demonstrate the effectiveness of each step in improving the overall **Security Posture** of the **Azure Environment**.

<br>

<br>

## Attack Maps BEFORE Hardening Measures and Security Controls

<br>

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

<br>

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

<br />
<br />
<br />

 
## Metrics Before Hardening / Security Controls

<br>

The following table shows the metrics we measured in our insecure environment for 24 hours:
- Start Time: 2024-06-02 17:02:00 PM
- Stop Time: 2024-06-03 17:02:00 PM

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

<br>

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
- Start Time: 2024-06-18 15:37
- Stop Time:	2024-06-19 15:37


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

<br>

For effective management of high-priority incidents I:

1. Adhered to **NIST 800-61 (Revision 2) Guidelines**.<br />
2. Implemented Security Controls specified in **NIST SP 800-53 (Revision 5)**.

<br>

The approach involved:

- Initiating preparations by establishing a log analytics workspace, configuring Azure Sentinel, and setting up alerts for incident detection. The implementation of NIST SP 800-53 security controls ensured a robust and secure environment.

- When incidents occurred, I categorized and assessed their severity, conducting thorough investigations into logs to distinguish false from true positives. The incident response procedures outlined in NIST 800-61 (Revision 2) guided this process, evaluating the scope of impact.
 
- To streamline incident response, I employed an incident response playbook aligned with NIST 800-61 (Revision 2), documenting incident details comprehensively. Relevant security controls from NIST SP 800-53 (Revision 5) guided the execution of incident response activities.
  
- Post-resolution, meticulous documentation of findings, steps taken, and analyses performed was undertaken for each incident. Closure involved indicating the resolution and any necessary follow-up actions while ensuring compliance with NIST SP 800-53 (Revision 5) security controls.

<br />
<br />
 
 
## Conclusion

<br>

In this project, a small-scale honeynet was set up in **Microsoft Azure**, and log sources were integrated into a **Log Analytics Workspace**.
  
**Microsoft Sentine**l was utilized to generate alerts and incidents based on the processed logs.
  
Furthermore, metrics were assessed in the initially insecure environment, both before and after the implementation of security controls.
  
The substantial decrease in security events and incidents post the application of security measures underscores their efficacy in fortifying the environment.
<br />
<br />

  <details close> 
  
**<summary> 💡 Note</summary>**

It's important to note that if the network's resources were heavily utilized by regular users, there could have been a likelyhood of generating more security events and alerts in the 24-hour period following the implementation of security controls.

  </details>




<br />
<br />
<br />
<br />






