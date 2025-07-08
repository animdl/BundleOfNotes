# Mitigate Threats using Microsoft Defender XDR
## Introduction to Defender XDR Threat Protection
### Explore Extended Detection & Response (XDR) Use Cases
#### Detection of Threat
1. Malicious Payload detected on a system
2. Microsoft Defender for Endpoints (MDE) detects the attack, disables user access from device, raises an alert to security operations, communicates to Intune that the risk level of the endpoint is changed, and shares telemetry details about the threat.
3. An Intune Compliance Policy configured with an MDE risk level severity is triggered and marks the account as noncompliant.
4. Conditional Access created in Microsoft Entra ID blocks user access to apps
#### Remediation
MDE remediates threat through:
- automated remediation
- security analyst approval of automated remediation
- analyst manual investigation
#### Access Restricted and Restored
- Conditional Access knows about device risk because MDE notified Intune, which updated compliance status in Entra ID. This restricts all corporate resource related requests.
- After remediation, MDE triggers Intune to update Entra ID, and Conditional Access restores user access to corporate resources.
### Understand Defender XDR in a Security Operations Center (SOC)
#### Modern Security Operations
1. Raw Data Collected: Security & Activity Logs
2. Deep Insights: Actionable alerts using XDR provides high quality detection for each asset and investigation remediation capabilities
3. Broad Enterprise View: Threat Intelligence (TI) shared with SIEM to create a Correlated/Unified Incident view
4. Analysts and Hunters use both SIEM and XDR to improve incident response/recovery time
#### Security Operations Model - Functions and Tools
An Incident starts from the lowest tier and can be escalated in its lifecycle.
##### Hunt and Incident Management (Tier 3)
Proactive Hunting, Advanced Forensics, and Detection Tuning (Used on Major Incidents)
##### Investigation (Tier 2)
Advanced Analysis and Remediation (XDR - Used on High Complexity Incidents)
##### Triage (Tier 1)
Rapid Remediation or Escalation (XDR - Used on High Volume Incidents)
##### Automation (Tier 0)
Automated Investigation and Remediation (XDR - Used on Well Known Attacks)
#### Threat Intelligence
Threat Intelligence teams use a Threat Intelligence Platform (TIP) to provide context and insights to support all other security functions.
### Microsoft Security Graph
Microsoft Graph Security API is an intermediary service that provides a unified model that exposes REST APIs and client libraries to access data on Microsoft cloud services.
### Defender XDR Solution by Domain
- Defender for Identity - Detect an Active Directory Domain compromise
- Defender for Office 365 - Detect a phishing email
- Defender for Endpoint - Detect a malware installation
## Mitigate Incidents using Defender
### Use the Defender Portal
- defender portal lists all the domains that defender covers
- includes protection, detection, investigation, and response
### Map Defender XDR Unified RBAC permissions
Unified Defender XDR RBAC rules replace the RBAC rules of the individual services
- all Unified RBAC rules map to an equivalent RBAC rule in the individual service
### Manage Incidents,
- incident is a collection of correlated alerts that make up the story of an attack
Defender XDR provides cross-domain threat correlation
- Incidents can be edited (name, status, classification)
- can be assigned to individuals
- alerts can be moved between incidents
- can add comments and incident tags
#### Incident Classifications
- True Alerts
- False Alerts
- Not Set
#### Prioritize Incidents
XDR applies correlation analytics and aggregates all related alerts and investigations from different products into one incident
- incident queue can be filtered
### Investigate Incidents
Meant to provide insight of the top characteristics during initial triage
- XDR is aligned to the MITRA ATT&CK framework
- scope section gives a list of top impacted assets that are a part of the incident
- alerts timeline is provided
- evidence section provides a summary of how many artifacts were included in the incident and their remediation
### Manage and Investigate Alerts
- Alert Severity:        
	- High (Red) - commonly associated with Advanced Persistent Threats (APT)
	- Medium (Orange) - from endpoint detection and response post-breach behaviors that may be part of an APT
	- Low (Yellow) - associated with prevalent malware
	- Informational (Grey) - not considered harmful to the network
