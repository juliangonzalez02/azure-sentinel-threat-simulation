# Connecting Windows VM to Sentinel
<br>

## Components

| Component | Purpose |
|---|---|
| Azure Arc | Onboards non-Azure machines into Azure environment |
| Data Collection Rule (DCR) | Defines which logs to collect |
| Azure Monitor Agent (AMA) | Forwards logs to Azure |
| Log Analytics Workspace | Centralized data collection from Azure and/or non-Azure resources, which Microsoft Sentinel processes for detection and investigation |
| Microsoft Sentinel | SIEM and SOAR solution for detection rules and investigations |

## Azure Arc

Azure Arc bridges non-Azure resources into the Azure Resource Manager control plane. This is essential for onboarding non-Azure VMs, on-premises servers, Kubernetes clusters, and databases.

Benefits:
- Enables cloud-native monitoring
- Applies Azure policies and extensions
- Integrates directly with Sentinel

## Azure Arc Agent Installation

**Portal:** Azure Arc > Infrastructure > Machines > Onboard/Create > Onboard Existing Machines > Generate script

Download and run the script on the Windows VM as Administrator.
<p align="center">
  <img width="700" height="450" alt="Arc Script Download"
       src="missing">
</p>
<p align="center"><em>Figure: Arc Script Download</em></p>

<p align="center">
  <img width="700" height="450" alt="Arc Agent Installing"
       src="missing">
</p>
<p align="center"><em>Figure: Arc Agent Installing</em></p>

<br>

After installation, the VM appears in Azure Arc: 

<br>

<p align="center">
  <img width="700" height="450" alt="VM in Azure Arc"
       src="missing">
</p>

<p align="center"><em>Figure: VM in Azure Arc</em></p>

## Configure the Data Connector

1. Go to **Microsoft Sentinel** > **Configuration** > **Data connectors**.
2. Select **Windows Security Events via AMA**.
3. Install the connector.
4. Click **Manage**.
5. Select **Windows Security Events via AMA**
6. Click **Open connector page**.

<p align="center">
  <img width="700" height="450" alt="Install the connector"
       src="missing">
</p>
<p align="center"><em>Figure: Install the connector</em></p>
<br>
<p align="center">
  <img width="700" height="450" alt="Open connector page"
       src="missing">
</p>
<p align="center"><em>Figure: Open connector page</em></p>

## Data Collection Rules

Two separate DCRs are required - one for Windows Security logs and another for Sysmon logs.

**Portal:** Sentinel > Data connectors > Windows Security Events via AMA > Open connector page

### DCR 1: Windows Security Events

#### Define Rule Details
1. Click **+ Create data collection rule**
2. Provide the following: 
   | Setting | Value |
   |---------|-------|
   | Rule Name | `WinSecurityEvents` |
   | Subscription | Select your subscription |
   | Resource Group | Select your lab resource group |

#### Add Target Machines
In the **Resources** tab, select the Windows VM to be monitored. 

#### Select Data to Collect
In the **Collect** tab:  
- Select **All Security Events**

Click **Review + create** to deploy the rule.

<p align="center">
  <img width="700" height="450" alt="WinSecurityEvents DCR"
       src="missing">
</p>
<p align="center"><em>Figure: WinSecurityEvents DCR</em></p>


### DCR 2: Sysmon Logs

#### Define Rule Details
1. Click **+ Create data collection rule**
2. Provide the following:
   | Setting | Value |
   |---------|-------|
   | Rule Name | `WinSysmonLogs` |
   | Subscription | Select your subscription |
   | Resource Group | Select your lab resource group |

#### Add Target Machines
In the **Resources** tab, select the Windows VM to be monitored.

#### Select Data to Collect
In the **Collect** tab:
- Select **Custom**
- Enter the following in the text box and click **Add**:

```
Microsoft-Windows-Sysmon/Operational!*
```
Click **Review + create** to deploy the rule.

<p align="center">
  <img width="700" height="450" alt="WinSysmonLogs DCR"
       src="missing">
</p>
<p align="center"><em>Figure: WinSysmonLogs DCR</em></p>

<br>

The Azure Monitor Agent installs automatically when the rule is applied.

<br>
<p align="center">
  <img width="700" height="450" alt="Create data collection rules"
       src="missing">
</p>
<p align="center"><em>Figure: Data Collection Rules (DCR)</em></p>


## Verify Log Ingestion

After 5-10 minutes, test log flow in Sentinel. 

**Portal:** Sentinel > Logs

```kql
SecurityEvent
| take 10
```

<p align="center">
  <img width="700" height="450" alt="Security Logs"
       src="missing">
</p>
<p align="center"><em>Figure: Security Logs</em></p>

<br>

```kql
SecurityEvent
| where Channel=="Microsoft-Windows-Sysmon/Operational"
```
<p align="center">
  <img width="700" height="450" alt="Sysmon Logs"
       src="missing">
</p>
<p align="center"><em>Figure: Sysmon Logs</em></p>

<br>

## Next Steps
The data connectors are now established and future compromised VM is sending logs to Sentinel. Next we must [parse](/parsers/parsers-setup.md) the logs into structured fields for easier querying and detection rule writing.

<br>

 **Reference Links:**
- https://www.techielass.com/azure-arc-windows-server-setup/
- https://jeffreyappel.nl/deploy-sysmon-and-collect-data-with-sentinel-and-the-ama-agent/
- https://github.com/fizahmad/azure-sentinel-threat-lab/blob/main/setup/sentinel_windows_onboarding.md
