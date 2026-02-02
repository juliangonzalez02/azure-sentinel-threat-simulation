# Azure Sentinel Threat Simulation
This lab is a threat simulation that leverages Azure Sentinel to automate detection rules, alerts, and playbooks against common Tactics, Techniques, and Procedures (TTPs).

_Adapted from the following project: https://github.com/fizahmad/azure-sentinel-threat-lab_

## Tasks
* Onboard non-Azure Windows VM via **Azure Arc**
* Create custom detection rules via **KQL**
* Build automated alerts via **Logic Apps**
* Utilize the automated alerts to deploy **playbooks**
* Leverage **Kali Linux** to simulate adversarial behavior using common TTPs

## Ordered Lab Steps
1. Setup → Begin lab with setup/README.md to build the Azure environment and onboard non-Azure VM.
2. Parsers → Deploy KQL scripts from parsers/ to normalize Sysmon and PowerShell logs.
3. Detections → Import YAML files from detections/ into Sentinel as Scheduled analytic rules.
4. Automate → Build automated alerts and playbooks for Incident Response.
5. Simulation → Leverage attack-simulation/README.md commands to trigger Sentinel workflows.
6. Documentation → See findings in documentation/ to view logs from Log Analytics Workspace and Sentinel
