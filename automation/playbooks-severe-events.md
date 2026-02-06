# Severe Security Events Automation
Now that we've created automated alerts for the security team, we will need to create playbooks that automatically resolve severe potential security events. But first, we must establish a baseline for severe security events.

## Establishing Severity Baseline
It is vital that we first define severe security events to prevent isolating systems, business-critical ones especially, that are not compromised. For instance, potential malicious activity in our environment can produce security events that are either low or medium severity. These events could be malicious but we do not want to immediately isolate the affected systems, Sentinel shall alert and the security team will investigate further. For security events that are either high or critical severity, Sentinel shall automatically isolate compromised systems and the security team will investigate potential breach in our environment.

## Playbooks for Severe Security Events
- `as-mde-isolate-machine.json` — Will match the hosts from a Microsoft Sentinel incident with Microsoft Defender machines and isolate them in Defender. A comment noting the affected machines will be added to the Microsoft Sentinel incident.

## Import Guide
1) Sentinel > Automation > Create > Import playbook (Logic App) > Upload JSON.
2) Fix connections: `azureloganalytics` as prompted.
3) Grant the Logic App `Microsoft Sentinel Responder` role to the workspace.
4) Enable the playbook as an automation rule (Incident triggers: `When High/Critical Azure Sentinel incident is created`).

## Automated Alert Notifications
- Severity >= High → Run `as-mde-isolate-machine.json` (after you create a service principal with isolate permissions).

## Notes
- Keep one playbook per action; chain via automation rules to stay modular.
- Store any secrets (webhook URLs, SP credentials) in Key Vault and reference via managed identity.
- Sample payload mappings are annotated inside each JSON file.

## Next Steps
Now that we've created automated playbooks that Sentinel will run to contain and resolve severe security events, next we will begin testing our security posture through simulating various common TTPs against the Windows VM we previously onboarded to our Azure environment.

<br>

**References:**
* [AS-MDE-Isolate-Machine](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks/AS-MDE-Isolate-Machine)
