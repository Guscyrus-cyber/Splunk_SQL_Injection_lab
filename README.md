Splunk Enterprise SQL Injection Detection & Web Attack Investigation Lab\
\
\
Lab Overview


This lab focused on detecting, monitoring, analyzing, and investigating SQL injection attack activity using Splunk Enterprise within a simulated SOC environment. A custom web attack dataset containing both normal web traffic and malicious SQL injection activity was ingested into the web index and analyzed through SPL queries, visualizations, dashboard panels, lookup enrichment, reports, and automated alerts. The investigation identified suspicious attacker IP addresses, SQL injection payloads, targeted application resources, abnormal HTTP response behavior, and suspicious user agents associated with automated attack activity.\
\
Dataset Overview


The dataset contained simulated web attack logs including:

SQL injection attempts\
authentication bypass attacks\
database extraction payloads\
suspicious automated tools\
malicious URL parameters\
blocked and failed attack activity

Key attacker IP addresses observed during the investigation:

123.123.123.123\
88.88.88.88\
77.77.77.77

Suspicious user agents observed:

sqlmap

HTTP response codes analyzed:

403\
500\
\
Investigation Steps Completed


### Step 1 — Confirm Data Ingestion

Verified that the SQL injection web attack logs were successfully indexed inside Splunk Enterprise under the web index and confirmed that the attack events were searchable.

### Step 2 — Detect SQL Injection Activity

Filtered malicious SQL injection activity using SPL queries to identify suspicious attacker behavior, SQL payloads, targeted URIs, and automated attack tools.

### Step 3 — Analyze Attacker IP Addresses

Analyzed source IP addresses responsible for repeated SQL injection activity and identified the most active attackers targeting the web application.

### Step 4 — Analyze Targeted URLs

Investigated the targeted application resources and analyzed malicious SQL injection payloads embedded within the URI parameters.

### Step 5 — Analyze HTTP Status Codes

Reviewed HTTP response behavior including blocked attack attempts using 403 responses and abnormal backend activity using 500 responses.

### Step 6 — Create Visualizations

Built bar charts, pie charts, column charts, and timeline charts to visually analyze attacker activity, targeted URLs, HTTP responses, and SQL injection timelines.

### Step 7 — Create Dashboard Panels

Organized the investigation visualizations into centralized SOC dashboard panels for security monitoring and web attack investigation workflows.

### Step 8 — Build SOC Monitoring Dashboard

Created a complete SQL Injection SOC Monitoring Dashboard inside Splunk Enterprise combining attacker analysis, URI monitoring, HTTP error analysis, and suspicious user agent activity into a unified investigation interface.

### Step 9 — Threat Intelligence Lookup Enrichment

Created a CSV lookup table and lookup definition to enrich attacker IP addresses with threat intelligence labels and improve SOC investigation visibility.

### Step 10 — SOC Investigation Report Creation

Generated a searchable SOC investigation report containing attacker IP addresses, malicious SQL injection payloads, HTTP response codes, suspicious user agents, and threat intelligence labels.

### Step 11 — Scheduled SQL Injection Alert

Configured a scheduled Splunk alert to automate SQL injection monitoring and continuously detect suspicious web attack activity inside the web index.

## SOC Skills Demonstrated

Splunk Enterprise\
SPL Query Writing\
SQL Injection Detection\
Web Attack Investigation\
Threat Intelligence Enrichment\
Dashboard Creation\
Security Visualization\
SOC Monitoring\
HTTP Log Analysis\
Attacker IP Analysis\
URI Analysis\
Alerting and Reporting\
Incident Investigation Workflow

This lab demonstrated how Splunk Enterprise can be used to detect, investigate, visualize, enrich, report, and automate SQL injection monitoring workflows within a realistic SOC investigation environment. The completed project simulated real-world web attack investigation processes including attacker identification, malicious payload analysis, HTTP response monitoring, threat intelligence enrichment, dashboard monitoring, and automated alerting capabilities suitable for Tier 1 and Tier 2 SOC investigation workflows and cybersecurity portfolio presentation.

