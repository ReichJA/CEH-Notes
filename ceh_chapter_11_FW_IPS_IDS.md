
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

## Firewall

Eine **Firewall** ist ein software- oder hardwarebasiertes System, das den Datenverkehr zwischen einem privaten und einem externen Netzwerk (z. B. dem Internet) filtert.

### Merkmale und Funktionen:
- Kontrolliert eingehenden und ausgehenden Datenverkehr nach definierten Regeln.
- Filterung nach:
  - Quell-/Zieladressen
  - Ports
  - Protokollen
- Protokolliert alle Zugriffsversuche (Audit-Logs).
- Kann Eindringversuche erkennen und Alarme auslösen.
- Konfigurierbar zur Freigabe spezifischer Dienste wie POP oder SMTP.
- Schutz durch Trennung vom restlichen Netz (z. B. physisch vor dem LAN platziert).

---

### Bastion Host

Ein **Bastion Host** ist ein speziell gesicherter Rechner, der als Schutzschild zwischen dem internen und externen Netzwerk dient.

#### Eigenschaften:
- Zwei Schnittstellen:
  - Öffentliche (Internet)
  - Private (Intranet)
- Vermittelt und prüft eingehenden und ausgehenden Verkehr.
- Häufig gezielt gehärtet (minimale Dienste, starke Authentifizierung).

---

### Screened Subnet (DMZ)

Ein **Screened Subnet** ist eine abgesicherte Zone zwischen dem Internet und dem Intranet.

#### Typische Struktur bei Drei-homed-Firewall:
- **Interface 1:** Internet
- **Interface 2:** DMZ (für öffentliche Dienste)
- **Interface 3:** Internes Netzwerk

#### Vorteile:
- Externe Zugriffe erreichen nur die DMZ, nicht das interne Netz.
- Schutz vor direktem Zugriff auf interne Ressourcen.

#### Nachteile:
- Bei Kompromittierung der zentralen Firewall → Gefahr für DMZ und Intranet.
- Bessere Sicherheit durch **mehrstufige Firewalls** (z. B. separate Firewall zwischen DMZ und Intranet).

---

### Multi-homed Firewall

Eine **Multi-homed Firewall** besitzt mehr als zwei Netzwerkschnittstellen.

#### Eigenschaften:
- Verbindet mehrere Netzsegmente logisch und physisch.
- Ermöglicht fein abgestufte Sicherheitszonen.
- Erhöht Effizienz und Ausfallsicherheit.
- Für höhere Sicherheit: Einsatz von **Back-to-Back-Firewall-Architektur** empfohlen.

---

### Demilitarized Zone (DMZ)

Die **DMZ** ist ein „Pufferbereich“ zwischen sicherem LAN und unsicherem Internet.

#### Merkmale:
- Schützt interne Systeme vor direkten Zugriffen von außen.
- Dienste mit öffentlichem Zugriff (Web, FTP, Mail) werden in der DMZ betrieben.
- Kein direkter Zugriff von außen auf das interne Netzwerk möglich.
- Webserver in der DMZ sollten **nicht direkt** mit internen Datenbankservern kommunizieren.
- Realisierung meist mit **mehrschnittigen Firewalls**.
---

# Vergleich: Firewall vs. IDS vs. IPS

