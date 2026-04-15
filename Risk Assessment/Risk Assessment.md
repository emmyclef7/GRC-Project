#### **Scope and context**

Define scope:  “Enterprise‑wide information security”

Confirm assets in scope: Applications, servers, devices, data assets, business processes.

In the dataset, They are included in:

* Applications.csv
* Servers.csv
* Devices.csv
* DataAssets.csv
* BusinessProcesses.csv



##### **Build the asset \& process register**

* Identify critical assets (systems, data, processes).
* Rank them by criticality and data sensitivity.
* Confirm owners for each.



In the dataset:

* BusinessProcesses.csv → Criticality, ProcessOwnerEmployeeID
* DataAssets.csv → DataSensitivity, SystemOfRecord
* Applications.csv / Servers.csv / Devices.csv → Criticality fields, owner





1. **From BusinessProcesses.csv**, here are the processes with Critical or High criticality:



|**ProcessID**|**ProcessName**|**Criticality**|Risks Present|
|-|-|-|-|
|BP001|Customer Onboarding|High|RSK001, RSK010|
|BP002|Payroll Processing|Critical|RSK003, RSK012|
|BP003|Financial Reporting|Critical|RSK004, RSK005|
|BP004|Vendor Management|High|RSK006, RSK014|
|BP005|Incident Response|Critical|RSK001, RSK016|
|BP006|Access Provisioning|High|RSK007, RSK024|
|BP007|Backup \& Recovery|Critical|RSK008, RSK020|
|BP008|Network Operations|High|RSK009, RSK023|
|BP010|Customer Support Operations|High|RSK001, RSK010|
|BP011|Board Governance|High|RSK003|
|BP012|Compliance Management|High|RSK013, RSK025|
|BP013|Software Development Lifecycle|High|RSK019, RSK030|
|BP016|Inventory \& Supply Chain Management|High|RSK009|
|BP017|Identity \& Access Governance|Critical|RSK003, RSK024|
|BP018|Security Monitoring|Critical|RSK001, RSK028|
|BP019|Customer Billing|High|RSK004|



* Potential Missing Risks



Even though all processes have risks, some processes are missing expected risks based on industry norms.



**CRITICAL PROCESSES**



**BP002 – Payroll Processing (Critical)**

Existing Risks: RSK003, RSK012

Additional Risks Identified:

\- RSK031 – Brute‑force login attempts (HR systems targeted in logs)

\- RSK032 – Credential theft (Payroll access is high‑value)

\- RSK033 – Privileged misuse (Payroll admins)

\- RSK039 – Critical vulnerabilities on servers (SRV008, SRV009)

\- RSK041 – Data leakage (Payroll data is highly sensitive)



**BP003 – Financial Reporting (Critical)**

Existing Risks: RSK004, RSK005

Additional Risks Identified:

\- RSK039 – Critical CVEs on financial servers (SRV009)

\- RSK040 – Patch SLA non‑compliance

\- RSK037 – API instability (APP001, APP029 dependencies)

\- RSK032 – Suspicious logins (Finance users targeted)



**BP005 – Incident Response (Critical)**

Existing Risks: RSK001, RSK016

Additional Risks Identified:

\- RSK035 – Endpoint compromise (SOC tools triggered multiple alerts)

\- RSK038 – Lateral movement (SOC detected this)

\- RSK033 – Privileged misuse (SOC analysts have elevated access)



**BP007 – Backup \& Recovery (Critical)**

Existing Risks: RSK008, RSK020

Additional Risks Identified:

\- RSK040 – Patch SLA non‑compliance (SRV020 backup server)

\- RSK035 – Malware risk (backup servers targeted in logs)

\- RSK041 – Data leakage (backup data is sensitive)



**BP017 – Identity \& Access Governance (Critical)**

Existing Risks: RSK003, RSK024

Additional Risks Identified:

\- RSK031 – Brute‑force login attempts

\- RSK032 – Credential theft

\- RSK033 – Privileged misuse

\- RSK036 – Cloud IAM misconfiguration

\- RSK038 – Lateral movement



**BP018 – Security Monitoring (Critical)**

Existing Risks: RSK001, RSK028

Additional Risks Identified:

\- RSK035 – Endpoint compromise

\- RSK038 – Lateral movement

\- RSK037 – API abuse (SOC tools rely on APIs)

\- RSK033 – Privileged misuse (SOC analysts)



**HIGH‑CRITICALITY PROCESSES**



**BP001 – Customer Onboarding (High)**

RSK001, RSK010, RSK032, RSK041



**BP004 – Vendor Management (High)**