**Splunk Enterprise SQL Injection Detection & Web Attack Investigation Lab\
\
Splunk Enterprise SQL Injection Detection & Web Attack Investigation Lab\
\
Splunk Enterprise SQL Injection Detection & Web Attack Investigation Lab\
\**
Top of Form

Bottom of Form

SQL injection is a web attack where an attacker puts malicious SQL code inside a website input, URL, or request. The goal is to trick the web application into sending harmful commands to the database.\
\
This SQL Injection SOC lab focuses on monitoring and investigating simulated web attack traffic using Splunk Enterprise. The dataset contains realistic SQL injection attempts, malicious payloads, attacker IP addresses, targeted URLs, HTTP status codes, and suspicious user agents. The lab demonstrates how Splunk can search, detect, monitor, and analyze web-based attacks through SPL queries, dashboards, reports, and visualizations. The investigation process includes identifying SQL injection payloads, tracking attacker behavior, analyzing targeted web resources, and reviewing server responses. The lab also covers dashboard creation, scheduled reporting, and SOC-style web attack investigation techniques. By the end of the lab, the environment functions as a realistic Tier 1 and Tier 2 SOC web security monitoring and incident analysis project suitable for GitHub documentation and professional portfolio presentation.**\**
\
In this SOC investigation lab, a custom web attack dataset was first created and saved locally on macOS as a log file. The dataset simulated realistic web traffic containing both normal HTTP requests and malicious SQL injection attempts. The log file was then uploaded into Splunk Enterprise for ingestion into the web index using a custom web sourcetype.

dataset entries:\
\
2026-05-15T13:00:00Z host=web01 src_ip=123.123.123.123 method=GET uri="/admin.php?id=1 OR 1=1" status=403 action=sql_injection_attempt user_agent="sqlmap"\
\
2026-05-15T13:01:15Z host=web01 src_ip=185.220.101.45 method=POST uri="/login.php" status=500 action=sql_injection_attempt user_agent="python-requests"

2026-05-15T13:02:33Z host=web01 src_ip=45.33.22.11 method=GET uri="/products.php?id=10 UNION SELECT username,password FROM users" status=403 action=sql_injection_attempt user_agent="curl"

2026-05-15T13:03:44Z host=web01 src_ip=192.168.1.20 method=GET uri="/index.php" status=200 action=normal_web_request user_agent="Mozilla/5.0"\
\
This dataset contains both external attacker IP addresses and legitimate internal web traffic, creating a realistic SOC investigation environment inside Splunk Enterprise. Suspicious external IPs such as 123.123.123.123, 185.220.101.45, and 45.33.22.11 generated SQL injection attempts using payloads like UNION SELECT and suspicious user agents such as sqlmap, curl, and Python-requests, while receiving HTTP 403 and 500 responses indicating blocked or failed attack activity. In contrast, the internal private IP address 192.168.1.20 generated normal web browsing traffic with a successful HTTP 200 response, allowing comparison between legitimate and malicious behavior during the investigation and helping demonstrate attacker identification, web attack monitoring, and traffic analysis within Splunk Enterprise.\
\
123.123.123.123\
185.220.101.45\
45.33.22.11\
192.168.1.20\
\
\
123.123.123.123\
suspicious external attacker IP\
performed UNION SELECT attack\
used sqlmap\
received HTTP 403 response

185.220.101.45\
suspicious external attacker IP\
used POST request\
generated HTTP 500 server error\
suspicious automation activity using Python-requests

45.33.22.11\
suspicious external attacker IP\
attempted database credential extraction\
used curl user agent\
SQL UNION SELECT activity observed

192.168.1.20\
internal/private IP address\
normal web browsing behavior\
legitimate user traffic\
returned HTTP 200 success\
\
\
External IPs:\
123.123.123.123\
185.220.101.45\
45.33.22.11

Internal/private IP:\
192.168.1.20\
\
This creates an investigation scenario because:

malicious external traffic exists\
legitimate internal traffic exists\
normal vs malicious behavior can be compared\
attack filtering becomes possible\
dashboards become more meaningful\
\
Qury:\
index=web\
\
\
\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Step 1. Confirm SQL Attack Data Is Indexed

