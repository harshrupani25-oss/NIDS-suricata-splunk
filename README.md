🛡️ End-to-End NIDS Lab: Suricata + Splunk



This project is a mini Security Operations Center (SOC) lab built using:

-> Linux VM with Suricata (IDS/IPS) + Splunk Universal Forwarder  

-> Windows Host with Splunk Enterprise  

-> It demonstrates how to detect and analyze network threats in a home lab setup.


⚙️ Architecture diagram:

<img width="301" height="280" alt="image" src="https://github.com/user-attachments/assets/e2f5c478-b7e8-4413-be3c-131d272d4ffd" />




Flow:

-> Linux VM:Suricata generates IDS alerts → Splunk Forwarder sends logs  

-> Windows Host: Splunk Enterprise ingests logs, builds dashboards, and runs searches 



📊 Dashboards & Detections:

Splunk Internal Logs:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/09c07231-85ac-4c12-af12-99f75958a82b" />


Apache Log Analysis:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2344d312-ba76-4d7d-a057-c8b6f39a5dbb" />


📂 Sample Logs:

In this lab, I ingested:

-> Apache access logs  

-> Linux syslogs 

-> Suricata IDS alerts


🔍 Log Analysis:

-> Some example Splunk queries:

    ..Detect Apache Web Requests
    
--------> &nbsp; ```spl

--------> &nbsp; index=apache\_index source="apache\_log.log"

--------> &nbsp; | stats count by status, clientip



-> Detect SSH Brute Force Attempts:

    ..index=syslog sourcetype=syslog dest\_port=22
    
--------> | stats count by src\_ip

--------> | where count > 10



-> Detect Nmap Scans:

    ..index=suricata sourcetype=suricata:json alert.signature="\*Nmap\*"
    
--------> | stats count by src\_ip, dest\_ip, dest\_port



📚 Learning Outcomes:

-> Through this project, I gained hands-on experience in:

- ✅ Installing and configuring **Suricata** as a network IDS  
- ✅ Setting up the **Splunk Forwarder** to send logs from Linux to Splunk Enterprise  
- ✅ Ingesting and analyzing **real-world logs** (Apache, syslog, Suricata alerts)  
- ✅ Writing **Splunk SPL queries** for threat detection and log analysis  
- ✅ Building and visualizing **dashboards in Splunk Enterprise**  
- ✅ Understanding the **SOC workflow**: log collection → analysis → visualization → detection  


