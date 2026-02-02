# Windows VM Guide

## VMware Workstation Setup

Create a Windows 10 Pro VM with VMWare Workstation with the following specs:
| Setting | Value |
--- | --- |
| RAM | 4 GB |
| CPUs | 2 |
| Disk | 60 GB |
| Network | NAT |

Image

## Download and Install Sysmon
Sysmon will provide greater logging detail for process creation, network activity, and file changes/updates
Download: <https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon>

## PowerShell Logging
Ensure to enable script block logging to capture PowerShell commands

Path: `gpedit.msc` > Computer Configuration > Administrative Templates > Windows Components > Windows PowerShell

Then Enable: "Turn on PowerShell Script Block Logging"

Next: Sentinel Onboarding