index=web\
\| table \_time host source sourcetype src_ip method uri status action user_agent

\
\
This search confirms that your SQL attack dataset is inside Splunk. The search looks inside the web index and displays the most important web security fields in a clean table.

You should screenshot the result showing events with fields such as src_ip, method, uri, status, and action.

In this step, I confirmed that the SQL injection web attack logs were successfully indexed in Splunk Enterprise under the web index. The search displayed important web fields such as source IP address, HTTP method, requested URI, status code, action, and user agent. This confirmed that Splunk was receiving and parsing the web attack data correctly before beginning the investigation.\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
Step 2. Detect SQL Injection Activity

index=web action=sql_injection_attempt\
\| table \_time src_ip method uri status user_agent\
\
\

So, this search filters only the malicious SQL injection activity from the web logs. The query displays the attacker IP address, HTTP method, targeted URI, HTTP status code, and user agent associated with each attack attempt. The results help identify which systems attempted SQL injection, what payloads were used, and how the web server responded to the malicious requests.

The output shows suspicious activity such as:

UNION SELECT\
OR 1=1\
suspicious tools like sqlmap\
HTTP 403 and 500 responses\
\
The GET method in the dataset indicates that the attacker sent the malicious request through the URL itself by inserting SQL payloads directly into web parameters such as id= or user=. This allowed the SQL injection attempt to be visible inside the URI field during analysis in Splunk Enterprise. The user_agent field identifies the browser, script, or automated tool used to generate the web request. Normal browsers such as Chrome or Firefox represent legitimate traffic, while suspicious user agents such as sqlmap, curl, and Python-requests indicate automated attack or penetration testing activity commonly associated with SQL injection attempts. The status field shows the HTTP response returned by the web server after receiving the request. In the dataset, 200 indicates successful normal web traffic, 403 indicates blocked or forbidden SQL injection attempts, and 500 represents possible server or database errors triggered during malicious SQL attack activity.

This step separates malicious activity from normal web traffic and begins the actual SOC investigation process. The URI field in the dataset shows the exact web pages and parameters targeted during the simulated SQL injection attacks. These URLs reveal how malicious SQL payloads were inserted into web requests in an attempt to manipulate the backend database. Examples in the dataset include authentication bypass attempts using OR 1=1, database extraction attempts using UNION SELECT, and server manipulation techniques such as SLEEP(5) and DROP TABLE. The targeted pages such as login.php, admin.php, products, and search.php represent common web application entry points frequently abused during SQL injection attacks. Analyzing the URI field in Splunk helps identify which web resources were attacked, what SQL techniques were used, and how attackers attempted to interact with the web application and underlying database systems.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Step 3. Analyze Attacker IP Addresses

index=web action=sql_injection_attempt\
\| stats count by src_ip\
\| sort - count


The results should show suspicious external IP addresses such as:

123.123.123.123\
185.220.101.45\
45.33.22.11

This step focused on analyzing the source IP addresses associated with SQL injection activity inside Splunk Enterprise. The search counted and sorted attacker IP addresses based on the number of malicious requests observed in the dataset. The results identified multiple suspicious external IP addresses performing repeated SQL injection attempts against the web application using payloads such as UNION SELECT and authentication bypass techniques. This analysis demonstrated how Splunk can be used to identify attacker behavior, detect repeated malicious activity, and support SOC investigation workflows through IP-based threat analysis.\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
Step 4. Analyze Targeted URLs

index=web action=sql_injection_attempt\
\| stats count by uri\
\| sort – count\
\
\
\
observations from the 5 events results:

/admin.php?id=1 UNION SELECT password FROM users

most targeted URI\
repeated SQL injection activity\
database credential extraction attempt\
UNION SELECT payload used to retrieve sensitive information\
the exact same SQL injection attack appeared 2 times\
repeated attack activity targeted admin.php\
likely automated or repeated scanning behavior

/login.php?id=1 OR 1=1

authentication bypass attempt\
attacker attempted to manipulate login logic\
classic SQL injection technique\
Single attack login.php

/products?id=1 UNION SELECT username,password FROM users

attempted database enumeration\
targeted product application parameter\
attempted extraction of usernames and passwords\
Single attack products

