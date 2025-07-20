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
### Automated Investigation and Response (AIR)
Includes a set of security playbooks that can be launched automatically in response to alerts. Can also trigger Entra workflows for password reset and MFA.
#### Remediation Actions:
- Soft delete email messages or clusters
- Block URL (time-of-click)
- Turn off external mail forwarding
- Turn off delegation
### Configure, Protect, and Detect
- You can define policies to determine the behavior and protection level for predefined threats.
- You can set fine-grained threat protection at the user, organization, recipient, and domain level.
### Safe Attachments
Is a policy that protects against unknown malware, viruses, and provides zero-day protection to safeguard your messaging system. All messages and attachments that don't have a known virus/malware signature are routed to a special environment and analyzed.
#### Actions
When creating a Safe Attachments policy, you have to select from the following options:
- Off - Attachments won't be scanned
- Monitor - Continues delivering the message after malware is detected and track the scan results
- Block - Blocks the current and future emails and attachments with detected malware
- Replace - Blocks the attachments with detected malware but deliver the message body
- Dynamic Delivery - Immediately deliver the message body without attachments, then reattach after scanning
#### Mail Flow Rule
To bypass Safe Attachment processing for internal senders, you can skip filtering by creating a transport rule, or mail flow rule, in the Exchange Admin Center (EAC). Add **X-MS-Exchange-Organization-SkipSafeAttachmentProcessing** to the message header
### Safe Links
- Protects users from malicious URLs in a message or Office document. Malicious links are dynamically blocked.
- Safe Links are both client and location agnostic.
- Includes a default policy that can be edited but not removed.
- Can be applied to messages sent within the organization
- Prevent users from clicking through to the original URL
- Add known safe URLs by flagging them as **Do not rewrite the following URL**
- **X-MS-Exchange-Organization-SkipSafeLinksProcessing**
### Anti-Phishing Policies
- no default anti-phishing policy
- Impersonation and Spoof detection comprise of the Anti-Phishing policies
### Simulate Attacks
- Threat Trackers - provides latest intelligence on prevailing cybersecurity issues
- Threat Explorer - is a real-time report that allows you to identify and analyze recent threats
- Attack Simulator - allows you to run realistic attack scenarios
## Manage Microsoft Entra Identity Protection
### Identity Protection Basics
Is a service that enables organization to view the security posture of any account by accomplishing these key tasks:
- Automate the detection and remediation of identity-based risks
- Investigate risks using data in the portal
- Export risk detection data to third-party utilities for further analysis
Entra Identity Protection requires an Entra ID Premium P2 license to work.
The signals generated by Identity Protection can be fed into Conditional Access or a SIEM
### Implement and Manage User Risk Policy
There are 2 risk policies:
- Sign-in Risk Policy - Focused on sign-in activity itself and analyzing the probability of a rogue sign-in
- User Risk Policy - Detects the probability that a user account has been compromised by detecting risk events that are atypical of user's behavior
#### Choosing Acceptable Risk Levels
Microsoft recommends that User Risk Policy Threshold to **High** and the Sign-in Risk Policy to **Medium** and higher
- High reduces the number of times a policy is triggered and minimizes the challenge to users
- Low threshold introduces extra user interrupts but increased security posture
#### Exclusions
All the policies allow for excluding users for emergency access or break-glass admin accounts.
### Investigate Risky users
Identity Protection provides organizations with 3 reports, in CSV or JSON format, they can use to investigate identity risks in their environment. Admins can perform actions on each detection within the portal.
#### Risky Users
Report provides info:
- Which users (are at/remediated/dismissed) risk
- Details about detections
- History of all risky sign-ins
- Risk history
Admin actions:
- Reset user password
- Confirm user compromise
- Dismiss user risk
- Block user sign-in
- Investigate further using Azure ATP
#### Risk Sign-ins
Report provides info:
- Which sign-ins are classified as:
	- At risk
	- Confirmed compromised
	- Confirmed sage
	- Dismissed
	- Remediated