- Alerts are categorized with the MITRE Enterprise matrix (attack categories)
- Can link alerts to incidents, and can create an incident from an alert
- Alerts can be suppressed
    
- Investigated* using the alert story which details why the alert was triggered, related events before and after, and other related entities
### Manage Automated Investigations,    
- when an alert is triggered, a security playbook goes into effect
- details from the investigation are available during and after
- if an incriminated entity is seen in another device, the scope will expand to that device
	- if the scope exceeds 10 devices, approval is required
### Use the Action Center
- unifies all remediation actions across Defender for Endpoint and Office 365
- lists the pending and completed remediation actions for all endpoints and identities
- can approve pending actions, and review and undo completed actions
- can remove files from quarantine across multiple devices
### Submissions
In Microsoft 265 organization with Exchange Online mailboxes, admins can use the Submission portal to submit artifacts for scanning
- user submissions can be toggled
### Advanced Hunting
- Advanced Hunting is a query-based threat-hunting tool in XDR, used to explore up to 30 days of raw data comprised of multiple tables
- Time zone is UTC
Advanced Hunting data categories:
- Event or Activity Data - info about alerts, security and system events, and routing assessments
- Entity Data - info about users and devices
#### Built-in Schema Reference
- Table Description - type and source of data in the table
- Columns
- Action Types - represent event types supported by the table
- Sample Queries
### Custom Detections
- Used to proactively monitor and respond to various events and system states (breach activity and misconfigured endpoints)
- Works with advanced hunting queries
#### Create Detection Rules
1. Prepare the query
2. Create a new rule and provide alert details
3. Rule frequency
4. Choose the impacted entities
5. Specify actions
6. Set the rule scope
7. Review and turn on the rule
### Investigate Entra ID sign-in logs
You can use KQL to perform sign-in investigation including conditional access policies
### Microsoft Secure Score
It is a measurement of an organization's security posture
### Threat Analytics
Threat analytics is a threat intelligence solution that is designed to provide info on:
- Active threat actors
- Popular and new attack techniques
- Critical vulnerabilities
- Common attack surfaces
- Prevalent malware
#### Threat Analytics Dashboard
Highlights the reports most relevant to your organization
- Latest threats
- High-impact threats
- Highest exposure
### Threat Analytics Reports
#### Assess Impact on your Organization
- Related Incidents - overview of the impact of tracked threats
- Alerts Over Time - shows number of related Active and Resolved alerts over time
- Impacted Assets - shows number of distinct devices and email accounts that have one active alert
- Prevented Email Attempts - shows number of emails in the past 7 days that were blocked or junk folder
#### Review Security Resilience and Posture
- Secure Configuration Status - shows number of devices with misconfigured security settings
- Vulnerability Patching Status - shows number of vulnerable devices
#### View Reports per Tags
Filter by:
- Threat tags
	- Ransomware
	- Phishing
	- Vulnerability
	- Activity Group
- Report types
- Filters
## Introduction to Defender for Office 365





---
## Microsoft Sentinel (SIEM)
- Data connecters - used to ingest data into Sentinel
	can ingest from
		- syslog
		- Common Event Format (CEF)
		- Trusted Automated eXchange of Indicator Information (TAXII)
		- azure activity
		- microsoft defender services\
		- AWS, GCP
- Log retention - after ingest, data is stored in log analytics
	can query data using Kusto Query Language (KQL)
- Workbooks - used to visualize data. essentially a dashboard
- Analytics alerts - can create custom, scheduled alerts
- Threat hunting - can create custom queries and integrate with Azure Notebooks
- Incidents and investigations - incident is created when an alert is triggered.
	sentinel has investigations, where you can visually map entities across log data on a timeline for an incident
- Automation playbooks - you can respond to incidents automatically by automating security operations
