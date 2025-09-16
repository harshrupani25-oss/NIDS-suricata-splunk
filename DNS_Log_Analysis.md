DNS Log Analysis Overview

This DNS log analysis demonstrates how DNS traffic can be ingested, parsed, and analyzed in Splunk as part of the NIDS-Suricata lab. The analysis includes:

- Log Ingestion:Importing DNS logs into Splunk with a defined sourcetype.
- Field Extraction:Parsing raw DNS logs into meaningful fields such as:
  - `src_ip` – Source IP of the query
  - `dest_ip` – Destination IP (DNS server)
  - `dns_query` – Queried domain name
  - `qtype` – Query type (e.g., A, PTR)
  - `rcode_name` – Response code (e.g., NXDOMAIN)
  - `proto` – Protocol (UDP/TCP)
- SPL Commands Used:
  - `eval` → Create new fields or categorize queries
  - `transaction` → Group related query-response events
  - `table / stats count` → Summarize queries by IP, domain, or response
- Data Enrichment (Optional):Using CSV lookup files to add context like location or client name.
- dedup removes duplicate events based on specified fields, keeping only the first occurrence of each unique value.
- Screenshots:Six screenshots demonstrating field extraction, SPL queries, and dashboards.


🛡️ Splunk DNS Log Analysis

This module demonstrates how DNS logs can be ingested, analyzed, and visualized in Splunk as part of the NIDS-Suricata lab. The workflow includes **log ingestion, field extraction, enrichment, SPL commands, and visualization**.

---

1. Log Ingestion
Import DNS log files into Splunk using a defined `sourcetype`.

<img width="1920" height="1080" alt="Screenshot (44)" src="https://github.com/user-attachments/assets/7057813d-fe0d-468a-a6c9-0d2ca170b433" />



---

2️. Field Extraction
Parse raw DNS logs into meaningful fields such as `src_ip`, `src_port`, `dst_ip`, `dst_port`, `dns_query`, `fqdn`, `rcode_type`, and `protocol`.

<img width="1920" height="1080" alt="dns log etract field 1" src="https://github.com/user-attachments/assets/6b0d3b44-0d8f-4545-83e7-8772f806e899" />

---

3️. Data Enrichment
(Optional) Enrich IP addresses or other fields using lookups or external CSVs.

<img width="1920" height="1080" alt="field in intresting field" src="https://github.com/user-attachments/assets/65e3b771-4dd5-4ffe-875d-471e3b821a93" />


---

4️. Using eval
Create new fields or categorize DNS queries using `eval` commands.

<img width="1920" height="1080" alt="dns log analisys using eval command " src="https://github.com/user-attachments/assets/126852b7-9872-48c1-8dea-562206898a0a" />


---

5️. Using transaction 
Group related DNS query-response events into single logical events using `transaction`.

<img width="1920" height="1080" alt="dns log analisys using tranction command " src="https://github.com/user-attachments/assets/c1fcda91-9ac7-4841-96b4-905f10cdd328" />

Using transaction / table:-

<img width="1920" height="1080" alt="dns log analisys using tranction table command " src="https://github.com/user-attachments/assets/2122f54c-e05f-45fd-97e2-badbad8f1c7d" />



---

6️. Using stats count
Summarize queries by client IP, domain, or response code using `table` and `stats count` commands.

<img width="1920" height="1080" alt="dns log analisys using stats count command " src="https://github.com/user-attachments/assets/ca29625d-5a11-4235-b2aa-040f8086204a" />

---

7. dedup removes duplicate events based on specified fields, keeping only the first occurrence of each unique value.

<img width="1920" height="1080" alt="Screenshot (45)" src="https://github.com/user-attachments/assets/de1ba03d-7ed8-4670-b2b2-2a8c26cd333e" />


---

✅ Summary
This workflow complements Suricata NIDS alerts by providing **contextual visibility into DNS traffic**, helping identify potential reconnaissance, suspicious queries, or misconfigurations in the network.

