
# 🧪 Honeypot-Zusammenfassung (Markdown)

## 🔍 Was ist ein Honeypot?
Ein **Honeypot** ist ein absichtlich bereitgestelltes Ködersystem innerhalb eines Netzwerks, das Angreifer anziehen soll. Ziel ist es, deren Verhalten zu analysieren, Angriffe frühzeitig zu erkennen und Schutzmaßnahmen zu verbessern.

> **Wichtig:** Honeypots haben keinen produktiven Zweck – jeder Zugriff wird als potenziell bösartig gewertet.

---

## 🎯 Ziele von Honeypots
- **Angriffe erkennen** (z. B. Portscans, Exploits, Brute-Force)
- **Verhalten und Tools von Angreifern analysieren**
- **Täuschung und Ablenkung** von produktiven Systemen
- **Forschung und Schulung** zur IT-Sicherheit

---

## 🧱 Typen von Honeypots

### 🔹 Low-Interaction Honeypots
- Emulieren nur bestimmte Dienste oder Ports (z. B. SSH, HTTP)
- Geringes Risiko, da kein echter Systemzugriff möglich
- Fokus: Früherkennung von Scans und automatisierten Angriffen

**Beispiele:**
- `KFSensor` – erkennt Portscans, DoS-Angriffe
- `Honeytrap` – lauscht auf TCP/UDP, erkennt Datei-Download-Versuche
- `tiny-ssh-honeypot` – minimalistischer SSH-Köder

---

### 🔸 Medium-Interaction Honeypots
- Simulieren ein Betriebssystem (z. B. Shell-Zugriff), aber ohne volle Systemkontrolle
- Protokollieren komplexeres Angreiferverhalten
- Mittleres Risiko, teilweise erkennbar für fortgeschrittene Angreifer

**Beispiele:**
- `Cowrie` – SSH-/Telnet-Honeypot mit Fake-Dateisystem und Befehlstracking
- `Honeygrove` – TCP-Honeypot mit Mustererkennung
- `Kippo` – älterer SSH-Köder, Cowrie-Vorgänger

---

### 🔺 High-Interaction Honeypots
- Vollwertige Systeme mit realen Schwachstellen und Anwendungen
- Ermöglichen vollständige Kompromittierung (kontrolliert)
- Sehr hohe Datenqualität, aber hohes Risiko → strenge Isolation nötig

**Beispiel: Honeynet**
- Ein **Honeynet** ist ein komplettes Netzwerk aus echten, verwundbaren Systemen
- Alle Aktivitäten werden überwacht (z. B. durch Kernel-Module)
- Steuerung über eine **Honeywall**, die ausgehenden Verkehr filtert

---

## 🧰 Honeypot-Tools im Überblick

| Tool              | Typ                    | Plattform         | Beschreibung                                                                 |
|-------------------|-------------------------|-------------------|------------------------------------------------------------------------------|
| **HoneyBOT**      | Medium-Interaction      | Windows           | GUI, Logging, ideal als IDS-Ergänzung                                        |
| **Cowrie**        | Medium-/High-Interaction| Linux             | SSH/Telnet-Honeypot mit Logging, Fake-Dateisystem                            |
| **KFSensor**      | Low-Interaction         | Windows           | Erkennt Portscans, simuliert Dienste                                         |
| **Honeytrap**     | Low-Interaction         | Linux             | Erkennt Datei-Downloads über FTP/TFTP                                        |
| **Valhala**       | Low-Interaction         | Windows           | Open Source, einfaches Setup                                                 |
| **StingBox**      | High-Interaction        | VM (Win/Linux)    | Virtualisierte Appliances, GUI-Steuerung                                     |
| **Blumira**       | Low-/Medium-Interaction | Cloud/Multi       | Kombiniert mit SIEM, erkennt Lateral Movement                                |
| **NeroSwarm**     | Medium-/High-Interaction| Windows/Linux     | Echtzeitüberwachung und Alarmierung                                          |

---

## 🧠 Vorteile & Risiken

| Vorteil                                  | Risiko                                      |
|------------------------------------------|---------------------------------------------|
| Früherkennung von Angriffen              | Bei High-Interaction: Gefahr durch reale Kompromittierung |
| Realistische Angriffsanalyse             | Wartungsaufwand                              |
| Tarnung von produktiven Systemen         | Evtl. rechtliche Grauzonen bei Logging        |
| Schulung & Forschung                     | Können von Angreifern erkannt werden         |

---

## 📝 Fazit
Honeypots sind **leistungsfähige Werkzeuge zur Angriffsüberwachung und -analyse**, die – je nach Interaktionstiefe – **unterschiedliche Einblicke in Angreiferverhalten ermöglichen**. Von simplen Portködern bis hin zu vollständigen, kompromittierbaren Netzwerken: Die richtige Wahl hängt vom Sicherheitsziel, dem verfügbaren Aufwand und der Umgebung ab.

**Tipp:** Für viele Use Cases reicht ein Medium-Interaction-Honeypot wie **Cowrie** für SSH-Brute-Force-Erkennung und detaillierte Analyse vollkommen aus.

---

> Erstellt: 🧠 mit ChatGPT · Stand: Juni 2025
