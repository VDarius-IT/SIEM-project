# 📚 Enterprise SIEM - User Manual (English)

## 🧭 Table of Contents
1. [Introduction](#introduction)
2. [System Requirements](#system-requirements)
3. [Installation Guide](#installation-guide)
4. [Configuration](#configuration)
5. [Usage](#usage)
6. [Troubleshooting](#troubleshooting)
7. [FAQ](#faq)

## 1. Introduction
Welcome to the Enterprise SIEM system user manual. This document provides comprehensive guidance for deploying, configuring, and operating our Security Information and Event Management solution.

### 1.1 System Overview
Our SIEM solution provides:
- Centralized log management
- Real-time threat detection
- Compliance reporting
- Automated incident response

### 1.2 Key Components
| Component | Purpose |
|----------|---------|
| Logstash | Log ingestion and parsing |
| Elasticsearch | Data storage and search |
| Kibana | Visualization and analysis |
| Sigma Rules | Threat detection framework |

## 2. System Requirements
### 2.1 Hardware Requirements
| Component | Minimum | Recommended |
|----------|---------|-------------|
| CPU | 8 vCPU | 16 vCPU |
| RAM | 32 GB | 64 GB |
| Storage | 1 TB SSD | 4 TB NVMe |

### 2.2 Software Requirements
- Windows Server 2019 or later
- PowerShell 7.0+
- Elastic Stack 8.12.0
- Python 3.9+

## 3. Installation Guide
### 3.1 Quick Installation
```powershell
# Clone repository
git clone https://github.com/example/siem.git

# Navigate to deployment directory
cd siem/deployment

# Run installation script
.\install-siem.ps1 -Mode Production
```

### 3.2 Manual Installation
1. Install Elastic Stack:
```powershell
# Install Elasticsearch
msiexec /i elasticsearch-8.12.0.msi /quiet

# Install Logstash
msiexec /i logstash-8.12.0.msi /quiet

# Install Kibana
msiexec /i kibana-8.12.0.msi /quiet
```

2. Configure services:
```powershell
# Set service recovery options
Set-Service -Name "elasticsearch" -StartupType Automatic
Set-Service -Name "logstash" -StartupType Automatic
Set-Service -Name "kibana" -StartupType Automatic
```

## 4. Configuration
### 4.1 Data Sources
Edit `config/logstash.conf` to configure data sources:
```ruby
input {
  tcp {
    port => 514
    type => "syslog"
  }
  beats {
    port => 5044
  }
}
```

### 4.2 Detection Rules
Place Sigma rules in `detection_rules/` directory:
```yaml
title: Windows Remote Desktop Login
description: Detects remote desktop logins
status: production
author: Security Team
date: 2025-05-01
logsource:
  product: windows
  service: security
detection:
  selection:
    EventID: 4624
    LogonType: 10
  condition: selection
```

## 5. Usage
### 5.1 Starting Services
```powershell
Start-Service -Name "elasticsearch", "logstash", "kibana"
```

### 5.2 Accessing Kibana
Open browser to: https://localhost:5601

### 5.3 Dashboard Navigation
1. Open Kibana
2. Click "Analytics" > "Discover"
3. Select time range (top right)
4. Choose index pattern (e.g., "winlogbeat-*")

## 6. Troubleshooting
### 6.1 Common Issues
**Issue:** No data appearing in Kibana  
**Solution:** 
1. Check service status:
```powershell
Get-Service -Name "elasticsearch", "logstash", "kibana"
```
2. Verify logstash configuration:
```bash
logstash -t -f config/logstash.conf
```

### 6.2 Log Files
- Elasticsearch: `C:\ProgramData\Elasticsearch\logs\`
- Logstash: `C:\ProgramData\Logstash\logs\`
- Kibana: `C:\ProgramData\Kibana\logs\`

## 7. FAQ
**Q:** How do I update detection rules?  
**A:** Place updated Sigma rules in `detection_rules/` directory and restart Logstash.

**Q:** Can I add custom data sources?  
**A:** Yes, modify `config/logstash.conf` input section and restart Logstash.

**Q:** How do I backup configurations?  
**A:** Use the backup script:
```powershell
.\backup-config.ps1 -Destination C:\Backups\siem