/search.php?q=admin UNION SELECT password FROM users

search functionality abuse\
malicious SQL payload injected into search parameter\
attempted password extraction from database\
Single attack search.php\
\
3 different events reveal

a separate SQL injection attempt\
different attack techniques\
different targeted application resources

The URI analysis revealed repeated SQL injection attempts targeting dynamic PHP application pages and URL parameters commonly connected to backend databases. Multiple attack payloads including UNION SELECT and OR 1=1 were observed attempting authentication bypass and database credential extraction against administrative, login, product, and search application resources.\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
Step 5. Analyze HTTP Status Codes

index=web\
\| stats count by status\
sort – count\
\
\
The HTTP status code analysis clearly shows how the web server responded to the SQL injection attacks.

Result interpretation:

403 4

4 attack requests were blocked or forbidden\
The web server denied access to the malicious SQL injection attempts\
security controls or application filtering likely prevented the attacks from succeeding

500 1

1 request triggered an internal server or database error\
The SQL injection payload may have caused abnormal application behavior possible backend database interaction failure occurred during the attack attempt

HTTP 500 responses are important because they can indicate:

Vulnerable application behavior\
unhandled exceptions\
Database query failures possible successful partial exploitation attempts

The HTTP status code analysis revealed that most SQL injection attempts were blocked by the web application using HTTP 403 responses, while one malicious request generated an HTTP 500 internal server error indicating abnormal backend application or database behavior during the attack activity.\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Step 6. Visualizations

After completing the investigation queries, the next phase focuses on transforming the SQL injection search results into SOC visualizations inside Splunk Enterprise. Visualizations help security analysts quickly identify attacker behavior, repeated attack activity, targeted application resources, and abnormal server responses through charts and graphical monitoring panels.

# Top Attacker IP Addresses

index=web action=sql_injection_attempt\
\| stats count by src_ip\
\| sort – count

\
This visualization displays the most active attacker IP addresses responsible for SQL injection activity. The chart helps identify repeated malicious behavior and highlights which external systems generated the highest number of attack requests.\
\
\
HTTP Status Code Distribution

index=web\
\| stats count by status\
\
\
\
\
\
\
\
This visualization displays the distribution of HTTP response codes observed during the investigation. The chart visually separates successful traffic (200) from blocked attack attempts (403) and server error activity (500).

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

## Most Targeted URLs

index=web action=sql_injection_attempt\
\| stats count by uri\
\| sort - count

\
This visualization identifies the web application pages most frequently targeted during the SQL injection attacks. The chart highlights attack concentration against pages such as admin.php, login.php, and products.


SQL Injection Activity Over Time\
\
index=web action=sql_injection_attempt\
\| timechart count by src_ip\
\
\
\
\

\
\
\


This visualization displays SQL injection activity across time and separates the attacks by source IP address. The timeline helps identify attack frequency, repeated scanning behavior, and periods of increased malicious activity during the investigation.

The visualization step focused on creating SOC visualizations inside Splunk Enterprise to graphically analyze SQL injection activity and web attack behavior. Multiple visualizations including bar charts, pie charts, column charts, and timeline charts were created using SPL queries built from the investigation results. The visualizations highlighted attacker IP activity, targeted URLs, HTTP response distributions, and SQL injection attack timelines. This phase demonstrated how Splunk visual analytics can support SOC monitoring, attack detection, incident investigation, and web security analysis through graphical dashboards and security-focused visual reporting.\
**\
\**
Although the same SPL queries and visualization charts were used in both Step 6 and Step 7, each phase served a different purpose within Splunk Enterprise. Step 6 focused on creating and testing individual visualizations such as bar charts, pie charts, column charts, and timeline charts directly from the investigation queries in order to visually analyze SQL injection activity, attacker behavior, targeted URLs, and HTTP response patterns. Step 7 then expanded these visualizations into organized dashboard panels within a centralized SOC monitoring dashboard. In this phase, the visualizations were transformed into permanent monitoring components capable of supporting real-time security analysis, web attack investigation, and incident monitoring workflows. This process demonstrated how Splunk visualizations can evolve from standalone analytical charts into structured SOC dashboard panels used for centralized monitoring, attack detection, and operational security investigations.\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

