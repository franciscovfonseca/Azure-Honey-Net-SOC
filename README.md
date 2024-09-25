<br />

<h1 align="center">Building a SOC Environment in Azure with Live Traffic</h1> 

<br />

![Cloud Honeynet / SOC](https://github.com/user-attachments/assets/b6f385a6-3b8f-4eb2-a3f4-759adb34e7fc)
 
## Introduction

<br>

In this Project I built a Honeynet & SOC Environment in **Microsoft Azure**.

I used **Log Analytics** to Ingest Logs from various sources into our Environment, then leveraged **Microsoft Sentinel** to Build Attack Maps, Trigger Alerts & Create Incidents.

I also Enabled **Microsoft Defender for Cloud** as a Data Source for the Log Analytics Workspace and to assess the Virtual Machines' Configurations relative to *Regulatory Frameworks & Security Controls*.

Following that, I configured Log Collection on the Insecure Environment, set Security Metrics and then observed the Environment for 24 hours.

After Investigating the Incidents that Microsoft Sentinel generated during that period, I incorporated Security Controls to address the Incidents and Harden our Environment, based on recommendations from **Microsoft Defender (*NIST 800-53*)**.

<details close> 
<summary> For the Post-Remediation phase of this Project and after a second 24-hour Observation Period, these were the Security Metrics collected:</summary>

- ```SecurityEvent``` ➜ Windows Event Logs

- ```Syslog``` ➜ Linux Event Logs

- ```SecurityAlert``` ➜ Log Analytics Alerts Triggered

- ```SecurityIncident``` ➜ Incidents created by Sentinel

- ```AzureNetworkAnalytics_CL``` ➜  Malicious Flows allowed into our Honeynet

  </details>

<br>

<br>

## Methodology

<details close> 
<summary> <h3> 1️⃣ Create the Honeynet</h3> </summary>

- [Deploy 2 Vulnerable Virtual Machines](https://github.com/franciscovfonseca/Setting-Up-Vulnerable-VMs-in-Azure/blob/main/README.md) in Azure, simulating an Insecure Environment.

- [Disable the Windows VM's Internal Firewall & Installed a SQL Server Database](https://github.com/franciscovfonseca/Disable-Windows-Firewall-Install-SQL-Server-and-Create-Vulnerabilities/blob/main/README.md) inside of it, in order to give bad actors a chance to Discover our VMs and Generate Logs.

  </details>
  
<details close> 
<summary> <h3> 2️⃣ Logging & Monitoring</h3> </summary>

- [Set up Log Analytics Workspace](https://github.com/franciscovfonseca/Geo-IP-Data-Ingestion-and-Log-Analytics-and-Microsoft-Sentinel-SIEM-Setup/blob/main/README.md) as our Central Log Repository.

- [Enable Microsoft Defender for Cloud](https://github.com/franciscovfonseca/Enable-Microsoft-Defender-for-Cloud/blob/main/README.md) to gives us a highlevel view of our Azure Environment in terms of Security and Secure Score.

- [Configure the Logs from the Virtual Machines & NSGs](https://github.com/franciscovfonseca/Enable-Log-Collection-for-VMs-and-NSGs/blob/main/README.md) to be sent into our Log Analytics Workspace.

- [Ingest the Logs from Microsoft Entra ID](https://github.com/franciscovfonseca/Microsoft-Entra-ID-Logging/blob/main/README.md) into our Log Analytics Workspace.

- [Configure Logging by Bringing the Activity Logs](https://github.com/franciscovfonseca/Activity-Log-Subscription-Level/blob/main/README.md) into our LAW.

- [Enable Logging for our Azure Storage Account & Key Vault](https://github.com/franciscovfonseca/Data-Plane-Logs-Resource-Level/blob/main/README.md)

  </details>

<details close> 
<summary> <h3> 3️⃣ Security Metrics Measurement</h3> </summary>

- [Configure Microsoft Sentinel (SIEM)](https://github.com/franciscovfonseca/Microsoft-Sentinel-Configuration/blob/main/README.md) in order to Create 4 different Attack Maps ➜ which highlight where people from around the World are performing Malicious Actions to our Environment.

- [Expose our Insecure Environment to Malicious Traffic for 24 hours & Capture Analytics](https://github.com/franciscovfonseca/Run-Insecure-Environment-for-24-Hours-and-Capture-Analytics/blob/main/README.md) by taking a Snapshot of Multiple Security Logs & Key  Metrics recorded.

- This provided a baseline to compare against after **Implementing Remediation Measures**.

  </details>

<details close> 
<summary> <h3> 4️⃣ Incident Response & Remediation</h3> </summary>

- [Investigate & Work the Incidents](https://github.com/franciscovfonseca/Working-Incidents-and-Incident-Response/blob/main/README.md) being generated within Microsoft Sentinel ➜ in accordance with the **NIST 800-61 Incident Management Lifecycle**.

- After Addressing the Incidents & Identifying Vulnerabilities ➜ Harden the Cloud Environment by:

  - [Enabling Microsoft Defender for Cloud Regulatory Compliance for NIST 800-53](https://github.com/franciscovfonseca/Securing-SOC-Environment-Part-1/blob/main/README.md).

  - [Implementing Security Controls from NIST 800-53 Control SC-7 - Boundary Protection](https://github.com/franciscovfonseca/Secure-SOC-Environmentn-Part-2/blob/main/README.md).

  </details>

<details close> 
<summary> <h3> 5️⃣ Post-Remediation Analysis</h3> </summary>

- The Environment was Observed again for another 24 hours to Measure Security Metrics again ➜ **Comparing the Results** with the initial baseline.

  </details>
  
<br>

<br>

## Technologies, Azure Components & Regulations Employed

<br>

- **Azure Virtual Network** (VNet)
- **Azure Network Security Groups** (NSGs)
- **Virtual Machines** (2x Windows, 1x Linux)
- **Log Analytics Workspace** with **Kusto Query Language** (KQL) Queries
- **Azure Key Vault** for Secure Secrets Management
- **Azure Storage Account** for Data Storage
- **Microsoft Sentinel** for Security Information and Event Management (SIEM)
- **Microsoft Defender for Cloud** to Protect Cloud Resources
- **Windows Remote Desktop** for Remote Access
- **Command Line Interface** (CLI) for System Management
- [NIST SP 800-53 Revision 5](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final) for Security Controls
- [NIST SP 800-61 Revision 2](https://www.nist.gov/privacy-framework/nist-sp-800-61) for Incident Handling Guidance

<br>

<br>

## Architecture *BEFORE* Implementing Hardening Measures & Security Controls

<br>
 
<p align="center">
<img src="https://github.com/user-attachments/assets/6eaabee4-606d-41c8-923f-e9c13c63cf58" height="80%" width="80%" alt="9"/><br />

 <br />

<details close> 
<summary> <h3> 🚫 BEFORE Hardening Measures & Security Controls:</h3> </summary>

- In the *BEFORE* stage of this Project ➜ all resources were initially deployed with Public Exposure to the Internet.

- This setup was Intentionally Insecure to Attract Potential Cyber Attackers and Observe their Tactics.
 
- The Virtual Machines had both their **Network Security Groups (NSGs)** and built-in **Firewalls** wide open, allowing Unrestricted Access from any source.

- Additionally, all other resources, such as **Storage Account**, **Key Vault** and **Databases**, were deployed with Public Endpoints visible to the internet, without utilizing any **Private Endpoints** for Added Security.

  </details>

<br>
 
<br>

## Architecture *AFTER* Implementing Hardening Measures & Security Controls

<br>
 
<p align="center">
<img src="https://github.com/user-attachments/assets/e62f66a3-02ab-4d15-814e-1315cc76f8a6" height="80%" width="80%" alt="9"/><br />

<br>

<details close> 
<summary> <h3> 🔒 AFTER Hardening Measures & Security Controls:</h3> </summary>

<br>

For the *AFTER* stage of this Project ➜ I implemented a series of **Hardening Measures & Security Control**s.

Th goal was to Improve the Environment's Overall **Security Posture**.

These improvements included:

<details close> 
<summary> <h4> ❶ Network Security Groups (NSGs)</h4> </summary>
 
 - I hardened the NSGs by blocking all inbound and outbound traffic, with the sole exception of my own public IP address.
 - This ensured that only authorized traffic from a trusted source was allowed to access the virtual machines.

   </details>

<details close> 
<summary> <h4> ❷ Built-in Firewalls</h4> </summary>

- I configured the built-in firewalls on the virtual machines to restrict access and protect the resources from unauthorized connections.
- This step involved fine-tuning the firewall rules based on the specific requirements of each VM, thereby minimizing the potential attack surface.

   </details>

<details close> 
<summary> <h4> ❸ Private Endpoints</h4> </summary>

- To enhance the security of other Azure resources, I replaced the public endpoints with Private Endpoints.
- This ensured that access to sensitive resources, such as storage accounts and databases, was limited to the virtual network and not exposed to the public internet.
- As a result, these resources were protected from unauthorized access and potential attacks.

   </details>

  </details>

<h2></h2>

<br>

<h3>Result:</h3>
 
By comparing the **Security Metrics** *BEFORE* and *AFTER* implementing these **Hardening Measures & Security Controls**:

✅ I was able to demonstrate the Effectiveness of each step in improving the overall **Security Posture** of the **Azure Environment**.

<br>

<br>

## Attack Maps *BEFORE* Hardening Measures & Security Controls

<br>

### 🌍 NSG Allowed Malicious Inbound Flows

This attack map demonstrates the consequences of leaving the **Network Security Group (NSG)** open, as it allowed for Malicious Traffic to flow unimpeded.

This visualization underscores the importance of implementing proper Security Measures, such as **Restricting NSG Rules**, to Prevent Unauthorized Access and Minimize Potential Threats.

<br>

![NSG Allowed Inbound Malicious Flows](https://github.com/user-attachments/assets/b4921d87-02c4-4ddf-bf40-0a37b6d35192)<br>

<br>

<h2></h2>

<br>

### 🌍 Linux SSH Authentication Failures
 
This attack map highlights the numerous **Syslog Authentication Failures** experienced by the **Linux Server** I deployed, indicating that unauthorized access attempts were made from outisde.

This serves as a reminder of the importance of securing Linux servers with **Strong Authentication Mechanisms** and **Monitoring System Logs** for signs of intrusion attempts.

<br>

![Linux Syslog Auth Failures](https://github.com/user-attachments/assets/83911862-03bb-4f8c-8cdb-99fde9a86391)<br>

<br>

<h2></h2>

<br>

### 🌍 Windows RDP/SMB Authentication Failures
 
This Attack Map showcases numerous **RDP and SMB Failures**, illustrating the persistent attempts by potential attackers to exploit these protocols.

The visualization emphasizes the need for **Securing Remote Access** and **File Sharing Services** to protect against unauthorized access and potential cyber threats.</b>
 
<br>

![Windows RDP/SMB Auth Failures](https://github.com/user-attachments/assets/506e5e97-90a2-48c0-8f9d-748a0023cf47)<br>

<br>

<h2></h2>

<br>

### 🌍 MS SQL Server Authentication Failures
 
The Attack Map displayed below provides a Snapshot of **Attack Attempts** aimed at a Publicly **Exposed Microsoft SQL Server** over a 24-hour period.

The Map Highlights the Exact Location from which these **Attacks or Login Attempts** originated ➜ Australia

<br>

![Windows RDP/SMB Auth Failures](https://github.com/user-attachments/assets/753fdcb6-fca5-4039-a11d-408c47115557)<br>

<br>

## Attack Maps *AFTER* Hardening Measures & Security Controls

<br>

✅ ```All Map Queries actually returned No Results due to No Instances of Malicious Activitis for the 24 hour period after Hardening.```

<br>

<br>
 
## Metrics *BEFORE* Hardening Measures & Security Controls

<br>

The following table shows the Metrics we measured in our **Insecure Environment** for 24 hours:

| Metric                               |    Count    |
| ------------------------------------ |:-----------:|
| SecurityEvent (Windows VM)           |   19470     |
| Syslog (Linux VM)                    |   3028      |
| SecurityAlert (Microsoft Defender for Cloud) |    10       |
| SecurityIncident (Sentinel Incidents) |   348       |
| NSG Inbound Malicious Flows Allowed  |   843       |

<br />
<br />


## Metrics *AFTER* Hardening / Security Controls

<br>

The following table shows the Metrics we measured in our Environment for another 24 hours, but *AFTER* I applied **Security Controls**:

| Metric                               |    Count | Change Post-Hardening  |
| ------------------------------------ |:--------:|:----------------------:|
| SecurityEvent (Windows VM)           |   8778   |    **-54.92%**          |
| Syslog (Linux VM)                    |    25    |    **-99.17%**          |
| SecurityAlert (Microsoft Defender for Cloud) |    0     |    **-100.00%**         |
| SecurityIncident (Sentinel Incidents) |    0     |    **-100.00%**         |
| NSG Inbound Malicious Flows Allowed  |    0     |    **-100.00%**         |

<br>

<br>

<br>


<details close> 
<summary> <h2> 🎯 Approach to Handling High-Priority Incidents with NIST Guidelines & Security Controls</h2> </summary>

<br>

For Effective Management of High-Priority Incidents:

1. I adhered to [NIST SP 800-61 Revision 2](https://www.nist.gov/privacy-framework/nist-sp-800-61) Guidelines.
2. Implemented Security Controls specified in [NIST SP 800-53 Revision 5](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final).

<br>

**This Approach involved**:

<details close> 
<summary> <h4> Step 1️⃣</h4> </summary>
 
 - Initial Preparation ➜ Configuring a Log Analytics Workspace & Microsoft Sentinel.
 - Setting up Alerts for Incident Detection.
 - Implement NIST SP 800-53 Security Controls to ensure a Robust and Secure Environment.

</details>

<details close> 
<summary> <h4> Step 2️⃣</h4> </summary>
 
- When Incidents occurred, I Categorized and Assessed their Severity ➜ thoroughly investigating the different Logs to determine if the Incidents were False or True positives.
- My Incident Response Process was based on the NIST 800-61 guidelines.

</details>

<details close> 
<summary> <h4> Step 3️⃣</h4> </summary>
 
 - I also employed an Incident Response Playbook aligned with NIST 800-61 ➜ to document each Incident's details in a very comprehensive way.
 - The necessary Incident Response Activities were based on the Security Controls from NIST SP 800-53.

</details>

<details close> 
<summary> <h4> Step 4️⃣</h4> </summary>
 
 - For each Incident I documented all the post-resolution activities performed, what were the findings, the steps taken, and what my analyses was.
 - I Closed the Incident after highlighting what the resolution was and if there was any necessary follow-up actions required ➜ while ensuring Compliance with NIST SP 800-53 Security Controls.

</details>

   </details>

<br>

<br>

<br>
 
## Conclusion

<br>

In this project, I set up a Honeynet and SOC Environment in **Microsoft Azure**, and integrated several Log Sources into a **Log Analytics Workspace**.
  
I used **Microsoft Sentinel** to Generate Alerts and Incidents based on the ingested Logs.
  
Furthermore, I assessed the Security Metrics in a initially Insecure Environment, *BEFORE* Implementing of Security Controls, and then *AFTER* doing so.
  
The substantial decrease in Security Events and Incidents Post-Implementation of **Security Measures** showcases how important they were in **fortifying our Cloud Environment**.
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






