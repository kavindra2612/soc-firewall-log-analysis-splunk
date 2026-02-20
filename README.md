# 🛡️ SOC Firewall Log Analysis using Splunk

## 📌 Project Overview
This project demonstrates firewall log analysis using Splunk SIEM to detect suspicious IP activity, blocked traffic patterns, and port scanning behavior.

This project simulates a real Security Operations Center (SOC) workflow for firewall log monitoring and threat detection using Splunk SIEM.

## 🛠️ Tools & Technologies
- Splunk Enterprise (SIEM)
- Firewall Log Dataset (CSV)
- Windows VM Lab
- SPL (Search Processing Language)

## 📂 Project Structure
- firewall_logs.csv → Sample firewall dataset
- queries.txt → SOC detection queries
- screenshots/ → Splunk analysis proof

## 🛡️ Key SOC Use Case Queries (Primary)
These queries simulate real SOC L1 analyst investigations:

### 1. Top Suspicious Source IP Detection
```spl
index=firewall | stats count by src_ip | sort -count
```

### 2. Blocked vs Allowed Traffic Monitoring
```spl
index=firewall | stats count by action
```

### 3. Most Targeted Ports Analysis
```spl
index=firewall | stats count by dest_port | sort -count
```

### 4. Port Scanning Detection (Nmap Behavior)
```spl
index=firewall | stats dc(dest_port) as unique_ports by src_ip | where unique_ports > 5
```

### 5. Suspicious Blocked IP Investigation
```spl
index=firewall action=blocked | stats count by src_ip | sort -count
```

## 🧠 Additional Investigation Queries (Optional)
```
index=firewall | timechart count by action
index=firewall | stats count by src_ip, dest_ip
index=firewall (dest_port=22 OR dest_port=3389 OR dest_port=445)
```

## 📊 SOC Skills Demonstrated
- SIEM Log Analysis (Splunk)
- Firewall Log Monitoring
- SPL Query Development
- Threat Detection & Investigation
- SOC Analyst Use Cases
- Security Event Analysis

## 📸 Screenshots
Screenshots of data ingestion, firewall log analysis, and detection queries are included in the screenshots folder as proof of hands-on lab.

### 🔥 1. Top Suspicious Source IP Detection
This query identifies the most active and potentially suspicious source IP addresses.

```spl
index=firewall | stats count by src_ip | sort -count
```
<img src="screenshots/Top Suspicious Source IP.png" width="700"/>

🚨 2. Blocked Traffic Analysis

This query shows allowed vs blocked traffic by the firewall.
```spl
index=firewall | stats count by action
```
<img src="screenshots/Blocked Traffic Analysis.png" width="700"/>

🌐 3. Most Targeted Ports Detection

This query identifies the most frequently targeted destination ports.

```spl
index=firewall | stats count by dest_port | sort -count
```
<img src="screenshots/Most Targeted Ports.png" width="700"/>

💀 4. Port Scanning Detection (Nmap Behavior)

This query detects IPs accessing multiple unique ports (possible scanning activity).
```spl
index=firewall 
| stats dc(dest_port) as unique_ports by src_ip 
| where unique_ports > 5
```
<img src="screenshots/Port Scanning Detection.png" width="700"/>

🧠 5. Suspicious Blocked IP Investigation

This query highlights source IPs that were blocked multiple times.

```
index=firewall action=blocked 
| stats count by src_ip 
| sort -count
```
<img src="screenshots/Blocked Suspicious IP Investigation.png" width="700"/> 

## 🎯 Author
## - Kavindra Patel  
## Aspiring SOC Analyst | Cybersecurity Student