# Step 7. Dashboard Panels

After creating the visualizations, the next phase focuses on building SOC dashboard panels inside Splunk Enterprise. Dashboard panels organize investigation data into a centralized monitoring view that allows security analysts to quickly identify attacker behavior, suspicious activity, targeted resources, and web application attack trends.

# Panel 1. Top Attacker IPs

index=web action=sql_injection_attempt\
\| stats count by src_ip\
\| sort - count

\
\
\
This panel and it’s visualization chart display the most active attacker IP addresses responsible for SQL injection attempts against the web application.


# Panel 2. SQL Injection Timeline

index=web action=sql_injection_attempt\
\| timechart count by src_ip

\
\
\
This panel visualizes SQL injection activity over time and separates attacks by source IP address to identify repeated or automated attack behavior.

# Panel 3. Most Targeted URIs

index=web action=sql_injection_attempt\
\| stats count by uri\
\| sort – count\
\

\
This panel identifies the most frequently targeted web application pages and SQL injection payload locations.\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
\
Panel 4. HTTP Error Analysis


index=web\
\| stats count by status

\
\
\
\
This panel displays the distribution of HTTP response codes generated during the investigation, including successful traffic, blocked attacks, and server error activity.


# Panel 5. Suspicious User Agents

index=web action=sql_injection_attempt\
\| stats count by user_agent\
\| sort - count

\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
This panel identifies suspicious tools and automated attack activity observed in the dataset, including user agents such as:

sqlmap\
curl\
Python-requests

This step focused on building SOC dashboard panels inside Splunk Enterprise to centralize the SQL injection investigation data into a unified monitoring interface. Multiple dashboard panels were created to visualize attacker IP activity, SQL injection timelines, targeted application resources, HTTP response distributions, and suspicious user agents associated with the web attacks. The dashboard panels transformed raw investigation data into organized security monitoring views capable of supporting Tier 1 and Tier 2 SOC analysis, web attack detection, and incident investigation workflows through real-time visual monitoring and graphical security analytics.\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
Step 8. Dashboard Creation\
\
Panel 1. Top Attacker IPs


index=web action=sql_injection_attempt\
\| stats count by src_ip\
\| sort - count


## Panel 2 — SQL Injection Timeline

index=web action=sql_injection_attempt\
\| timechart count by src_ip


## Panel 3 — Most Targeted URIs

index=web action=sql_injection_attempt\
\| stats count by uri\
\| sort - count


## Panel 4 — HTTP Error Analysis

index=web\
\| stats count by status


## Panel 5 — Suspicious User Agents

index=web action=sql_injection_attempt\
\| stats count by user_agent\
\| sort - count

\
\
\
This step focused on building a complete SQL Injection SOC Monitoring Dashboard inside Splunk Enterprise by combining the investigation visualizations and dashboard panels into a centralized monitoring interface. The dashboard integrated attacker IP analysis, SQL injection timelines, targeted URI monitoring, HTTP status code analysis, and suspicious user agent activity into a unified SOC investigation environment. The completed dashboard demonstrated how Splunk Enterprise can centralize web attack detection, security visualization, incident monitoring, and SQL injection investigation workflows through real-time dashboard analytics and operational SOC monitoring capabilities.\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
Lookup: A lookup in Splunk is a way to add extra information to existing log data. For example:


Splunk sees an IP address\
lookup adds a label or description to that IP Address

123.123.123.123\
It becomes:

123.123.123.123 → Known SQL Injection Attacker

## Lookup Table: A lookup table is usually a CSV file containing data that Splunk can reference. For example:

src_ip,label\
\
123.123.123.123,Known SQL Injection Attacker\
185.220.101.45,Suspicious Automated Scanner\
192.168.1.20,Normal Internal Traffic

**\
\**
Lookup Query: It Matches the IP addresses in logs with the IP addresses in the lookup table and add the labels. For example:

index=web\
\| lookup attacker_ip_lookup src_ip OUTPUT label

\
\
Step 9. Lookup Table


