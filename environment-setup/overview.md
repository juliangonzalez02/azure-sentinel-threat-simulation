# Azure Environment Setup
To begin this lab we must set up our Azure environment with a Log Analytics Workspace that Sentinel will then leverage in order to protect an on-boarded Windows VM.

## Components
| Component	| Purpose
--- | ---
| Windows 10 VM |	Target machine for attack simulation
| Azure Arc | Connects local non-Azure VM to Azure
| Log Analytics Workspace	| Centralized log storage
| Microsoft Sentinel | SIEM for detection and alerting
| Sysmon | Enhanced Windows logging

## Setup Guide
1. [Azure Environment Setup](azure-env-setup.md) - Create free Azure account, create/configure Log Analystics Workspace, deploy Sentinel
2. [Windows VM Setup](windows_vm_setup.md) - Deploy Windows 10 VM
3. [Azure Arc Onboarding](sentinel-vm-onboard.md) - Connect VM to Azure via Arc and configure data collection
