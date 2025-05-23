**Cheatsheet: Module 1 – Introduction to Ethical Hacking**

---

### 🔒 Information Security Concepts

- **CIA-Triade:**
  - **Confidentiality:** Zugriff nur für Berechtigte (z. B. Verschlüsselung, Datenklassifizierung). Ziel: Schutz vor unbefugtem Zugriff.
  - **Integrity:** Daten sind korrekt und unverändert (z. B. Checksums, Access Control). Ziel: Manipulationssicherheit.
  - **Availability:** Systeme und Daten sind zugänglich (z. B. Redundanzen, Antivirus). Ziel: Verfügbarkeit im Bedarfsfall.
- **Erweiterte Konzepte:**
  - **Authenticity:** Echtheit und Unverfälschtheit von Informationen (z. B. digitale Signaturen). Sicherstellung der Urheberschaft.
  - **Non-Repudiation:** Abstreitbarkeit wird verhindert (z. B. durch Logs, Signaturen). Beweisbarkeit von Aktionen.

---

### 🤖 Hacker-Typen

- **White Hat:** Legale Sicherheitstester im Auftrag von Organisationen.
- **Black Hat:** Kriminelle Angreifer mit Schadensabsicht.
- **Gray Hat:** Wechseln zwischen legalen und illegalen Aktivitäten.
- **Blue Hat:** Externe Tester vor Produkteinführung.
- **Red Hat:** Aggressiv gegen Black Hats gerichtet, teils unethisch.
- **Green Hat:** Lernende Anfänger mit ethischer Absicht.
- **Suicide Hacker:** Ignorieren Konsequenzen, verfolgen radikale Ziele.
- **Weitere Typen:** Hacktivists, staatlich unterstützte Gruppen, Industriespione etc.

---

### 🔎 Hacking-Konzepte

- **Hacking:** Technisches Ausnutzen von Schwachstellen für Zugriff oder Manipulation.
- **Ethical Hacking:** Legitime Sicherheitsüberprüfung zur Abwehr von Bedrohungen.

---

### ⚖️ Ethical Hacking Prozess (CEH Framework)

1. **Reconnaissance:** Zielauswahl, Sammeln öffentlich verfügbarer Informationen.
2. **Scanning:** Identifikation offener Ports, Dienste, Schwachstellen.
3. **Gaining Access:** Exploits nutzen, um Kontrolle über Systeme zu erlangen.
4. **Maintaining Access:** Persistenzmechanismen wie Backdoors installieren.
5. **Clearing Tracks:** Spurenverwischung durch Log-Löschung etc.

#### 🔢 Phasen des Frameworks

| **Phase**                         | **Beschreibung**                                                                                          |
|----------------------------------|-----------------------------------------------------------------------------------------------------------|
| **1. Reconnaissance**            | Informationsbeschaffung über das Zielsystem (z. B. IPs, Domains, Dienste).                               |
| **2. Scanning**                  | Technische Analyse zur Identifikation offener Ports und Schwachstellen.                                  |
| **3. Gaining Access**           | Ausnutzen von Schwachstellen zum Eindringen ins System.                                                  |
| **4. Maintaining Access**       | Aufrechterhaltung des Zugriffs über Backdoors oder persistente Verbindungen.                             |
| **5. Clearing Tracks**          | Beseitigung von Spuren, z. B. durch Löschen von Logs und temporären Dateien.                             |
| **6. Reporting**                | Detaillierte Dokumentation der Erkenntnisse und Empfehlungen zur Behebung.                               |

---

#### 🧰 Tools nach Phase

| **Phase**            | **Beispiele für Tools**                                       |
|----------------------|---------------------------------------------------------------|
| Reconnaissance       | Maltego, Google Dorking, Whois, Recon-ng                      |
| Scanning             | Nmap, Nessus, OpenVAS, Nikto                                  |
| Gaining Access       | Metasploit, Hydra, SQLmap, Exploit-DB                         |
| Maintaining Access   | Netcat, Empire, Meterpreter                                   |
| Clearing Tracks      | Auditpol, Logcleaner, Timestomp                               |
| Reporting            | Dradis, Faraday, Serpico                                      |

---

#### 🎯 Ziel des Frameworks

- Strukturierter und nachvollziehbarer Ablauf beim Ethical Hacking
- Verantwortungsvolle Sicherheitsüberprüfung mit Genehmigung
- Identifikation und Behebung realer Sicherheitslücken
- Basis für Sicherheitsgutachten und technische Risikoanalysen

---

### 🔎 Cyber Kill Chain Phasen

