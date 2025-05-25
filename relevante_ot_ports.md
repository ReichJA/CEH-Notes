
# 🔧 Relevante Ports in OT-Netzwerken

In OT-Umgebungen (z. B. SCADA, ICS, Gebäudeautomation) spielen neben industriellen auch klassische IT-Protokolle eine wichtige Rolle. Nachfolgend eine Übersicht der wichtigsten Ports, die bei der Netzwerkanalyse, Überwachung oder Pentests berücksichtigt werden sollten.

## 📌 Portübersicht

| **Dienst**           | **Protokoll** | **Port(s)**       | **Beschreibung**                                                                 |
|----------------------|---------------|-------------------|----------------------------------------------------------------------------------|
| SSH                  | TCP           | 22                | Sicherer Fernzugriff auf Geräte                                                  |
| Telnet               | TCP           | 23                | Unsicherer Fernzugriff, in älteren OT-Systemen verbreitet                        |
| FTP                  | TCP           | 20, 21            | Unverschlüsselte Dateiübertragung (z. B. Firmware, Logs)                         |
| SFTP (über SSH)      | TCP           | 22                | Sichere Dateiübertragung via SSH                                                 |
| RDP                  | TCP           | 3389              | Fernzugriff auf Windows-HMIs oder Engineering-Stationen                          |
| SNMPv1/v2c           | UDP           | 161, 162          | Überwachung und Verwaltung (unsicher ohne SNMPv3)                                |
| NTP                  | UDP           | 123               | Zeitsynchronisation                                                              |
| VNC                  | TCP           | 5900–5905         | Fernzugriff auf Visualisierungen, häufig unverschlüsselt                         |
| Modbus TCP           | TCP           | 502               | Kommunikation mit SPS (z. B. Siemens, Wago)                                      |
| DNP3                 | TCP/UDP       | 20000             | SCADA/RTU-Kommunikation, besonders im Energiebereich                             |
| BACnet/IP            | UDP           | 47808             | Gebäudeautomatisierung (Heizung, Lüftung, Klima)                                 |
| PROFINET             | UDP           | 34962–34964       | Kommunikation zwischen SPS und IO                                                |
| EtherNet/IP          | TCP/UDP       | 44818, 2222       | Industrielle Kommunikation mit Allen-Bradley                                     |
| OPC Classic (DCOM)   | TCP           | 135 + dynamisch   | Alte Prozesskommunikation (Windows DCOM), schwer abzusichern                     |
| OPC UA               | TCP           | 4840              | Moderne, sichere Prozessdatenkommunikation                                      |
| HTTP                 | TCP           | 80                | Webinterface für Geräte, Panels, SCADA-Systeme                                   |
| HTTPS                | TCP           | 443               | Sichere Webschnittstellen                                                        |

## ⚠️ Hinweise

- **Nicht abgesicherte Dienste** wie Telnet, VNC oder SNMPv1/v2c sollten vermieden oder ersetzt werden.
- Viele OT-Geräte besitzen **Webinterfaces** – Port 80/443 ist daher ein häufiger Einstiegspunkt.
- Achte auf **UDP-Ports**, da sie oft von Sicherheitslösungen übersehen werden.