- Real-time and aggregate risk levels associated with sign-in attempts
- Detection types triggered
- Conditional Access policies applied
- MFA details
- Device information
- Application information
- Location information
Admin actions:
- Confirm sign-in compromise
- Confirm sign-in safe
#### Risk Detections
Report provides info:
- Information about each risk detection, including type
- Other risks triggered at the same time
- Sign-in attempt location
Admin actions:
- Can return to the User Risk or Sign-ins Report
- Can go to Microsoft Defender for Cloud Apps (MDCA) portal for additional logs and alerts
### Remediate Risks
All active risk detections contribute to User Risk Level.
Remediation options:
- Self-remediation with Risk Policy - allow users to unblock with MFA and self-service password reset (SSPR)
- Manual Password Reset - generate temporary password or require user password reset
- Dismiss User Risk - close all events associated with the user
- Close Individual Risk Detections Manually - following actions:
	- Confirm User Compromised
	- Dismiss User Risk
	- Confirm Sign-in Safe
	- Confirm Sign-in Compromised
### Unblock based on User Risk
Unblock options based on User Risk:
- Reset password
- Dismiss User Risk
- Exclude the user from policy
- Disable policy
Unblock options based on Sign-in Risk:
- Sign-in from a familiar location or device
- Exclude the user from policy
- Disable policy
### Use Graph API
3 APIs:
- riskDetection - query both user and sign-in
- riskyUsers
- signIn
### Implement Security for Workload Identities
A Workload Identity allows an application or service principal access to resources. They:
- Can't perform MFA
- Often have no formal lifecycle process
- Need to store their credentials or secrets somewhere
#### Requirements to use Workload Identity Protection
- Entra ID Premium P2 License
- Logged on user must be assigned:
	- Security Administrator
	- Security Operator
	- Security Reader
#### Types of Risks Detected
- Entra Threat Intelligence
- Suspicious Sign-ins
- Unusual addition of credentials to an OAuth app
- Admin confirmed account compromised
- Leaker Credentials
## Introduction to Microsoft Defender for Identity
It is a cloud-based security solution that uses your on-premises Active Directory signals to provide Identity Protection. Provides:
- Monitor users, entity behavior, and activities with learning-based analytics
- Protect user identities and credentials stored in Active Directory
- Identify suspicious user activities and advanced attacks across the cyber-attack kill-chain
- Provide clear incident information on a simple timeline for fast triage
It consists of 3 parts:
- Defender for Identity Portal
- Defender for Identity Sensor
- Defender for Identity Cloud Service
### Identity Sensor
Defender for Identity sensor is installed directly on your domain controllers and accesses the event logs directly. It parses the information and then sends a percentage of them to Identity Cloud Service.
Core functionality:
- Capture and inspect domain controller network traffic
- Receive Windows events directly
- Receive RADIUS accounting information from your VPN
- Retrieve user data from Active Directory
- Perform resolution of network entities
- Transfer relevant data to Identity cloud service
### Review Compromised Accounts or Data
Identity security alerts are divided into the following phases:
- Reconnaissance Phase Alerts
- Compromised ""
- Lateral Movement ""
- Domain Dominance ""
- Exfiltration ""
### Security Alert Structure
- Alert Title - Official Defender for Identity name
- Description
- Evidence - Additional relevant information and data to help with investigation and triage
- Excel Download
### Integrate with other Microsoft Tools
Identity Cloud Service runs on Azure infrastructure, which enables it to connect with Defender for Cloud Apps. This allows you to see and gain insights for on-premises user activities. It also allows you to see all the policies for Defender for Identity in the Cloud Apps policies page.
Defender for Identity can also be integrated with Defender for Endpoint.
## Secure services with Defender for Cloud Apps
### Understand the Defender for Cloud Apps Framework
Cloud Access Security Broker (CASBs) are defined by Gartner as security policy enforcement points, placed between cloud service consumers and service providers to interject security policies on cloud-based resources. CASBs are intermediaries and help you apply monitoring and security controls. Cloud Apps is a CASB.
Elements to Defender for Cloud Apps Framework:
- Discover and control the use of Shadow IT
- Protect sensitive information anywhere in the cloud - provides Data Loss Prevention (DLP) 
- Protect against Cyberthreats and Anomalies - anomaly detection, User Entity Behavioral Analytics (UEBA), Rule-based activity detection, etc.
- Assess the compliance of your Cloud Apps
### Cloud Discovery Dashboard
Shows what is happening in your network. Cloud Discovery analyzes traffic logs and ranks each cloud app against known risk factors. It helps you understand what's happening in your cloud environment after the fact.
### Protect Data and Apps with Conditional Access App Control
Defender for Cloud Apps integrates with identity providers (IdPs) and Entra ID. Access and Session controls are done through Conditional Access App Control if you use IdPs and Defender for Cloud Apps if you use Entra ID. Conditional Access App Control lets you monitor and control user app access and sessions in real time. Can be integrated with Entra Conditional Access. 
Access and Session Policy features:
- Prevent data exfiltration
- Protect on download
- Prevent upload of unlabeled files
- Monitor user sessions for compliance
- Block access
- Block custom activities
### Information Protection
An employee can accidentally send/upload confidential information to the wrong person or place. This lost or wrongfully exposed information can have serious consequences. Defender for Cloud Apps integrates Azure Information Protection, which is a cloud-based service that helps classify and protect files and emails.
Information protection is done through phases:
1. Discover Data - Defender for Cloud Apps can scan and classify data using the app connector or Conditional Access App Control
2. Classify Sensitive Information - Label the data:
	- Personal
	- Public
	- General
	- Confidential
	- Highly Confidential