| Merkmal                   | **Firewall**                                      | **IDS (Intrusion Detection System)**             | **IPS (Intrusion Prevention System)**            |
|--------------------------|---------------------------------------------------|--------------------------------------------------|--------------------------------------------------|
| **Ziel**                 | Zugriffskontrolle und Paketfilterung              | Angriffserkennung                               | Angriffserkennung und Verhinderung               |
| **Arbeitsweise**         | Regelbasiertes Blockieren/Erlauben von Traffic    | Passives Monitoring und Alarmierung             | Aktive Blockierung und Traffic-Manipulation      |
| **Position im Netzwerk** | Zwischen internem und externem Netz (Gateway)     | Meist hinter der Firewall (z. B. SPAN-Port)      | Inline im Datenpfad (zwischen Endpunkten)        |
| **Traffic-Verarbeitung** | Blockiert oder erlaubt Pakete anhand von Regeln   | Analysiert Kopien des Datenverkehrs             | Analysiert und blockiert/ändert Traffic direkt   |
| **Reaktion auf Angriffe**| Blockiert nach Regeln                             | Alarmiert (Log, E-Mail, SIEM-Anbindung)         | Blockiert/verändert Traffic, trennt Verbindungen |
| **Regelbasis**           | Manuell definierte Regeln                         | Signatur- oder verhaltensbasiert                | Signatur- oder verhaltensbasiert                 |
| **Fokus**                | Zugriffskontrolle                                | Erkennung von Angriffen (z. B. Exploits)         | Erkennung und Verhinderung von Angriffen         |
| **Einfluss auf Latenz**  | Gering bis mittel                                 | Gering (da passiv)                              | Mittel bis hoch (durch Analyse im Datenpfad)     |
| **False Positives**      | Selten bei korrekter Konfiguration                | Möglich (führt zu Fehlalarmen)                  | Kritisch (kann legitimen Traffic blockieren)     |
| **Beispiele**            | iptables, pfSense, Cisco ASA                      | Snort (IDS-Modus), Suricata, Zeek               | Snort (IPS-Modus), Suricata, Cisco Firepower     |# Vergleich: Firewall vs. IDS vs. IPS

## 🔥 Unterschied zwischen Network-based und Host-based Firewalls

### 🧱 1. Network-based Firewall

Eine **network-based firewall** (netzwerkbasierte Firewall) wird auf einem dedizierten Gerät oder Gateway installiert, das den Datenverkehr zwischen verschiedenen Netzwerken überwacht und filtert – typischerweise zwischen dem internen Netzwerk und dem Internet.

#### Merkmale:
- Läuft auf Routern, Hardware-Appliances oder dedizierten Servern.
- Schützt **mehrere Geräte gleichzeitig** innerhalb eines Netzwerks.
- Arbeitet meist auf Netzwerk- oder Transportebene (OSI-Schichten 3 und 4).
- Typischerweise im Rechenzentrum oder an Netzwerkgrenzen platziert.
- Beispiele: Cisco ASA, pfSense, Fortinet, Palo Alto.

#### Vorteile:
- Zentrale Kontrolle über ein gesamtes Netzwerksegment.
- Weniger Belastung für Endgeräte.
- Gut skalierbar.

#### Nachteile:
- Keine Sicht auf lokalen Datenverkehr innerhalb eines Hosts.
- Kann umgangen werden, wenn ein Angreifer bereits im internen Netz ist.

---

### 💻 2. Host-based Firewall

Eine **host-based firewall** (hostbasierte Firewall) wird direkt auf einem einzelnen Gerät (Host) installiert, z. B. einem Laptop, Server oder PC.

#### Merkmale:
- Läuft als Software auf dem Endgerät (z. B. Windows Defender Firewall, iptables).
- Schützt **nur das jeweilige Gerät**.
- Erkennt auch lokalen Verkehr zwischen Anwendungen oder Schnittstellen.
- Arbeitet oft auf höheren OSI-Schichten (Schichten 4–7).

#### Vorteile:
- Fein granulare Kontrolle über eingehende/ausgehende Verbindungen pro Anwendung.
- Bietet Schutz auch innerhalb des Netzwerks (z. B. gegen laterale Bewegungen von Angreifern).
- Ideal für mobile Geräte, Notebooks und Server.

#### Nachteile:
- Muss auf jedem Gerät separat installiert und konfiguriert werden.
- Höherer Verwaltungsaufwand bei vielen Endpunkten.
- Kann durch Malware auf dem Host selbst kompromittiert werden.

---

### 🔄 Vergleichstabelle

| Merkmal                  | Network-based Firewall     | Host-based Firewall           |
|--------------------------|----------------------------|-------------------------------|
| Schutzumfang             | Gesamtes Netzwerksegment   | Einzelner Host                |
| Installation             | Auf Gateway/Appliance      | Auf dem Endgerät              |
| Sichtbarkeit             | Netzwerkverkehr            | Lokaler & Netzwerkverkehr     |
| Performance              | Entlastet Hosts            | Nutzt lokale Ressourcen       |
| Verwaltung               | Zentralisiert              | Dezentral (je Host)           |
| Angriffserkennung lokal  | Eingeschränkt              | Sehr gut                      |

---
