# Azure Sentinel Threat Simulation
This lab is a threat simulation that leverages Azure Sentinel to automate detection rules, alerts, and playbooks against common Tactics, Techniques, and Procedures (TTPs). We will onboard a Windows 10 VM onto a sandbox Azure environment through Azure Arc, assume the Windows VM has been compromised, then simulate malicious scripts/executables using Atomic Red Team on the aforementioned VM with administrator privileges.

<br>

The goal for this lab is to demonstrate the capabilities of Sentinel and Log Analytics Workspace against fairly rudimentary TTPs through loosely applying the scientific method for replication/analysis purposes.

<br>

_Adapted from the following project: https://github.com/fizahmad/azure-sentinel-threat-lab_

## Tasks
* Onboard non-Azure Windows VM via **Azure Arc**
* Create custom detection rules via **KQL**
* Build automated alerts via **Logic Apps**
* Utilize the automated alerts to deploy **playbooks**
* Leverage **Atomic Red Team** to simulate adversarial behavior using common TTPs

## Ordered Lab Steps
1. Setup → Begin lab with [environment-setup/overview.md](environment-setup/overview.md) to build the Azure environment and onboard non-Azure VM.
2. Parsers → Deploy KQL scripts from [parsers/parsers-setup.md](parsers/parsers-setup.md) to normalize Sysmon and PowerShell logs.
3. Detections → Import YAML files from [detections/detection-rules-setup.md](detections/detection-rules-setup.md) into Sentinel as Scheduled analytic rules.
4. Automate → Build automated alerts and playbooks from [automation/alerts-setup.md](automation/alerts-setup.md) for Incident Response.
5. Simulation → Leverage [threat-simulations/malicious-exploits.md](threat-simulations/malicious-exploits.md) commands to trigger Sentinel workflows.
6. Documentation → See [reports/findings.md](reports/findings.md) to view analysis regarding simulation from Log Analytics Workspace and Sentinel.