This step focuses on using a lookup table inside Splunk Enterprise to enrich the SQL injection investigation data with additional threat intelligence information. A lookup table allows attacker IP addresses to be labeled with custom descriptions such as malicious activity, suspicious behavior, or threat reputation categories. This helps SOC analysts quickly identify known attackers and improves investigation visibility during web attack analysis.

lookup table:

src_ip,label\
\
123.123.123.123,Known SQL Injection Attacker\
185.220.101.45,Suspicious Automated Scanner\
45.33.22.11,Credential Extraction Attempt\
192.168.1.20,Normal Internal Traffic

This lookup table would be save as: attacker_ip_lookup.csv

Then Uploading this CSV file into Splunk Enterprise under:

Settings\
Lookups\
Lookup table files\
saves as attacker_ip_lookup

Now creating the lookup definition: The lookup definition is the configuration object inside Splunk that connects. In this lab:\
\
index=web\
\| lookup attacker_ip_lookup src_ip OUTPUT label\
\| table src_ip label uri status user_agent\
\
\
\
\
\
\
\
\
\
\
\
Lookup Definition Name:\
attacker_ip_lookup

connects to:

CSV File:\
attacker_ip_lookup.csv\
\
The lookup definition tells Splunk:

Which CSV file to use\
Which field to match (src_ip)\
How the lookup query should enrich the logs\
\
when running:

index=web\
\| lookup attacker_ip_lookup src_ip OUTPUT label

Splunk uses the lookup definition named:

attacker_ip_lookup

to find matching IPs inside:

attacker_ip_lookup.csv

and then adds the label field to the search results.

# Lookup Query A

index=web\
\| lookup attacker_ip_lookup src_ip OUTPUT label\
\| table src_ip label uri status user_agent

\
The output of this lookup query displays the source IP address, threat intelligence label, targeted URI, HTTP status code, and user agent associated with the web attack activity observed in the SQL injection investigation dataset. The query searched the web logs inside the web index and used the attacker_ip_lookup lookup definition to match the src_ip field against the uploaded CSV lookup table containing malicious IP classifications. When a matching IP address was found inside the lookup table, Splunk automatically appended the corresponding descriptive label to the investigation results. The output revealed that the IP address 123.123.123.123 was successfully enriched with the label Known SQL Injection Attacker, while other IP addresses such as 88.88.88.88 and 77.77.77.77 remained unlabeled because they were not yet included inside the lookup table. The query also displayed the targeted URIs containing SQL injection payloads, the HTTP response codes generated during the attacks, and suspicious user agents such as sqlmap, allowing the investigation data to become more readable, organized, and useful for SOC monitoring and threat intelligence analysis.\
\
Lookup Query B\
\
index=web\
\| lookup attacker_ip_lookup src_ip OUTPUT label\
\
\
\
The output of the lookup query B displayed enriched SQL injection investigation results by combining the original web attack logs with threat intelligence labels stored inside the custom lookup table. The query matched application resources using suspicious user agents such as sqlmap. This lookup enrichment process demonstrated how Splunk Enterprise can combine raw security logs with external threat intelligence information to improve attacker the src_ip values from the web logs against the IP addresses stored in the attacker_ip_lookup lookup definition and automatically appended descriptive labels to matching attacker IP addresses. The results showed attacker IP activity, targeted SQL injection URIs, HTTP response codes, and suspicious user agents associated with the web attacks. The IP address 123.123.123.123 was successfully identified and labeled as a known SQL injection attacker, while the query also displayed malicious SQL payloads targeting administrative, login, and product identification, SOC monitoring visibility, and web attack investigation workflows.

Bottom of Form