3. Protect Data - Create policies to apply governance actions:
	- Trigger alerts and email notification
	- Change sharing access for files
	- Quarantine files
	- Remove file or folder permissions
	- Move files to a trash folder
4. Monitor and Report
### Detect Threats
Defender for Cloud Apps provides anomaly detection policies that utilize UEBA and machine learning. Anomaly detections are nondeterministic, meaning they only trigger when behavior deviates from the norm. Defender for Cloud Apps spends the first 7 days learning about the environments IP addresses, devices, locations of the users, and apps and services they use. It then generates a risk score for these activities.
#### Anomaly Detection Policy Overview
- Impossible Travel
- Activity from Infrequent Country
- Malware Detection
- Ransomware Activity
- Activity from Suspicious IP addresses
- Suspicious Inbox Forwarding
- Unusual Multiple File Downloads
- Unusual Administrative Activities
#### Fine-tune Anomaly Detection Policies for Suppression or Surfacing Alerts
Fine-tuning helps reduce alert fatigue from too many false positives.
There are 3 types of suppressions:
- System - built-in detections that are always suppressed
- Tenant - common activities based on the tenant
- User - common activities based on the the user
You can set the suppression sensitivity:
- Low - affects System, Tenant, and User alerts
- Medium - System and User
- High - System
# Mitigate Threats using Microsoft Security Copilot
### What is Generative AI
It is a category of AI that creates original content. This includes natural language, image, and code generation.
### How do LLMs Work
Natural Language Processing (NLP) creates LLMs. NLP has used these methods:
- Tokenization - text is split into tokens based on a rule
- Word Embeddings - defines semantic relationships between words by defining contextual vectors that represents some particular semantic attributes of the token. The vector is in multi-dimensional space. If words have similar amplitudes and magnitudes then you can assume they are related.
- Architectural Developments - the architecture of a ML model defines how data is processed, the model is trained and evaluated, and how predictions are generated. First breakthrough was Recurrent Neural Networks (RNNs). RNNs take the context of the words into account through multiple sequential steps by taking an input and a hidden state. 
### Transformer Architecture



---
## Microsoft Sentinel (SIEM)
- Data connecters - used to ingest data into Sentinel
	can ingest from
		- syslog
		- Common Event Format (CEF)
		- Trusted Automated eXchange of Indicator Information (TAXII)
		- azure activity
		- Microsoft defender services
		- AWS, GCP
- Log retention - after ingest, data is stored in log analytics
	can query data using Kusto Query Language (KQL)
- Workbooks - used to visualize data. essentially a dashboard
- Analytics alerts - can create custom, scheduled alerts
- Threat hunting - can create custom queries and integrate with Azure Notebooks
- Incidents and investigations - incident is created when an alert is triggered.
	sentinel has investigations, where you can visually map entities across log data on a timeline for an incident
- Automation playbooks - you can respond to incidents automatically by automating security operations
