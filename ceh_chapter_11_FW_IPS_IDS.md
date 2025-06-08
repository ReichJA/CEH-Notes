
# IDS, IPS & Firewall – Zusammenfassung

## 🎯 Lernziele
- IDS, IPS und Firewalls beschreiben und einsetzen
- Techniken zur Umgehung dieser Systeme verstehen
- Honeypots erkennen und nutzen
- Gegenmaßnahmen entwickeln

---

## 🔍 Intrusion Detection System (IDS)

### 🧩 Definition
Ein IDS ist eine Sicherheitslösung (Hardware oder Software), die Netzwerkverkehr analysiert und bei Erkennung verdächtiger Aktivitäten Alarm schlägt.

### 🛠 Hauptfunktionen
- Analyse von Datenverkehr (Sniffer-Funktion)
- Musterabgleich mit bekannten Angriffssignaturen
- Alarmierung bei Verstößen
- Passives System (nur erkennung, keine Blockierung)

### 🧭 Platzierung im Netzwerk
- Vor und/oder hinter Firewalls (Layered Defense)
- Idealerweise nahe der DMZ
- Vorher: Topologie analysieren & kritische Komponenten identifizieren

---

## 🛡️ Intrusion Prevention System (IPS)

### 🧩 Definition
Ein IPS ist ein „aktives“ IDS, das verdächtigen Datenverkehr **inline** analysiert und **automatisch blockiert**.

### 📌 Funktionen
- Realtime-Monitoring und Logging
- Filterung & Blockierung von Angriffen
- Schnelle Reaktion bei Bedrohungen
- Regeln zur Erkennung und Verhinderung von Angriffen

### 📂 Klassifizierung
- Host-based IPS (HIPS)
- Network-based IPS (NIPS)

### ✅ Vorteile gegenüber IDS
- Aktives Eingreifen in den Traffic
- Keine reine Beobachtung
- Schutz vor internen und externen Bedrohungen

---

## 🔎 Erkennungsmethoden von IDS

### 🔹 1. Signature Recognition (Missbrauchserkennung)
- Vergleich von Paketen mit bekannten Angriffssignaturen
- Vorteile: Erkennung bekannter Angriffe
- Nachteile:
  - False Positives durch unscharfe Signaturen
  - Hoher Wartungsaufwand
  - Neue Varianten benötigen viele neue Signaturen

### 🔹 2. Anomaly Detection (Verhaltensbasierte Erkennung)
- Modell des „normalen Verhaltens“ wird erstellt
- Abweichungen = potenzielle Angriffe
- Herausforderungen:
  - Unvorhersehbares Verhalten im Netzwerk
  - Hohe False Positive Rate
  - Schwierige Modellierung

### 🔹 3. Protocol Anomaly Detection
- Vergleich des Protokollverhaltens mit bekannten Standards
- Prüft z. B. Struktur, Reihenfolge, Antwortzeiten
- Erkennt Protokollverletzungen als potenziell bösartig

---

## 🚨 Indikatoren für Intrusionen

### 📁 Dateisystem
- Neue, unbekannte Dateien oder doppelte Erweiterungen
- Änderungen an Dateigröße, Eigentum, Rechten
- Verdächtige SUID/SGID-Dateien (Linux)
- Unerklärlicher Speicherplatzverbrauch
- Langsames Systemverhalten

### 🌐 Netzwerk
- Bandbreitenerhöhung
- Repetitive Scans und Login-Versuche
- Fremde IPs außerhalb des Netzbereichs
- DDoS-Symptome
- Änderungen an Firewall-/Netzwerkkonfiguration
- Unerklärlicher Outbound-Traffic

### 🖥️ System
- Verkürzte oder fehlende Logdateien
- Veränderte Systemkonfigurationen
- Abstürze, Neustarts
- Unbekannte Prozesse oder Software
- Shell-Historys, temporäre Dateien, Tools des Angreifers

---

## 🌐 IDS-Typen

### ▪ Network-Based IDS (NIDS)
- Analysiert Netzwerkverkehr am Übergangspunkt
- Prüft Pakete auf Inhalt, Struktur, Muster
- Häufig verteilt (z. B. an Routern oder Firewalls)

### ▪ Host-Based IDS (HIDS)
- Installiert auf Endgeräten
- Überwacht lokale Logs, Dateizugriffe, Prozesse
- Effektiv gegen Insider-Bedrohungen

---

## ⚠️ IDS-Alarmtypen

- **True Positive**: Angriff erkannt → Alarm ausgelöst ✅
- **False Positive**: Kein Angriff, aber Alarm ⛔
- **False Negative**: Angriff, aber kein Alarm ⚠️
- **True Negative**: Kein Angriff, kein Alarm ✅

---

## 🚨 Indikatoren für Angriffe

### 📁 Dateisystem
- Neue/unbekannte Dateien, doppelte Erweiterungen
- SUID/SGID-Dateien, Dateigrößenänderungen
- Fehlende Logs, auffällige Prozesse

### 🌐 Netzwerk
- Bandbreitenspitzen
- Verbindungen von unbekannten IPs
- Firewallregeländerungen

### 🖥️ System
- Unerklärte Neustarts
- Fremde Software
- Systemverlangsamung, Crashs

---

## 🔥 Firewall

### 🧩 Definition
Firewall = Hard-/Software-Gateway, das Verkehr zwischen Netzwerken basierend auf definierten Regeln erlaubt/blockiert.

### 🔧 Funktionen
- Filtert nach Adresse, Port, Protokoll
- Verhindert unautorisierten Zugriff
- Kann POP/SMTP regeln, Logging & Alarme auslösen
- Arbeitet eng mit Router zusammen

### 🔍 Filtermechanismen
- **Adressfilter**: Quell-/Ziel-IP, Portnummer
- **Protokollfilter**: Erkennung & Blockierung unerwünschter Dienste
- **Zustandsüberprüfung**: Paketkontext wird analysiert

---

## 🏗️ Firewall-Architektur

### ▪ Bastion Host
- Speziell gehärteter Server zwischen Internet & Intranet
- Zwei Schnittstellen: öffentlich (Internet), intern (Intranet)

### ▪ Screened Subnet (DMZ)
- Drei-Zonen-Modell mit separater DMZ für öffentliche Dienste
- Internet ↔ Firewall ↔ DMZ ↔ weitere Firewall ↔ Intranet
- Vorteil: Schutz des Intranets durch Segmentierung

### ▪ Multi-homed Firewall
- Mehrere Netzwerkkarten (NICs)
- Verbindet mehrere Netzsegmente logisch & physisch
- Erlaubt feingranulare Sicherheitszonen

---



---