So the step 9 focused on creating a lookup table inside Splunk Enterprise to enrich the SQL injection investigation data with attacker IP classifications and threat intelligence labels. A custom CSV lookup file was created containing malicious external IP addresses, suspicious automated scanners, credential extraction activity, and normal internal traffic labels. The lookup was integrated into Splunk searches to automatically associate descriptive threat labels with attacker IP addresses during the investigation. This demonstrated how Splunk lookup tables can enhance SOC analysis, improve attacker identification, and support threat intelligence enrichment workflows during web application security investigations.\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Step 10. Report creation\
\
This step focused on creating a SOC investigation report inside Splunk Enterprise to document the SQL injection activity identified during the web attack investigation. The report combined attacker IP addresses, threat intelligence labels, targeted URIs, HTTP response codes, and suspicious user agents into a centralized investigation output suitable for SOC monitoring and incident analysis. The report displayed malicious SQL injection attempts targeting administrative, login, and product application resources while also identifying suspicious tools such as sqlmap associated with the attacks.\
\
index=web

\| lookup attacker_ip_lookup src_ip OUTPUT label

\| table \_time src_ip label uri status user_agent\
\
\
This query was used for report creation because it combines the most important SOC investigation information into a single organized report output inside Splunk Enterprise. The query searches the web index for SQL injection activity, enriches the attacker IP addresses using the attacker_ip_lookup lookup table, and displays the investigation results in a readable table format containing timestamps, attacker IP addresses, threat intelligence labels, targeted URIs, HTTP response codes, and suspicious user agents. This allows the report to document when the attacks occurred, which systems performed the attacks, what SQL injection payloads were used, how the web server responded, and which attack tools were involved during the investigation. The report transforms raw web attack logs into structured SOC investigation evidence suitable for monitoring, incident analysis, threat hunting, and security documentation workflows.

The first and fifth events show repeated SQL injection attacks from the IP address 123.123.123.123 targeting the administrative application page /admin.php using a UNION SELECT payload attempting to retrieve passwords from the backend database. The lookup table successfully identified this IP address as a Known SQL Injection Attacker, while the HTTP 403 response indicates the attack was blocked by the web application or security controls. The second event shows the IP address 88.88.88.88 targeting the search functionality using a malicious UNION SELECT payload attempting database extraction through the search.php page. The third event also came from 88.88.88.88 and targeted the product application page using another SQL injection payload attempting to retrieve usernames and passwords, while the HTTP 500 response suggests abnormal backend application or database behavior occurred during the attack. The fourth event shows the IP address 77.77.77.77 attempting an authentication bypass attack against the login application using the classic SQL injection payload OR 1=1, while the HTTP 403 response indicates the malicious login attempt was blocked. All five events used the suspicious user agent sqlmap, indicating automated SQL injection attack activity throughout the investigation dataset.



\
\
\
\
\
\
Also, This step focused on creating a SOC investigation report inside Splunk Enterprise to document the SQL injection activity identified during the web attack investigation. The report combined attacker IP addresses, lookup-based threat intelligence labels, targeted SQL injection URIs, HTTP response codes, and suspicious user agents into a centralized investigation output suitable for security monitoring and incident analysis workflows. The completed report demonstrated how Splunk Enterprise can transform raw web attack logs into organized SOC investigation reports capable of supporting threat analysis, attacker identification, SQL injection detection, and operational incident response activities through searchable and exportable security reporting capabilities.\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
Step 11. Scheduled Report/Alert\
\
The scheduled alert transforms the SQL injection investigation into an automated SOC monitoring workflow capable of continuously detecting suspicious web attack activity inside Splunk Enterprise. Instead of manually searching the logs, the alert automatically monitors incoming events and notifies security analysts whenever SQL injection attempts are detected.\
\
This step focused on creating an automated SQL injection monitoring alert inside Splunk Enterprise. The alert continuously monitors the web index for SQL injection activity and automatically generates results whenever malicious web attack behavior is detected in the logs. The search analyzes attacker IP addresses, targeted URIs, HTTP response codes, and suspicious user agents associated with SQL injection attempts.\
\
index=web action=sql_injection_attempt

\| stats count by src_ip uri status user_agent\
\
\
The alert helps automate:

SQL injection detection\
attacker monitoring\
suspicious web activity monitoring\
SOC investigation workflows\
web application attack visibility

And the alert query identifies:

repeated SQL injection attempts\
malicious SQL payload activity\
suspicious automated tools such as sqlmap\
blocked attack behavior using HTTP 403\
abnormal server activity using HTTP 500\
\
Creating Scheduled Report/Alert

\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
