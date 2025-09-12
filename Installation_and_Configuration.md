🔹 Installation Steps

Install Splunk Enterprise (Windows Host):

1. Download Splunk Enterprise for Windows.
        ..[Splunk Enterprise Download](https://www.splunk.com/en_us/download/splunk-enterprise.html)  
2. Run the installer and follow the setup wizard (default settings are fine).  
3. Start Splunk Enterprise and log in via.
4. Create an admin account during setup.  
-> Go to browser and open with http://<Windows_Host_IP>:8000



🔹 Install Splunk Universal Forwarder (Linux Target VM)

    wget -O splunkforwarder.tgz 'https://download.splunk.com/products/universalforwarder/releases/9.3.0/linux/splunkforwarder-9.3.0-Linux-x86_64.tgz'
    tar -xvzf splunkforwarder.tgz -C /opt
    cd /opt/splunkforwarder/bin
    sudo ./splunk start --accept-license
    sudo ./splunk enable boot-start



-> Add the Windows Splunk Enterprise server (replace with Windows host IP + port):

    sudo ./splunk add forward-server <Windows_Host_IP>:9997 -auth admin:changeme

-> Add monitored logs:

    sudo ./splunk add monitor /var/log/syslog
    sudo ./splunk add monitor /var/log/suricata/eve.json



🔹 Install Suricata NIDS (Linux Target VM)

     sudo apt update && sudo apt upgrade -y
     sudo apt install suricata -y
     suricata --build-info


-> Edit configuration:

    sudo nano /etc/suricata/suricata.yaml


-> Set network interface (example eth0):

    af-packet:
     - interface: eth0


-> Enable EVE JSON logging:

    outputs:
     - eve-log:
       enabled: yes
       filetype: regular
       filename: /var/log/suricata/eve.json
       types:
         - alert
         - http
         - dns
         - tls
         - ssh
         - flow


-> Test & start:

    sudo suricata -T -c /etc/suricata/suricata.yaml -v
    sudo systemctl enable suricata
    sudo systemctl start suricata

🔹  Integration

The Splunk Forwarder on the Linux target VM monitors /var/log/suricata/eve.json and /var/log/syslog.

Logs are sent to Windows Splunk Enterprise for indexing and dashboarding.

Example Splunk search:

    index=* sourcetype=json source="/var/log/suricata/eve.json"


🔹 Testing the Setup

Use the Attacker VM to generate traffic (e.g., nmap, ping, curl).

Suricata detects suspicious activity → logs are forwarded to Splunk.

Verify alerts in Splunk dashboards.



🔹 Useful Commands

-> Splunk Forwarder (Linux Target VM)

    sudo /opt/splunkforwarder/bin/splunk start
    
    sudo /opt/splunkforwarder/bin/splunk stop
    
    sudo /opt/splunkforwarder/bin/splunk restart


-> Suricata (Linux Target VM)

    sudo systemctl start suricata
    
    sudo systemctl stop suricata
    
    sudo systemctl restart suricata
    
    sudo systemctl status suricata


-> Splunk Enterprise (Windows)

    "C:\Program Files\Splunk\bin\splunk.exe" start
    "C:\Program Files\Splunk\bin\splunk.exe" stop
    "C:\Program Files\Splunk\bin\splunk.exe" restart
    "C:\Program Files\Splunk\bin\splunk.exe" status