1. **Reconnaissance:** Informationsbeschaffung
2. **Weaponization:** Erstellung schadhafter Payloads
3. **Delivery:** Zustellung z. B. per Mail, USB
4. **Exploitation:** Ausnutzung der Schwachstelle
5. **Installation:** Schadcode wird installiert
6. **Command & Control:** Aufbau eines Steuerkanals
7. **Actions on Objectives:** Zielerreichung (Exfiltration, Zerstörung)

# 🔁 Cyber Kill Chain Methodology

Die **Cyber Kill Chain** ist ein von Lockheed Martin entwickeltes Modell zur Beschreibung der Phasen eines gezielten Cyberangriffs. Ziel ist es, Angriffe frühzeitig zu erkennen, besser zu verstehen und effektiv zu stoppen.

---

#### 🧱 Die 7 Phasen der Cyber Kill Chain

| **Phase**               | **Beschreibung**                                                                                      |
|-------------------------|-------------------------------------------------------------------------------------------------------|
| **1. Reconnaissance**   | Informationssammlung über das Ziel (z. B. Netzwerkstruktur, Mitarbeiter, Schwachstellen).            |
| **2. Weaponization**    | Erstellung einer schadhaften Datei (z. B. Exploit + Payload, meist ohne direkten Kontakt zum Ziel).   |
| **3. Delivery**         | Zustellung des Schadcodes an das Ziel (z. B. per E-Mail-Anhang, USB, Webseite).                       |
| **4. Exploitation**     | Ausnutzung einer Sicherheitslücke zur Codeausführung auf dem Zielsystem.                              |
| **5. Installation**     | Installation von Malware zur Schaffung dauerhaften Zugriffs (Backdoors, Trojaner, Rootkits).          |
| **6. Command & Control (C2)** | Aufbau einer Verbindung zum Angreifer, um das System fernzusteuern.                                 |
| **7. Actions on Objectives** | Durchführung des eigentlichen Ziels: Datendiebstahl, Sabotage, Spionage.                          |

---

#### 🛡️ Abwehrmaßnahmen je Phase

| **Phase**               | **Typische Gegenmaßnahmen**                                                       |
|-------------------------|-----------------------------------------------------------------------------------|
| Reconnaissance          | DNS-Monitoring, Täuschziele (Honeypots), OSINT-Kontrolle                         |
| Weaponization           | Threat Intelligence, Dateianalyse, Antivirus-Signaturen                          |
| Delivery                | E-Mail-Filter, Web-Gateway, Sandbox-Analyse                                       |
| Exploitation            | Patch-Management, Exploit-Prevention-Technologien                                |
| Installation            | Application Whitelisting, Endpoint Detection & Response (EDR)                    |
| Command & Control       | Netzwerk-Monitoring, Firewall-Regeln, Anomalie-Erkennung                         |
| Actions on Objectives   | DLP-Systeme, Protokollierung, Zugriffskontrolle, SIEM                            |

---

#### 🎯 Ziel und Nutzen

- Früherkennung von Angriffen
- Strukturierte Verteidigungsstrategie
- Basis für Incident Response und Security Monitoring


---

#### 🔒 Tactics, Techniques & Procedures (TTPs)

- **Tactics:** Übergeordnetes Ziel einer Angriffsphase
- **Techniques:** Konkrete Umsetzungsmethoden (z. B. Credential Dumping)
- **Procedures:** Gruppenspezifische Vorgehensweisen (z. B. APT-Verhalten)

---

# 🧠 MITRE ATT&CK Framework

Das **MITRE ATT&CK Framework** ist eine öffentlich zugängliche Wissensdatenbank mit realweltlichen Angriffstechniken. Es wird verwendet, um das Verhalten von Angreifern zu analysieren, zu erkennen und geeignete Gegenmaßnahmen zu planen.

---

## 📚 Was bedeutet ATT&CK?

**ATT&CK** = *Adversarial Tactics, Techniques, and Common Knowledge*

- Entwickelt von **MITRE**, einem US-Forschungsinstitut.
- Beschreibt Angreiferverhalten anhand realer Cyberangriffe.
- Wird weltweit in Threat Intelligence, Security Operations, und Red/Blue Teaming eingesetzt.

---

## 🧱 Aufbau des Frameworks

Das Framework ist als Matrix strukturiert:

### 🧭 Tactics (Spalten)
> Beschreiben **das Ziel** eines Angreifers in einem bestimmten Schritt des Angriffs.

Beispiele:
- Initial Access
- Execution
- Persistence
- Privilege Escalation
- Defense Evasion
- Credential Access
- Discovery
- Lateral Movement
- Collection
- Exfiltration
- Command and Control