RSK006, RSK014, RSK034, RSK039



**BP006 – Access Provisioning (High)**

RSK007, RSK024, RSK031, RSK033, RSK036



**BP008 – Network Operations (High)**

RSK009, RSK023, RSK034, RSK040



**BP010 – Customer Support Operations (High)**

RSK001, RSK010, RSK032, RSK041



**BP011 – Board Governance (High)**

RSK003, RSK032, RSK041



**BP012 – Compliance Management (High)**

RSK013, RSK025, RSK041



**BP013 – Software Development Lifecycle (High)**

RSK019, RSK030, RSK037, RSK039



**BP016 – Inventory \& Supply Chain Management (High)**

RSK009, RSK034, RSK039



**BP019 – Customer Billing (High)**

RSK004, RSK039, RSK040, RSK037



So even though every process has risks, several processes are under‑represented.



|**Category**|**Old Register**|**New Register**|
|-|-|-|
|Total Risks|30|41|
|Critical/High Processes Covered|100%|100%|
|Processes with Missing Risks|16|0|
|New Risks Added|-|11|
|Completeness|Medium|High|
|Audit Readiness|Partial|Strong|



**2. From the Applications.csv**



Since the Applications.csv does not include a Criticality column, I derived it using a structured scoring model based on:

**1. Business Process Dependency (0–3 points)**

• 	3 = Supports a Critical process

• 	2 = Supports a High process

• 	1 = Supports a Medium process

• 	0 = Supports only Low processes

**2. Data Sensitivity Handled (0–3 points)**

• 	3 = Restricted data

• 	2 = Confidential data

• 	1 = Internal data

• 	0 = Public data

**3. Incident History (0–2 points)**

• 	2 = Multiple incidents

• 	1 = One incident

• 	0 = No incidents

**4. Vulnerability Exposure (0–2 points)**

• 	2 = Critical vulns

• 	1 = Medium vulns

• 	0 = None

**5. Security Function Criticality (0–2 points)**

• 	2 = Security tooling (SIEM, IAM, IR)

• 	1 = Monitoring/Logging



|**Score**|**Rating**|
|-|-|
|9-12|Critical|
|6-8|High|
|3-5|Medium|
|0-2|Low|





**Step 1:** Derive business process dependency score

From the BusinessProcesses.csv and look at SupportingSystems.



1.1. Map applications to process criticality

From your processes:

* **Critical processes**

\- BP002: APP003, APP007

\- BP003: APP001, APP006, APP029

\- BP005: APP022, APP043, APP044

\- BP007: APP025, APP041, APP020

\- BP017: APP006, APP021, APP040

\- BP018: APP022, APP023, APP024



* **High processes**

\- BP001: APP002, APP037

\- BP004: APP008, APP010

\- BP006: APP021, APP033, APP034

\- BP008: APP021, APP017

\- BP010: APP004, APP005

\- BP011: APP015, APP016

\- BP012: APP030, APP031

\- BP013: APP017, APP018, APP019

\- BP016: APP035, APP036

\- BP019: APP001, APP029



* **Medium processes**

\- BP009: APP014, APP038

\- BP014: APP015, APP039

\- BP015: APP011, APP012

\- BP020: APP028, APP030



For each application, take the highest applicable score:

\- 3 = supports at least one Critical process

\- 2 = supports at least one High (but no Critical)

\- 1 = supports at least one Medium (but no High/Critical)

\- 0 = not referenced in any process

Examples

\- APP001 (CoreBank)

&#x09;Used by BP003 (Critical) and BP019 (High) → score = 3

\- APP002 (CRM360)

&#x09;Used by BP001 (High) → score = 2

\- APP015 (Analytics360)

&#x09;Used by BP011 (High) and BP014 (Medium) → score = 2 (take the max)

\- APP011 (DocuSign)

&#x09;Used by BP015 (Medium) → score = 1

\- APP047 (CloudStorage)

&#x09;Not listed in any process → score = 0



Applying this logic to all apps.



**Step 2:** Data sensitivity score

From Applications.csv:

\- Restricted → 3

\- Confidential → 2

\- Internal → 1

\- Public → 0 (none in file)

Examples:

\- APP001 CoreBank → Restricted → 3

\- APP002 CRM360 → Confidential → 2

\- APP004 TicketFlow → Internal → 1

\- APP022 SIEMVision → Restricted → 3



**Step 3:** Incident history score

look at Incidents.csv and obvious mappings.

\- APP017 DevOpsPipeline

* INC2026‑014 “API Abuse Attempt” (unusual API traffic)
* LOG024 “API Error” and LOG036 “Pipeline Alert”

