# Severe Security Events Automation
Now that we've created automated alerts for the security team, we will need to create playbooks that automatically resolve severe potential security events. But first, we must establish a baseline for severe security events.

## Establishing Severity Baseline
It is vital that we first define severe security events to prevent isolating systems, business-critical ones especially, that are not compromised. For instance, potential malicious activity in our environment can produce security events that are either low or medium severity. These events could be malicious but we do not want to immediately isolate the affected systems, Sentinel shall alert and the security team will investigate further. For security events that are either high or critical severity, Sentinel shall automatically isolate compromised systems and the security team will investigate potential breach in our environment.

## Alert of Incident
- `playbook-alert-to-email.json` — On Sentinel incident creation: get incident → extract entities → send email to SOC team members.
- `playbook-alert-to-teams.json` — Post to Teams webhook with incident link and entities.

## Import Guide
1) Sentinel > Automation > Create > Import playbook (Logic App) > Upload JSON.
2) Fix connections: `azureloganalytics`, `office365`, `teams` as prompted.
3) Grant the Logic App `Microsoft Sentinel Responder` role to the workspace.
4) Enable the playbook as an automation rule (Incident triggers: `When Azure Sentinel incident is created`).

## Automated Alert Notifications
- Severity >= High → Run `playbook-auto-contain-host.json` (after you create a service principal with isolate permissions).
- All severities → Run `playbook-alert-to-email.json` for awareness.
- Lateral movement detections → Run `playbook-alert-to-teams.json` to SOC channel.

## Notes
- Keep one playbook per action; chain via automation rules to stay modular.
- Store any secrets (webhook URLs, SP credentials) in Key Vault and reference via managed identity.
- Sample payload mappings are annotated inside each JSON file.

## Next Steps
Now that we've automated security events to alert the security team, next we will create [playbooks](/playbooks-severe-events.md) that Sentinel will run to automatically contain and resolve security events.

**References:**
* Link to playbook
