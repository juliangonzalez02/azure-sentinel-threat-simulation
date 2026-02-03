# Alert Automation

First we will leverage workflows from Azure Logic Apps to automatically notify the security team of a security event occurring. 

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
