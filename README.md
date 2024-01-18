# Building a SOC + Honeynet in Azure (Live Traffic)
![Neon Blue Glitch Youtube Thumbnail - 1](https://github.com/TriandosM/Azure-SOC/assets/141364341/f83809f1-049f-437a-947d-cdaa94ee4eb4)


## Introduction

In this project, I constructed a mini honeynet within Azure and integrated log sources from diverse resources into a Log Analytics workspace. Microsoft Sentinel utilized this workspace to generate attack maps, trigger alerts, and create incidents. I conducted security metric measurements in the insecure environment for a 24 hour period, implemented security controls to fortify the environment, conducted metric assessments for another 24 hours, and present the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Neon Blue Glitch Youtube Thumbnail - 2](https://github.com/TriandosM/Azure-SOC/assets/141364341/58842968-ea2f-4509-97c4-7556aa780b0d)

## Architecture After Hardening / Security Controls
![Neon Blue Glitch Youtube Thumbnail - 3](https://github.com/TriandosM/Azure-SOC/assets/141364341/d33c59a2-2e37-42de-9545-6a4250370eef)


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

In the initial "BEFORE" metrics, all resources were initially deployed and exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls set to allow all traffic, and all other resources were deployed with public endpoints visible to the Internet, meaning there was no utilization of Private Endpoints.

In the subsequent "AFTER" metrics, Network Security Groups were strengthened by blocking ALL traffic, except for access from my admin workstation. Additionally, all other resources were safeguarded by their built-in firewalls and Private Endpoints.

## Attack Maps Before Hardening / Security Controls
<img width="1089" alt="(Before)nsg-malicious-allowed-in" src="https://github.com/TriandosM/Azure-SOC/assets/141364341/df276dcd-08cf-4a05-b322-db4e28babc27">
<br>
<img width="1115" alt="(Before)syslog-ssh-auth-fail" src="https://github.com/TriandosM/Azure-SOC/assets/141364341/754e33ba-a6d0-4cd5-b4ee-c64c5d7fe4c9">
<br>
<img width="1147" alt="(Before)windows-rdp-smb-auth-fai" src="https://github.com/TriandosM/Azure-SOC/assets/141364341/f787e68f-fa05-4afe-9f40-9e9b084539dd">
<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-08-21 05:13:34 
Stop Time 2023-08-22 13:13:34

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 92032
| Syslog                   | 2147
| SecurityAlert            | 5
| SecurityIncident         | 284
| AzureNetworkAnalytics_CL | 3198

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-08-23 19:54:58
Stop Time	2023-08-24 19:54:58

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 9287
| Syslog                   | 50
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet using Microsoft Azure, integrating log sources into a Log Analytics workspace. The deployment of Microsoft Sentinel enabled the triggering of alerts and the creation of incidents based on the received logs. We conducted metric assessments in the insecure environment both before and after implementing security controls. It is significant to highlight that the implementation of security measures resulted in a significant reduction in the number of security events and incidents, showcasing their effectiveness.

It's important to mention that if regular users heavily utilized network resources, there might have been a higher likelihood of generating more security events and alerts in the 24-hour period following the implementation of security controls.
