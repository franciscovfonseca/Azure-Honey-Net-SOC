# Azure Honeynet: Simulating Real-World Cyber Attacks
![Cloud Honeynet / SOC](https://imgur.com/4v9WYM7.png)

## Introduction

In this project I built a honeynet in Microsoft Azure to simulate real-world cyber attacks. 
The main objective of this project was to showcase optimal security measures, effective incident response strategies, and the impact of fortifying our Azure environment. 
This was achieved by [setting up virtual machines that were intentionally vulnerable](https://github.com/franciscovfonseca/Setting-Up-Vulnerable-VMs-in-Azure/blob/main/README.md), lacking safeguards against the public internet. This helped me to better understand the tactics and techniques used by cyber attackers, while also showcasing my ability to respond quickly and effectively to any identified issues.

## Methodology

- <b>*Creating the honeynet*</b>: I began by [deploying multiple vulnerable virtual machines](https://github.com/franciscovfonseca/Setting-Up-Vulnerable-VMs-in-Azure/blob/main/README.md) in Azure, simulating an insecure environment.

- <b>*Monitoring and analysis*</b>: Azure was configured to ingest log sources from various resources into a log analytics workspace. Microsoft Sentinel was then used to build attack maps, trigger alerts, and create incidents based on the collected data.

- <b>*Security metrics measurement*</b>: I observed the environment for 24 hours, recording key security metrics while it was insecure. This provided a baseline to compare against after implementing remediation measures.

- <b>*Incident response and remediation*</b>: After addressing the incidents and identifying vulnerabilities, I began the process of hardening the environment by applying security best practices and Azure-specific recommendations.

- <b>*Post-remediation analysis*</b>: I re-observed the environment for another 24 hours to measure security metrics again, comparing the results with the initial baseline.

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

## 




## Architecture Prior to Implementing Hardening Measures and Security Controls
![Architecture Diagram](https://i.imgur.com/1tLjWY9.png)

<b>Before Hardening Measures and Security Controls:</b>

- In the "BEFORE" stage of the project, all resources were initially deployed with public exposure to the internet. This setup was intentionally insecure to attract potential cyber attackers and observe their tactics. The Virtual Machines had both their Network Security Groups (NSGs) and built-in firewalls wide open, allowing unrestricted access from any source. Additionally, all other resources, such as storage accounts and databases, were deployed with public endpoints visible to the internet, without utilizing any Private Endpoints for added security.

## Architecture After Implementing Hardening Measures and Security Controls
![Architecture Diagram](https://i.imgur.com/ch1cAMU.png)
 <b>For the "AFTER" stage, I implemented a series of hardening measures and security controls to improve the environment's overall security posture. These improvements included:</b>

- <b>Network Security Groups (NSGs)</b>: I hardened the NSGs by blocking all inbound and outbound traffic, with the sole exception of my own public IP address. This ensured that only authorized traffic from a trusted source was allowed to access the virtual machines.

- <b>Built-in Firewalls</b>: I configured the built-in firewalls on the virtual machines to restrict access and protect the resources from unauthorized connections. This step involved fine-tuning the firewall rules based on the specific requirements of each VM, thereby minimizing the potential attack surface.

- <b>Private Endpoints</b>: To enhance the security of other Azure resources, I replaced the public endpoints with Private Endpoints. This ensured that access to sensitive resources, such as storage accounts and databases, was limited to the virtual network and not exposed to the public internet. As a result, these resources were protected from unauthorized access and potential attacks.

By comparing the security metrics before and after implementing these hardening measures and security controls, I was able to demonstrate the effectiveness of each step in improving the overall security posture of the Azure environment.
<br />

## Attack Maps Before Hardening / Security Controls
<br />


In the initial "BEFORE" metrics assessment, all resources were deployed with open exposure to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls configured with unrestricted access. Additionally, all other resources were deployed with public endpoints visible to the internet, without utilizing Private Endpoints.


 <br />
 <br />
 
- <b>This attack map demonstrates the consequences of leaving the Network Security Group (NSG) open, as it allowed for malicious traffic to flow unimpeded. This visualization underscores the importance of implementing proper security measures, such as restricting NSG rules, to prevent unauthorized access and minimize potential threats.</b>



![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/JeElX9R.png)<br>

 <br />
 <br />
 
- <b>This attack map highlights the numerous syslog authentication failures experienced by the Linux server I deployed, indicating that unauthorized access attempts were made from outisde. This serves as a reminder of the importance of securing Linux servers with strong authentication mechanisms and monitoring system logs for signs of intrusion attempts.</b>
 
 
![Linux Syslog Auth Failures](https://i.imgur.com/QW8PF0o.png)<br>

 <br />
 <br />
 
  - <b>This attack map showcases numerous RDP and SMB failures, illustrating the persistent attempts by potential attackers to exploit these protocols. The visualization emphasizes the need for securing remote access and file sharing services to protect against unauthorized access and potential cyber threats.</b>
 
![Windows RDP/SMB Auth Failures](https://i.imgur.com/SETmQBl.png)<br>

 <br />
 <br />

## Attack Maps After Hardening / Security Controls

> All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.

 <br />
 <br />
 
## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-05-02 17:02:00 PM
Stop Time 2023-05-03 17:02:00 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 21182
| Syslog (Linux VM)                   | 4877
| SecurityAlert (Microsoft Defender for Cloud            | 0
| SecurityIncident (Sentinel Incidents)        | 343
| NSG Inbound Malicious Flows Allowed | 969



## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37


| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 783
| Syslog (Linux VM)                   | 23
| SecurityAlert (Microsoft Defender for Cloud            | 0
| SecurityIncident (Sentinel Incidents)        | 0
| NSG Inbound Malicious Flows Allowed | 0

## Conclusion

In conclusion, I set up a compact, but effective honeynet using Microsoft Azure's robust cloud infrastructure. Microsoft Sentinel was then utilized to trigger alerts and generate incidents based on the logs ingested from the implemented watch lists. Baseline metrics were recorded in the unprotected environment before the implementation of any security controls. Following this, a range of security measures were enforced to fortify the network against potential threats. Upon implementation of these controls, another set of measurements was taken.

The comparison of pre- and post-implementation metrics demonstrated a significant reduction in security events and incidents, which highlights the effectiveness of the enforced security controls.
It's important to mention that if the network's resources were extensively engaged by regular users, it's plausible that a higher number of security events and alerts could have been produced within the 24-hour timeframe post-security control implementation.
