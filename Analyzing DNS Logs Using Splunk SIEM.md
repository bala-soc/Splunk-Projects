# Analyzing DNS Log Files Using Splunk SIEM

## Introduction
DNS (Domain Name System) logs are crucial for understanding network activity and identifying potential security threats. Splunk SIEM (Security Information and Event Management) provides powerful capabilities for analyzing DNS logs and detecting anomalies or malicious activities.

## Prerequisites
Before analyzing DNS logs in Splunk, ensure the following:
- Splunk instance is installed and configured.
- DNS log data sources are configured to forward logs to Splunk.

## Steps to Upload Sample DNS Log Files to Splunk SIEM

### 1. Prepare Sample DNS Log Files
- Obtain sample [DNS log file](https://www.secrepo.com/maccdc2012/dns.log.gz) in a suitable format (e.g., text files).
- Ensure the log files contain relevant DNS events, including source IP, destination IP, domain name, query type, response code, etc.
- Save the sample log files in a directory accessible by the Splunk instance.

### 2. Upload Log Files to Splunk
- Log in to the Splunk web interface.
- Navigate to **Settings** > **Add Data**.

<img width="863" height="771" alt="1" src="https://github.com/user-attachments/assets/d5fa2e99-12f0-4e7d-b297-59f2c3db7706" />

- Select **Upload** as the data input method.

<img width="1391" height="421" alt="2" src="https://github.com/user-attachments/assets/4d81ca8e-171e-418d-90f0-7e81fdab5143" />


### 3. Choose File
- Click on **Select File** and choose the sample DNS log file you prepared earlier.

<img width="1223" height="846" alt="3" src="https://github.com/user-attachments/assets/83da9ee6-1cbb-409b-8594-f3fc04a44c85" />


### 4. Set Source Type
- In the **Set Source Type** section, specify the source type for the uploaded log file.
- Choose the appropriate source type for DNS logs (e.g., `dns` or a custom source type if applicable).

<img width="773" height="702" alt="4" src="https://github.com/user-attachments/assets/a845f794-c800-4806-bfda-62ba5a2d392f" />


### 5. Review Settings
- Review other settings such as index, host, and sourcetype.
- Ensure the settings are configured correctly to match the sample DNS log file.

<img width="1302" height="833" alt="5" src="https://github.com/user-attachments/assets/096848ae-567c-4d76-bf54-81bd3657429e" />


### 6. Click Upload
- Once all settings are configured, click on the **Review** button.
- Review the settings one final time to ensure accuracy.
- Click **Submit** to upload the sample DNS log file to Splunk.

<img width="1260" height="479" alt="6" src="https://github.com/user-attachments/assets/85ea55a1-850e-4291-b0a2-5cf35f9c9df8" />


### 7. Verify Upload
- After uploading, navigate to the search bar in the Splunk interface.

<img width="1381" height="677" alt="7" src="https://github.com/user-attachments/assets/ecd3eda6-f37e-4d88-a023-a45b2d0d2a2c" />


- Run a search query to verify that the uploaded DNS events are visible.
  
  ```spl
  index=<your_dns_index> sourcetype=<your_dns_sourcetype>

<img width="1920" height="378" alt="8" src="https://github.com/user-attachments/assets/af52e138-2b19-4c9b-af06-b79335eff185" />


## Steps to Analyze DNS Log Files in Splunk SIEM

### 1. Search for DNS Events   
- Open Splunk interface and navigate to the search bar.   
- Enter the following search query to retrieve DNS events   
```
index=* sourcetype=dnslog
```

<img width="1920" height="378" alt="8" src="https://github.com/user-attachments/assets/c920ae85-11a1-47a0-b753-1eb929f598a9" />
<img width="1584" height="838" alt="9" src="https://github.com/user-attachments/assets/a4b1135a-ba43-4380-9073-d401f74b4903" />

### 2. Extract Relevant Fields
- Identify key fields in DNS logs such as source IP, destination IP, domain name, query type, response code, etc.   
- As mentioned below,  | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b": This regex searches for common DNS-related keywords in the raw event data.
- Example extraction command:
```
index=* sourcetype=dnslog | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b"
```
<img width="1102" height="393" alt="10" src="https://github.com/user-attachments/assets/6abac288-1161-4709-9581-f465e72fbf82" />
<img width="1575" height="876" alt="11" src="https://github.com/user-attachments/assets/321a6234-5830-4c6f-b5ec-f475e6447f2a" />


### 3. Identify Anomalies
- Look for unusual patterns or anomalies in DNS activity.
- Example query to identify spikes
```
index=_* OR index=* sourcetype=dnslog  | stats count by fqdn
```

<img width="1032" height="388" alt="12" src="https://github.com/user-attachments/assets/d50d244e-f683-4014-905f-43e25aa989de" />
<img width="1920" height="603" alt="13" src="https://github.com/user-attachments/assets/1cb78ead-ecfb-4faf-bdbd-e805b912307a" />


### 4. Find the top DNS sources
- Use the top command to count the occurrences of each query type:   
```
index=* sourcetype=dnslog | top fqdn, src_ip
```

<img width="934" height="272" alt="14" src="https://github.com/user-attachments/assets/f456ebef-4b6f-445a-9480-af4280c38cc0" />
<img width="1920" height="595" alt="15" src="https://github.com/user-attachments/assets/511cfaf2-e529-4e80-8a01-8c34071c05df" />


### 5. Investigate Suspicious Domains
- Search for domains associated with known malicious activity or suspicious behavior.
- Utilize threat intelligence feeds or reputation databases to identify malicious domains such virustotal.com
- Example search for known malicious domains:
```
index=* sourcetype=dnslog fqdn="maliciousdomain.com"
```

<img width="833" height="280" alt="16" src="https://github.com/user-attachments/assets/8a5185a0-0876-43d2-8ca2-91cdeef8ed0d" />
<img width="1920" height="818" alt="17" src="https://github.com/user-attachments/assets/81f9269b-09c7-4ac7-9619-5879ee9b00cc" />


## Conclusion
Analyzing DNS log files using Splunk SIEM enables security professionals to detect and respond to potential security incidents effectively. By understanding DNS activity and identifying anomalies, organizations can enhance their overall security posture and protect against various cyber threats.