### 🧰 Techniques (Zeilen)
> Beschreiben **wie** ein Ziel erreicht wird.

Beispiele:
- Phishing
- PowerShell Execution
- DLL Injection
- Pass-the-Hash
- Kerberoasting

### 📊 Sub-techniques
> **Feinere Varianten** von Techniken.

Beispiel:  
Technik: Phishing  
Sub-Techniken: Spear Phishing Attachment, Spear Phishing Link, Spear Phishing via Service

---

## 🔧 Varianten des Frameworks

| **Version**       | **Einsatzbereich**                                       |
|-------------------|----------------------------------------------------------|
| Enterprise        | Für Windows, macOS, Linux, Cloud und Netzwerke           |
| Mobile            | Für Angriffe auf Android und iOS                         |
| ICS               | Für industrielle Steuerungssysteme (z. B. SCADA, PLCs)   |

---

## 🔍 Beispielhafte Matrix-Zeile

| **Taktik**          | **Technik**            | **Sub-Technik**                          |
|---------------------|------------------------|-------------------------------------------|
| Credential Access   | Credential Dumping     | LSASS Memory Dump via ProcDump            |
| Lateral Movement    | Remote Services        | Windows Admin Shares                      |
| Persistence         | Registry Run Keys      | Run Keys / Startup Folder                 |

---

## 🎯 Einsatzbereiche

- Aufbau von **Threat Intelligence** und Angriffserkennung
- Erstellung von **Detection Rules** (SIEM, EDR)
- Planung von **Red-/Blue-/Purple-Teaming**
- **Gap-Analysen** und Abgleich mit realen APT-Gruppen
- Mapping von Schwachstellen und Vorfällen

---

## 🔗 Ressourcen