→ Treat as multiple incidents → 2



\- APP022 SIEMVision

* INC2026‑012 “SIEM Alert: Suspicious Login”
* Multiple SIEM alerts in logs (LOG010, LOG023, LOG034)

→ 2



\- APP025 BackupVault

\- INC2026‑013 “Backup Failure”

→ 1



\- APP001 CoreBank

\- INC2026‑016 “Web Server Outage” (reasonable to tie to a core service)

→ 1



\- APP037 CustomerPortal

\- LOG010 “Suspicious login from unusual location”

→ 1



For most other apps with no clear incident reference,i assign:

\- 0 = No incidents



**Step 4:** Vulnerability exposure score

I map applications to servers/devices where it’s reasonable:

\- CoreBank (APP001) → SRV001 (VUL001 Critical) → 2

\- FinanceLedger (APP006) → SRV009 (VUL003 Critical) → 2

\- ExpensePro (APP029) → likely on SRV009 as well → 2

\- BackupVault (APP025) → SRV020 (VUL013 High, plus VUL039 Patch Alert on SRV018/020) → treat as 1–2; we’ll use 2 because of critical patch alert.

\- NetworkMonitor (APP021) → NET001/NET019/NET020 (VUL014–VUL016 High) → 1

\- SIEMVision / IncidentManager / EndpointGuard → run on infra with High vulns but no explicit Critical CVEs → 1

If no clear mapping → 0.



**Step 5:** Security function criticality score

From descriptions:

* 2 = Security tooling (SIEM, IAM, IR, key management, encryption)

\- APP020 DatabaseAdmin (admin to restricted DBs)

\- APP021 NetworkMonitor

\- APP022 SIEMVision

\- APP023 ThreatIntel

\- APP024 EndpointGuard

\- APP025 BackupVault

\- APP032 SecureShare (secure file sharing)

\- APP033 VPNGateway

\- APP039 DataWarehouse (restricted analytics platform)

\- APP040 KeyManagementSystem

\- APP041 EncryptionSuite

\- APP042 LogArchive

\- APP043 IncidentManager

\- APP044 PhishSim



* 1 = Monitoring/Logging (but not full security tooling)

\- APP017 DevOpsPipeline

\- APP018 GitRepo

\- APP019 BuildServer

\- APP026 CloudManager

\- APP038 WebAnalytics

\- 0 = Normal business apps



\- Everything else.



**Step 6:** Work through a few applications end‑to‑end

6.1. APP001 – CoreBank

\- Business Process Dependency

\- Supports BP003 (Critical) and BP019 (High) → 3

\- Data Sensitivity

\- Restricted → 3

\- Incident History

\- Web Server Outage (INC2026‑016) → 1

\- Vulnerability Exposure

\- SRV001 has Critical CVE (VUL001) → 2

\- Security Function Criticality

\- Core business app, not security tooling → 0

Total Score

3+3+1+2+0=9 → Critical

Risks Present (from earlier mapping):

RSK004; RSK005; RSK039; RSK040; RSK037; RSK032



6.2. APP022 – SIEMVision

\- Business Process Dependency

\- Supports BP005 (Incident Response, Critical)

\- Supports BP018 (Security Monitoring, Critical) → 3

\- Data Sensitivity

\- Restricted → 3

\- Incident History

\- Multiple SIEM alerts \& incident INC2026‑012 → 2

\- Vulnerability Exposure

\- Runs on infra with High vulns (no explicit Critical) → 1

\- Security Function Criticality

\- SIEM → 2

Total Score

3+3+2+1+2=11 → Critical

Risks Present:

RSK001; RSK028; RSK035; RSK038; RSK037; RSK033



6.3. APP025 – BackupVault

\- Business Process Dependency

\- Supports BP007 (Backup \& Recovery, Critical) → 3

\- Data Sensitivity

\- Confidential → 2

\- Incident History

\- Backup Failure (INC2026‑013) → 1

\- Vulnerability Exposure

\- SRV020 / backup infra with High vulns + critical patch alert → 2

\- Security Function Criticality

\- Backup \& recovery security → 2

Total Score

3+2+1+2+2=10 → Critical

Risks Present:

RSK008; RSK020; RSK040; RSK035; RSK041



6.4. APP002 – CRM360

\- Business Process Dependency

\- Supports BP001 (Customer Onboarding, High) → 2

\- Data Sensitivity

\- Confidential → 2

\- Incident History

\- No direct incidents → 0

\- Vulnerability Exposure

\- No mapped vulns → 0

\- Security Function Criticality

\- Normal business SaaS → 0

