# 📚 Enterprise SIEM - Benutzerhandbuch (Deutsch)

## 🧭 Inhaltsverzeichnis
1. [Einführung](#einführung)
2. [Systemanforderungen](#systemanforderungen)
3. [Installationsanleitung](#installationsanleitung)
4. [Konfiguration](#konfiguration)
5. [Verwendung](#verwendung)
6. [Fehlerbehebung](#fehlerbehebung)
7. [FAQ](#faq)

## 1. Einführung
Willkommen beim Benutzerhandbuch für das Enterprise SIEM-System. Dieses Dokument bietet umfassende Anleitungen zur Bereitstellung, Konfiguration und Bedienung unserer Security Information and Event Management-Lösung.

### 1.1 Systemübersicht
Unsere SIEM-Lösung bietet:
- Zentrales Log-Management
- Echtzeit-Bedrohungserkennung
- Compliance-Berichterstattung
- Automatisierte Incident Response

### 1.2 Hauptkomponenten
| Komponente | Zweck |
|----------|---------|
| Logstash | Log-Erfassung und -verarbeitung |
| Elasticsearch | Datenspeicherung und Suche |
| Kibana | Visualisierung und Analyse |
| Sigma-Regeln | Bedrohungserkennungs-Framework |

## 2. Systemanforderungen
### 2.1 Hardware-Anforderungen
| Komponente | Minimum | Empfohlen |
|----------|---------|-------------|
| CPU | 8 vCPU | 16 vCPU |
| RAM | 32 GB | 64 GB |
| Speicher | 1 TB SSD | 4 TB NVMe |

### 2.2 Software-Anforderungen
- Windows Server 2019 oder neuer
- PowerShell 7.0+
- Elastic Stack 8.12.0
- Python 3.9+

## 3. Installationsanleitung
### 3.1 Schnellinstallation
```powershell
# Repository klonen
git clone https://github.com/example/siem.git

# Wechseln zum Bereitstellungsverzeichnis
cd siem/deployment

# Installationsskript ausführen
.\install-siem.ps1 -Mode Production
```

### 3.2 Manuelle Installation
1. Elastic Stack installieren:
```powershell
# Elasticsearch installieren
msiexec /i elasticsearch-8.12.0.msi /quiet

# Logstash installieren
msiexec /i logstash-8.12.0.msi /quiet

# Kibana installieren
msiexec /i kibana-8.12.0.msi /quiet
```

2. Dienste konfigurieren:
```powershell
# Dienstwiederherstellungsoptionen festlegen
Set-Service -Name "elasticsearch" -StartupType Automatic
Set-Service -Name "logstash" -StartupType Automatic
Set-Service -Name "kibana" -StartupType<write_to_file>
<path>documentation/user_manual_de.md</path>
<content>
# 📚 Enterprise SIEM - Benutzerhandbuch (Deutsch)

## 🧭 Inhaltsverzeichnis
1. [Einführung](#einführung)
2. [Systemanforderungen](#systemanforderungen)
3. [Installationsanleitung](#installationsanleitung)
4. [Konfiguration](#konfiguration)
5. [Verwendung](#verwendung)
6. [Fehlerbehebung](#fehlerbehebung)
7. [FAQ](#faq)

## 1. Einführung
Willkommen beim Enterprise SIEM-Benutzerhandbuch. Dieses Dokument bietet umfassende Anleitungen zur Bereitstellung, Konfiguration und Bedienung unserer Security Information and Event Management-Lösung.

### 1.1 Systemübersicht
Unsere SIEM-Lösung bietet:
- Zentrales Log-Management
- Echtzeit-Bedrohungserkennung
- Compliance-Berichterstattung
- Automatisierte Incident Response

### 1.2 Wichtige Komponenten
| Komponente | Zweck |
|----------|---------|
| Logstash | Log-Erfassung und -verarbeitung |
| Elasticsearch | Datenspeicherung und -suche |
| Kibana | Visualisierung und Analyse |
| Sigma-Regeln | Bedrohungserkennungs-Framework |

## 2. Systemanforderungen
### 2.1 Hardware-Anforderungen
| Komponente | Minimum | Empfohlen |
|----------|---------|-------------|
| CPU | 8 vCPU | 16 vCPU |
| RAM | 32 GB | 64 GB |
| Speicher | 1 TB SSD | 4 TB NVMe |

### 2.2 Software-Anforderungen
- Windows Server 2019 oder neuer
- PowerShell 7.0+
- Elastic Stack 8.12.0
- Python 3.9+

## 3. Installationsanleitung
### 3.1 Schnellinstallation
```powershell
# Repository klonen
git clone https://github.com/example/siem.git

# Wechseln zum Bereitstellungsverzeichnis
cd siem/deployment

# Installationsskript ausführen
.\install-siem.ps1 -Mode Production
```

### 3.2 Manuelle Installation
1. Elastic Stack installieren:
```powershell
# Elasticsearch installieren
msiexec /i elasticsearch-8.12.0.msi /quiet

# Logstash installieren
msiexec /i logstash-8.12.0.msi /quiet

# Kibana installieren
msiexec /i kibana-8.12.0.msi /quiet
```

2. Dienste konfigurieren:
```powershell
# Dienstwiederherstellungsoptionen festlegen
Set-Service -Name "elasticsearch" -StartupType Automatic
Set-Service -Name "logstash" -StartupType Automatic
Set-Service -Name "kibana" -StartupType Automatic
```

## 4. Konfiguration
### 4.1 Datenquellen
Bearbeiten Sie `config/logstash.conf` zur Konfiguration der Datenquellen:
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

### 4.2 Erkennungsregeln
Platzieren Sie Sigma-Regeln im Verzeichnis `detection_rules/`:
```yaml
title: Windows Remote Desktop Anmeldung
description: Erkennt Remote Desktop Anmeldungen
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

## 5. Verwendung
### 5.1 Starten der Dienste
```powershell
Start-Service -Name "elasticsearch", "logstash", "kibana"
```

### 5.2 Zugriff auf Kibana
Öffnen Sie den Browser unter: https://localhost:5601

### 5.3 Dashboard-Navigation
1. Öffnen Sie Kibana
2. Klicken Sie auf "Analytics" > "Discover"
3. Wählen Sie den Zeitbereich (oben rechts)
4. Wählen Sie das Indexmuster (z.B. "winlogbeat-*")

## 6. Fehlerbehebung
### 6.1 Häufige Probleme
**Problem:** Keine Daten erscheinen in Kibana  
**Lösung:** 
1. Dienststatus prüfen:
```powershell
Get-Service -Name "elasticsearch", "logstash", "kibana"
```
2. Logstash-Konfiguration prüfen:
```bash
logstash -t -f config/logstash.conf
```

### 6.2 Log-Dateien
- Elasticsearch: `C:\ProgramData\Elasticsearch\logs\`
- Logstash: `C:\ProgramData\Logstash\logs\`
- Kibana: `C:\ProgramData\Kibana\logs\`

## 7. FAQ
**Q:** Wie aktualisiere ich Erkennungsregeln?  
**A:** Legen Sie aktualisierte Sigma-Regeln im Verzeichnis `detection_rules/` ab und starten Sie Logstash neu.

**Q:** Kann ich benutzerdefinierte Datenquellen hinzufügen?  
**A:** Ja, ändern Sie den Eingabeteil der Datei `config/logstash.conf` und starten Sie Logstash neu.

**Q:** Wie erstelle ich eine Sicherungskonfiguration?  
**A:** Verwenden Sie das Sicherungsskript:
```powershell
.\backup-config.ps1 -Destination C:\Backups\siem