- 🔗 [Offizielle Website](https://attack.mitre.org)
- 🧭 [ATT&CK Navigator (Visualisierung)](https://mitre-attack.github.io/attack-navigator/)
- 📂 [Threat Groups Übersicht](https://attack.mitre.org/groups/)

---

> 💡 MITRE ATT&CK ist **dynamisch und erweiterbar** – es wird laufend mit neuen Taktiken, Techniken und Gruppen aktualisiert.


---

### 🔓 Security Controls

- **Information Assurance (IA):** Schutz der Datenverarbeitung durch Richtlinien und Maßnahmen.
- **Defense-in-Depth:** Mehrschichtiger Verteidigungsansatz, der verschiedene Schutzebenen kombiniert.
- **Continual Security Strategy:** Dynamische Verteidigung mit Fokus auf Vorhersage, Prävention, Erkennung und Reaktion.

---

### ⚠️ Risiko & Risikomanagement

- **Definition:** Risiko = Bedrohung × Schwachstelle × Wert des Assets
- **Ziel:** Minimierung durch gezielte Sicherheitsmaßnahmen und Ressourcenmanagement.

---

### 🔧 AI-Tools für Ethical Hacking

- **Beispiele:** BurpGPT, BugBountyGPT, PentestGPT, CybGPT, etc.
- **Funktion:** Automatisierung von Schwachstellenscans, C2-Erkennung, Berichterstellung, Angriffssimulation.

---

### 📃 Informationssicherheitsgesetze & Standards

- **PCI DSS (Payment Card Industry Data Security Standard):** Schutz von Kartenzahlungsdaten durch Sicherheitsanforderungen für Händler und Zahlungsdienstleister.
- **ISO/IEC 27001 (Information Security Management Systems):** Internationaler Standard für Informationssicherheits-Managementsysteme (ISMS).
- **HIPAA (Health Insurance Portability and Accountability Act):** US-amerikanischer Standard zum Schutz von Gesundheitsdaten.
- **SOX (Sarbanes-Oxley Act):** US-Gesetz zur Sicherstellung korrekter Finanzberichterstattung.
- **DMCA (Digital Millennium Copyright Act):** Schützt Urheberrechte im digitalen Raum (USA).
- **FISMA (Federal Information Security Management Act):** Sicherheitsanforderungen für US-Behörden.
- **GDPR (General Data Protection Regulation):** EU-weite Datenschutzverordnung mit extraterritorialem Geltungsbereich.
- **DPA 2018 (UK Data Protection Act 2018):** Britisches Datenschutzgesetz, angepasst an Post-Brexit-Bedingungen.


# 📚 Übersicht relevanter Regelwerke in Informationssicherheit & Datenschutz (mit Kurzfassung)

Eine strukturierte Übersicht über internationale Normen, Industriestandards und Gesetze zu Datenschutz, Cybersicherheit und IT-Compliance.

---

| **Kürzel**              | **Langtitel**                                                  | **Themenschwerpunkt**                  | **Typ**                 | **Beschreibung**                                                                 | **Inhalt (Kurzfassung)**                                                                 |
|-------------------------|----------------------------------------------------------------|----------------------------------------|--------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| **PCI DSS**             | Payment Card Industry Data Security Standard                   | Zahlungskartensicherheit               | Branchenstandard         | Schutz von Karteninhaberdaten                                                    | Regelt Sicherheitsmaßnahmen zum Schutz von Kreditkartendaten im Zahlungsverkehr.          |
| **ISO/IEC 27701:2022**  | Privacy Information Management                                 | Datenschutz-Management                 | Internationale Norm      | Erweiterung zu ISO/IEC 27001 für Datenschutz                                     | Führt ein Datenschutz-Managementsystem als Erweiterung zur ISO/IEC 27001 ein.             |
| **ISO/IEC 27002:2022**  | Code of Practice for Information Security Controls             | Maßnahmenkatalog                       | Internationale Norm      | Leitfaden zur Umsetzung von Sicherheitskontrollen                                | Bietet einen Katalog empfohlener Sicherheitsmaßnahmen für Informationssysteme.            |
| **ISO/IEC 27005:2022**  | Information Security Risk Management                           | Risikomanagement                       | Internationale Norm      | Management von Informationssicherheitsrisiken                                    | Definiert Methoden zur Identifikation, Bewertung und Behandlung von Risiken.              |
| **ISO/IEC 27018:2019**  | Protection of Personal Data in Cloud                           | Datenschutz in der Cloud               | Internationale Norm      | Schutz personenbezogener Daten in Cloud-Diensten                                 | Gibt Leitlinien zum Schutz personenbezogener Daten in Cloud-Diensten.                     |
| **ISO/IEC 27032:2023**  | Cybersecurity Guidelines                                       | Cybersicherheitsleitlinien             | Internationale Norm      | Schutz im Cyberspace inkl. Internet, Netzwerke                                  | Stellt Leitlinien zur Cybersicherheit auf, u. a. für Endgeräte, Netzwerke und Web.        |
| **ISO/IEC 27036-3:2023**| Information Security for Supplier Relationships                | Sicherheit in Lieferantenbeziehungen   | Internationale Norm      | Sicherheitsmanagement in der Lieferkette                                         | Regelt Sicherheitsanforderungen in Beziehungen mit externen Lieferanten.                  |
| **ISO/IEC 27040:2024**  | Storage Security                                               | Speichersicherheit                     | Internationale Norm      | Sicherheit von Speichersystemen und -diensten                                    | Beschreibt Anforderungen zur Sicherung von Daten in Speicherlösungen.                     |
| **HIPAA**               | Health Insurance Portability and Accountability Act            | Gesundheitsdatenschutz                 | US-Gesetz                | Schutz sensibler Patientendaten                                                  | Regelt den Umgang mit Gesundheitsdaten und verpflichtet zum Datenschutz.                  |
| **SOX**                 | Sarbanes-Oxley Act                                             | Finanztransparenz                      | US-Gesetz                | Schutz vor Bilanzbetrug, IT-Kontrollen für Finanzberichte                        | Schreibt interne Kontrollen und IT-Sicherheitsmaßnahmen für Finanzberichte vor.           |
| **DMCA**                | Digital Millennium Copyright Act                                | Urheberrechtsschutz                    | US-Gesetz                | Schutz digitaler Inhalte, Anti-Umgehungsmaßnahmen                                | Schützt digitale Werke und verbietet Umgehung von Kopierschutzmaßnahmen.                  |
| **FISMA**               | Federal Information Security Management Act                    | Behördliche Informationssicherheit     | US-Gesetz                | Sicherheitsvorgaben für US-Bundesbehörden                                        | Verpflichtet US-Behörden zur Informationssicherheit und Risikomanagement.                 |
| **GDPR**                | General Data Protection Regulation                              | Datenschutz-Grundverordnung            | EU-Verordnung            | Einheitlicher Datenschutz in der EU                                              | Schützt personenbezogene Daten EU-weit und regelt deren Verarbeitung.                     |
| **DPA 2018**            | Data Protection Act 2018                                       | Datenschutzgesetz UK                   | UK-Gesetz                | Nationale Umsetzung der GDPR im Vereinigten Königreich                          | Ergänzt die DSGVO im britischen Recht und regelt nationale Ausnahmen.                     |

---

> Stand: 2025 – Änderungen und Erweiterungen vorbehalten.


---

**Ende Cheatsheet Modul 1**