Total Score

2+2+0+0+0=4 → Medium

(You could reasonably argue High if you want to weigh business impact more heavily, but strictly by the model it’s 4.)

Risks Present:

RSK001; RSK010; RSK032; RSK041 (from Customer Onboarding process)





**3. From Server.csv:**



Step 1: Define the scoring model for servers

We’ll reuse your 5‑factor model, interpreted for servers:

1\. 	Business Process Dependency (0–3)

• 	3 = Hosts data/services for a Critical process

• 	2 = Hosts data/services for a High process

• 	1 = Hosts data/services for a Medium process

• 	0 = Only Low / not clearly mapped

2\. 	Data Sensitivity (0–3)

• 	3 = Restricted (core banking, finance DBs, key records)

• 	2 = Confidential (HR, legal, backups, sensitive docs)

• 	1 = Internal (intranet, shared drives, dev infra)

• 	0 = Public

3\. 	Incident History (0–2)

• 	2 = Multiple incidents tied to this server/service

• 	1 = One incident

• 	0 = None known

4\. 	Vulnerability Exposure (0–2)

• 	2 = Critical CVEs on this server (from Vulnerabilities.csv)

• 	1 = Only High/Medium CVEs

• 	0 = None

5\. 	Security Function Criticality (0–2)

• 	2 = Security infra (AD, backup, auth, logging, key/crypto)

• 	1 = Monitoring/DevOps infra

• 	0 = Normal business servers

Rating thresholds:

• 	9–12 → Critical

• 	6–8 → High

• 	3–5 → Medium

• 	0–2 → Low



Step 2: Map business process dependency per server

We infer from  + what we already know from Applications/Processes:

• 	SRV001 – CoreBank Backend

• 	Supports CoreBank (APP001) → BP003 (Financial Reporting, Critical) \& BP019 (Customer Billing, High)

→ BP score = 3

• 	SRV002 – CoreBank API

• 	Same as above → 3

• 	SRV003 – Customer Portal

• 	Supports CustomerPortal (APP037) → BP001 (Customer Onboarding, High) \& BP010 (Customer Support, High)

→ 2

• 	SRV008 – CoreBank Database

• 	Same as SRV001/2 → 3

• 	SRV009 – FinanceLedger DB

• 	Supports FinanceLedger (APP006) → BP003 (Critical) \& BP019 (High)

→ 3

• 	SRV010 – DevOps Pipeline

• 	Supports DevOpsPipeline (APP017) → BP013 (SDLC, High) \& BP008 (Network Ops, High)

→ 2

• 	SRV005–SRV007 – DevOps Build Cluster

• 	Same DevOps / SDLC context → 2

• 	SRV011–SRV014 – File Servers (Shared/HR/Legal/Operations)

• 	Support various business functions; no explicit Critical/High process mapping, but clearly important.

• 	We’ll treat them as Medium dependency → 1

• 	SRV015 – AuditTrail DB

• 	Supports AuditTrail (APP009) used by GRC/Compliance (BP012 High, BP003 Critical indirectly)

→ 3

• 	SRV016 – ComplianceSuite DB

• 	Supports ComplianceSuite (APP030) → BP012 (Compliance Management, High) \& BP020 (Training \& Awareness, Medium)

→ 2

• 	SRV017 – HRPro DB Mirror

• 	Supports HRPro (APP003) → BP002 (Payroll Processing, Critical)

→ 3

• 	SRV018 – Intranet Portal

• 	Internal comms; no explicit Critical/High process → 1

• 	SRV019 – VendorTrack Portal

• 	Supports VendorTrack (APP008) → BP004 (Vendor Management, High)

→ 2

• 	SRV020 – BackupVault Storage

• 	Supports BackupVault (APP025) → BP007 (Backup \& Recovery, Critical)

→ 3



Step 3: Data sensitivity per server

Based on :

• 	Restricted (3):

• 	SRV001 (CoreBank Backend)

• 	SRV002 (CoreBank API)

• 	SRV008 (CoreBank DB)

• 	SRV009 (FinanceLedger DB)

• 	SRV015 (AuditTrail DB – logs of sensitive actions)

• 	SRV016 (ComplianceSuite DB – compliance records)

• 	SRV017 (HRPro DB Mirror – HR/payroll data)

• 	SRV020 (BackupVault Storage – backups of everything)

• 	Confidential (2):

• 	SRV011 (Shared Drives – mixed but includes sensitive)

• 	SRV012 (HR Documents)

• 	SRV013 (Legal Documents)

• 	SRV014 (Operations Files)

• 	Internal (1):

• 	SRV003 (Customer Portal front‑end)

• 	SRV005–SRV007 (DevOps Build Cluster)

• 	SRV010 (DevOps Pipeline)

• 	SRV018 (Intranet Portal)

• 	SRV019 (VendorTrack Portal)



Step 4: Incident history per server

From Incidents.csv (and reasonable mapping):

• 	INC2026‑016 – Web Server Outage (Application bug)

• 	Likely tied to a web front‑end like SRV003 (Customer Portal) or SRV001/2.

• 	We’ll associate 1 incident with SRV003.

• 	INC2026‑013 – Backup Failure

• 	Clearly tied to backup infra → SRV020 → 1 incident

No other incidents clearly reference specific servers, so:

• 	SRV003 → IncidentScore = 1

• 	SRV020 → IncidentScore = 1

• 	All others → 0



Step 5: Vulnerability exposure per server

From your Vulnerabilities.csv:

• 	Critical CVEs (score 2):

• 	SRV001 → VUL001 (Critical)

• 	SRV008 → VUL002 (Critical)

• 	SRV009 → VUL003 (Critical)

• 	SRV015 → VUL004 (Critical)

• 	SRV016 → VUL005 (Critical)

• 	SRV017 → VUL006 (Critical)

• 	High CVEs (score 1):

• 	SRV004 → VUL010 (High, mitigated)

• 	SRV018 → VUL011 (High, mitigated)

• 	SRV019 → VUL012 (High, mitigated)

• 	SRV020 → VUL013 (High, mitigated)

• 	SRV011–SRV014 → VUL027–VUL030 (Medium, mitigated) → we still treat as 1 (non‑critical but present)

• 	No mapped vulns (score 0):

• 	SRV002, SRV003, SRV005, SRV006, SRV007, SRV010



Step 6: Security function criticality per server

• 	Score 2 (security infra):

• 	SRV004 – Domain Controller (AD)

• 	SRV015 – AuditTrail DB (logging)

• 	SRV016 – ComplianceSuite DB (compliance)

• 	SRV020 – Backup Server (backup/DR)

• 	Score 1 (monitoring/DevOps infra):

• 	SRV005–SRV007 – DevOps Build Cluster

• 	SRV010 – DevOps Pipeline

• 	SRV018 – Intranet Portal (less security, more internal comms → I’ll keep this at 0)

• 	Score 0 (normal business servers):

• 	SRV001, SRV002, SRV003, SRV008, SRV009, SRV011–SRV014, SRV018, SRV019, SRV017



Step 7: Work a few servers end‑to‑end

7.1. SRV001 – CoreBank Backend

• 	BPDependencyScore = 3 (Critical financial processes)

• 	DataSensitivityScore = 3 (Restricted)

• 	IncidentScore = 0 (no direct incident mapped)

• 	VulnerabilityScore = 2 (Critical CVE)

• 	SecurityFunctionScore = 0

Total = 3 + 3 + 0 + 2 + 0 = 8 → High

Risks Present:

RSK004; RSK005; RSK039; RSK040; RSK037; RSK032



7.2. SRV009 – FinanceLedger DB

• 	BPDependencyScore = 3 (Critical financial reporting \& billing)

• 	DataSensitivityScore = 3 (Restricted financial data)

• 	IncidentScore = 0

• 	VulnerabilityScore = 2 (Critical CVE)

• 	SecurityFunctionScore = 0

Total = 3 + 3 + 0 + 2 + 0 = 8 → High

Risks Present:

RSK004; RSK005; RSK039; RSK040; RSK037; RSK032



7.3. SRV020 – Backup Server

• 	BPDependencyScore = 3 (Backup \& Recovery is Critical)

• 	DataSensitivityScore = 3 (Backups of sensitive systems)

• 	IncidentScore = 1 (Backup Failure incident)

• 	VulnerabilityScore = 1 (High CVE)

• 	SecurityFunctionScore = 2 (Backup/DR infra)

Total = 3 + 3 + 1 + 1 + 2 = 10 → Critical

Risks Present:

RSK008; RSK020; RSK040; RSK035; RSK041



7.4. SRV004 – Domain Controller

• 	BPDependencyScore = 2 (supports many High‑criticality processes via AD)

• 	DataSensitivityScore = 2 (credentials, group memberships)

• 	IncidentScore = 0

• 	VulnerabilityScore = 1 (High CVE mitigated)

• 	SecurityFunctionScore = 2 (core IAM infra)

Total = 2 + 2 + 0 + 1 + 2 = 7 → High

Risks Present:

RSK031; RSK032; RSK033; RSK036





