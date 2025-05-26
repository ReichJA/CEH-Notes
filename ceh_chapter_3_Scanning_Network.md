
# 🛠️ Cheatsheet: Chapter 03 – Scanning Networks

## 🎯 Lernziele
- Netzwerk-Scanning-Konzepte verstehen
- Verschiedene Scanning-Tools anwenden
- Hosts erkennen (Host Discovery)
- Port- und Dienst-Erkennung durchführen
- Betriebssystem identifizieren (OS Fingerprinting)
- IDS-/Firewall-Erkennung umgehen
- Gegenmaßnahmen beim Scanning kennen

## Einleitung: Grundlagenprotokolle

### 🔹 Was ist ARP (Address Resolution Protocol)?
ARP ist ein Netzwerkprotokoll, das verwendet wird, um die MAC-Adresse (physikalische Adresse) eines Geräts anhand seiner IP-Adresse zu ermitteln. Es arbeitet im OSI-Schichtenmodell auf der Sicherungsschicht (Layer 2) und ist essenziell für IPv4-basierte Netzwerke.

### 🔹 Was ist ICMP (Internet Control Message Protocol)?
ICMP ist ein Kontrollprotokoll der Netzwerkschicht (Layer 3), das für die Übertragung von Fehler- und Statusmeldungen zuständig ist. Es wird z. B. von Ping oder Traceroute verwendet.

### 🔹 Was ist TCP/IP?
TCP/IP ist das grundlegende Kommunikationsprotokoll des Internets. Es besteht u. a. aus:
- **TCP (Transmission Control Protocol):** verbindungsorientiertes Protokoll zur zuverlässigen Datenübertragung.
- **IP (Internet Protocol):** zuständig für das Routing und die Adressierung der Pakete im Netzwerk.


## 🔍 Scanning-Arten

| Typ                 | Zweck |
|---------------------|-------|
| **Port Scanning**   | Liste offener Ports und laufender Dienste |
| **Network Scanning**| Erkennt aktive Hosts und IPs |
| **Vulnerability Scanning** | Erkennt bekannte Schwachstellen anhand von Katalogen (z. B. Exploit-Listen) |

## 🎯 Scanning-Ziele
- Live-Hosts, offene Ports und IP-Adressen entdecken
- OS und Systemarchitektur bestimmen (Fingerprinting)
- Laufende Dienste erkennen
- Anwendungen und Versionen identifizieren
- Schwachstellen analysieren
- Netzwerktopologie kartieren

## 🧱 TCP-Kommunikation & Flags

### 📡 TCP Flags
| Flag | Beschreibung |
|------|--------------|
| `SYN` | Verbindungsaufbau einleiten |
| `ACK` | Empfang bestätigen |
| `PSH` | Daten direkt an Anwendung weiterleiten |
| `URG` | Dringende Daten bevorzugt behandeln |
| `FIN` | Verbindung beenden |
| `RST` | Verbindung abbrechen |

### 🔁 Three-Way Handshake
1. `SYN` (Client → Server)
2. `SYN-ACK` (Server → Client)
3. `ACK` (Client → Server)

### 🔚 Verbindung beenden
- `FIN` oder `RST` vom Sender
- `ACK` vom Empfänger
- Gegenseitiger `FIN`, danach vollständiger Verbindungsabbau

## ⚙️ Tools & Beispiele

### 🔧 Nmap
- Quelle: [nmap.org](https://nmap.org)
- Syntax: `nmap <optionen> <Ziel-IP>`

### 🔧 Hping3
- Quelle: [salsa.debian.org](https://salsa.debian.org)
- Wichtige Optionen:
  - `-1`: ICMP-Modus
  - `-2` oder `--udp`: UDP-Modus
  - `-A`: ACK-Scan
  - `-Q`: Sequence Number sammeln
  - `--tcp-timestamp`: TCP Timestamp setzen
  - `-8`: Scan-Modus (z. B. SYN-Port-Scan)
  - `-F`, `-P`, `-U`: FIN, PUSH, URG-Scan
  - `--rand-dest`: Zufällige Zieladressen
  - `-9`: Listen-Modus (HTTP etc.)
  - `--flood`: Flooding (z. B. DoS mit SYN)
  - `--icmp`, `--count N`: ICMP mit Anzahl-Paketen

#### 🧪 Beispielkommandos
```bash
hping3 -1 10.0.0.25
hping3 -A 10.0.0.25 -p 80
hping3 -2 10.0.0.25 -p 80
hping3 192.168.1.103 -Q -p 139
hping3 -S 72.14.207.99 -p 80 --tcp-timestamp
hping3 -8 50-60 -S 10.0.0.25 -V
hping3 -F -P -U 10.0.0.25 -p 80
hping3 -1 10.0.1.x --rand-dest -I eth0
hping3 -9 HTTP -I eth0
hping3 -S 192.168.1.1 -a 192.168.1.254 -p 22 --flood
```

## 🤖 AI-gestütztes Scanning mit Hping3

Beispiel-Prompt:
> "Use Hping3 to perform ICMP scanning on the target IP address 10.10.1.11 and stop after 10 iterations"

```bash
sudo hping3 --icmp --count 10 10.10.1.11
sudo hping3 --ack -p 80 10.10.1.11
```

## 🧰 Weitere Tools

### 🛠️ Metasploit
- Quelle: [metasploit.com](https://www.metasploit.com)

### 🛠️ NetScanTools Pro
- Quelle: [netscantools.com](https://www.netscantools.com)

### 🛠️ Weitere Tools
| Tool                        | Quelle |
|----------------------------|--------|
| `sx`                       | [GitHub](https://github.com) |
| `RustScan`                 | [GitHub](https://github.com) |
| `MegaPing`                 | [magnetosoft.com](http://magnetosoft.com) |
| `SolarWinds Toolset`       | [solarwinds.com](https://www.solarwinds.com) |
| `PRTG Network Monitor`     | [paessler.com](https://www.paessler.com) |


## 🔍 1. Host Discovery

Host Discovery ist der erste Schritt im Network Scanning. Ziel ist es, aktive Systeme zu identifizieren, um unnötige Portscans auf inaktive Hosts zu vermeiden.

---

## 📡 Host Discovery Techniques

| Methode               | Beschreibung |
|----------------------|--------------|
| **ARP Ping Scan**    | Sendet ARP-Anfragen im LAN; funktioniert auch bei restriktiven Firewalls. |
| **UDP Ping Scan**    | Sendet UDP-Pakete (Default Port: 40125) – Antwort zeigt aktiven Host. |
| **ICMP Ping Scan**   | Sendet ICMP Echo Request – Antwort bestätigt aktive Hosts. |
| **ICMP Timestamp Ping** | Fragt Zeitstempel des Hosts ab – nützlich bei geblockten Echo-Anfragen. |
| **ICMP Address Mask Ping** | Fragt Subnetzmaske ab – ebenfalls nützlich bei geblockten Echos. |
| **TCP SYN Ping**     | Initiiert halbe TCP-Verbindung mit SYN, prüft auf ACK – Default: Port 80. |
| **TCP ACK Ping**     | Sendet TCP ACK – aktiver Host antwortet mit RST. |
| **IP Protocol Scan** | Nutzt Header von Protokollen (ICMP/IGMP/TCP/UDP) zur Host-Erkennung. |

---

## 🛠 Details zu Scans und Tools

### 🔧 ARP Ping Scan
- Verwendet ARP-Pakete zur Erkennung aktiver Geräte.
- Tool: **Nmap** mit `-PR`
- Kein Portscan: `-sn`, deaktivierbar mit `--disable-arp-ping`

### 🔧 UDP Ping Scan
- Tool: **Nmap** mit `-PU`
- Antwort oder ICMP Fehler → Host ist aktiv

### 🔧 ICMP ECHO Ping
- Tool: **Nmap** mit `-PE`
- Optionen: `-L` (Parallelisierung), `-T` (Timeout)

### 🔧 ICMP ECHO Ping Sweep
- Sendet ICMP an IP-Range
- Antworten = aktive Hosts

### 🔧 ICMP Timestamp Ping
- Tool: **Nmap** mit `-PP`
- Fragt Zeitwert ab – nützlich bei geblocktem Echo

### 🔧 ICMP Address Mask Ping
- Tool: **Nmap** mit `-PM`
- Erkennt Subnetzmaske

### 🔧 TCP SYN Ping
- Tool: **Nmap** mit `-PS`
- Ports: `-PS22-25,80,113`
- Silent Scan ohne Verbindung

### 🔧 TCP ACK Ping
- Tool: **Nmap** mit `-PA`
- RST-Antwort → Host aktiv

### 🔧 IP Protocol Ping
- Tool: **Nmap** mit `-PO`
- Nutzt Protokolle ICMP/IGMP/IPinIP/TCP/UDP

---

## 🤖 Host Discovery with AI

### Beispiel #1
```bash
nmap -sn 10.10.1.0/24 -oG - | awk '/Up$/{print $2}' > scan1.txt
```

### Beispiel #2
```bash
nmap -T4 -iL scan.txt -oN scan2.txt -v0
```

### Beispiel #3
```bash
nmap -sn -PE 10.10.1.0/24
```

---

## 🧰 Ping Sweep Tools

| Tool                          | URL |
|-------------------------------|-----|
| **Angry IP Scanner**          | https://angryip.org |
| **SolarWinds Engineer’s Toolset** | https://www.solarwinds.com |
| **NetScanTools Pro**          | https://www.netscantools.com |
| **Colasoft Ping Tool**        | https://www.colasoft.com |
| **Advanced IP Scanner**       | https://www.advanced-ip-scanner.com |
| **OpUtils**                   | https://www.manageengine.com |


## Port and Service Discovery

- Ziel: Erkennung offener Ports und Dienste auf Live-Systemen.
- Admins nutzen Portscans zur Überprüfung der Netzwerksicherheit.
- Angreifer nutzen Portscans, um Angriffsflächen zu identifizieren.
- Oft offen gelassene Ports bieten Angriffsvektoren.

### Wichtige Ports (Auswahl)

| Port / Protokoll       | Dienst / Beschreibung                          |
|-----------------------|----------------------------------------------|
| 7/tcp,udp              | echo, sink null Users                         |
| 21/tcp                 | FTP (Dateiübertragung)                        |
| 22/tcp                 | SSH (Secure Shell)                            |
| 23/tcp                 | Telnet                                       |
| 25/tcp                 | SMTP (E-Mail Versand)                         |
| 53/tcp,udp             | DNS (Domain Name Service)                     |
| 80/tcp                 | HTTP                                         |
| 443/tcp                | HTTPS                                        |
| 110/tcp                | POP3 (Post Office Protocol)                   |
| 137-139/tcp,udp        | NetBIOS Dienste                              |
| 143/tcp                | IMAP                                         |
| 161/udp                | SNMP                                         |
| 194/tcp                | IRC (Internet Relay Chat)                     |
| 389/tcp                | LDAP                                         |
| 445/tcp                | Microsoft-DS / SMB                            |
| 5060/tcp,udp           | SIP (Session Initiation Protocol)             |
| 1723/tcp               | PPTP                                         |
| 2049/tcp               | NFS                                          |

## Wichtige Ports für Tests

- ftp (21), ssh (22), telnet (23), tftp (69), http (80), https (443), pop3 (110), ntp (123), netbios-ns (137), imap (143), snmp (161), irc (194), imap3 (220), syslog (514), printer (515), kerberos-* (88, 749), sip (5060), x11 (6000-6063)

---

## 3. Scan-Typen

### TCP Scanning

- **Open TCP Scanning Methods:**
  - TCP Connect/Full-open Scan

- **Stealth TCP Scanning Methods:**
  - Half-open (SYN) Scan
  - Inverse TCP Flag Scans:
    - Xmas Scan (FIN, URG, PSH Flags)
    - FIN Scan
    - NULL Scan
    - Maimon Scan
  - ACK Flag Probe Scans:
    - TTL-Based Scan
    - Window-Based Scan

- **Third Party and Spoofed TCP Scanning:**
  - IDLE/IP ID Header Scan

### UDP Scanning

- UDP Scanning

### SCTP Scanning

- SCTP (Stream Control Transmission Protocol) ist ein Transportprotokoll mit erweiterten Funktionen wie Multi-Homing und Multi-Streaming.
- SCTP Scanning nutzt spezielle SCTP-Nachrichten (z. B. INIT, COOKIE-ECHO), um offene SCTP-Ports zu erkennen.
- **SCTP INIT Scanning:** Sendet INIT-Anfragen, um Verbindungen zu initiieren und offene Ports zu identifizieren.
- **SCTP COOKIE/ECHO Scanning:** Sendet COOKIE-ECHO Nachrichten zur Verbindungsbestätigung.
- Wichtig für Netzwerke, die SCTP verwenden (z. B. Telekommunikationsinfrastruktur).

### SSDP Scanning

- SSDP and List Scanning

### IPv6 Scanning

- IPv6 Scanning

---

## Erläuterungen zu Scan-Methoden

### TCP Connect/Full-Open Scan

- Betriebssystem öffnet vollständige TCP-Verbindung (3-Wege-Handshake).
- Erfolgreiche Verbindung zeigt offenen Port.
- Nach Abschluss des Handshakes wird Verbindung durch RST beendet.
- Sehr zuverlässig, aber leicht durch IDS erkennbar.

### Stealth Scan (Half-Open / SYN Scan)

- Sendet nur SYN-Paket.
- Ziel antwortet mit SYN/ACK bei offenem Port, RST bei geschlossenem.
- Scanner sendet danach RST, um Verbindung abzubrechen, ohne vollständigen Handshake.
- Vermeidet Protokollierung in vielen Systemen (stealthy).

### Inverse TCP Flag Scans

- TCP-Pakete mit ungewöhnlichen Flag-Kombinationen (FIN, URG, PSH, NULL).
- Offene Ports reagieren meist nicht.
- Geschlossene Ports senden RST.
- Beispiele:
  - **Xmas Scan**: FIN, URG, PSH Flags gesetzt.
  - **FIN Scan**: Nur FIN Flag gesetzt.
  - **NULL Scan**: Keine Flags gesetzt.
- Effektiv nur gegen BSD-basierte TCP/IP-Stacks, meist nicht gegen Windows.

### TCP Maimon Scan

- Ähnlich zu NULL, FIN, Xmas, verwendet FIN/ACK Pakete.
- Kein Antwort = offen/filtered; RST Antwort = geschlossen.

### ACK Flag Probe Scan

- Sendet ACK-Pakete.
- Analysiert TTL und Window-Feld in empfangenen RST-Paketen.
- Effektiv gegen BSD-TCP/IP-Stacks.

#### TTL-Based ACK Flag Probe Scan

- TTL-Wert < 64 im RST zeigt offenen Port.
- Beispiel: Port 22 mit TTL 50 = offen.

#### Window-Based ACK Flag Probe Scan

- Fensterwert (Window) im RST-Paket > 0 = Port offen.
- Wird genutzt, wenn TTL bei allen Paketen gleich ist.

---

## 5. Tools und Optionen (Zenmap / Nmap)

| Scan-Typ                | Nmap-Option         |
|-------------------------|---------------------|
| Xmas Scan               | `-sX`               |
| FIN Scan                | `-sF`               |
| NULL Scan               | `-sN`               |
| Maimon Scan             | `-sM`               |
| Window-Based ACK Scan   | `-sW`               |
| TTL-Based ACK Scan      | `nmap --ttl [time]` |

---

## Vor- und Nachteile der Scan-Methoden

| Scan-Methode           | Vorteile                                | Nachteile                             |
|-----------------------|-----------------------------------------|-------------------------------------|
| TCP Connect Scan      | Sehr zuverlässig                        | Leicht von IDS erkannt               |
| Stealth (SYN) Scan    | Weniger auffällig, kein kompletter Handshake | Benötigt Zugriff auf rohe Sockets, Adminrechte |
| Inverse TCP Flag Scan | Vermeidet IDS, sehr stealthy             | Funktioniert nur bei BSD-Systemen, nicht bei Windows |
| ACK Flag Probe Scan   | Erkennt offene Ports durch Header-Analyse | Nur bei BSD-basierten TCP/IP-Stacks effektiv |

---

# IDLE/IPID Header Scan

- **Beschreibung:**  
  TCP-Port-Scan, der den IP Identifier (IPID) eines „Zombie“-Hosts ausnutzt, um offene Ports auf einem Zielsystem zu erkennen.  
  Der Angreifer spoofed die IP-Adresse des Zombies und sendet SYN-Pakete an das Ziel.  
  Das Ziel antwortet (je nach Portstatus) und beeinflusst den IPID-Zähler des Zombies.  
  Der Angreifer beobachtet Änderungen am IPID des Zombies, um offene Ports zu identifizieren.

- **Ablauf:**  
  1. Wähle einen geeigneten Zombie mit inkrementellem globalem IPID.  
  2. Ermittle die aktuelle IPID des Zombies (Baseline).  
  3. Sende SYN-Paket an Ziel mit gefälschter Zombie-IP.  
  4. Beobachte IPID-Anstieg des Zombies:  
     - +2 → Port offen  
     - +1 → Port geschlossen  
     - Keine Änderung → Port gefiltert

- **Zenmap Beispiel:**  
  ```bash
  nmap -sI <Zombie-IP> <Ziel-IP>

---


# UDP Scan

- **Beschreibung:**
UDP-Scan verwendet das verbindungslose UDP-Protokoll, um Ports zu prüfen.
Da UDP keine Antwort garantiert, wird das Fehlen einer Antwort als offen oder gefiltert interpretiert.
Antwortet ein Port mit ICMP Port Unreachable, ist er geschlossen.

- **Eigenschaften:**
- Kein Drei-Wege-Handshake.
- UDP-Scans sind langsamer, da ICMP-Fehlermeldungen oft gedrosselt werden (RFC 1812).
- Root-Rechte meist notwendig.
- Pakete werden retransmittiert, um Paketverluste zu kompensieren.

**Zenmap Beispiel:**
  ```bash
  nmap -sU <Ziel-IP>


#UDP RECVFROM() und WRITE() Scan

**Beschreibung:**  
Nicht-root-User können ICMP-Fehler nicht direkt auslesen, nutzen aber indirekte Signale über `recvfrom()` und `write()` Systemcalls.  
Windows-Betriebssysteme drosseln ICMP meist nicht, was effizientere Scans ermöglicht.

**Beispiel:**  
Tools wie Netcat oder Pluvials pscan.c nutzen diese Technik.

---

# SCTP INIT Scan

**Was ist SCTP?**  
Stream Control Transmission Protocol ist ein zuverlässiges, nachrichtenorientiertes Transportprotokoll, ähnlich TCP/UDP.  
Unterstützt Multi-Homing und Multi-Streaming. Wird u.a. bei VoIP und SS7/SIGTRAN verwendet.

**Scan-Prinzip:**  
- Sendet INIT chunk an Zielport.  
- Antwort: INIT+ACK (offen), ABORT (geschlossen), keine Antwort oder ICMP unreachable (gefiltert).  
- Stealthy, da keine vollständigen Verbindungen aufgebaut werden.

**Zenmap Beispiel:**  
```bash
nmap -sY <Ziel-IP>

## SCTP COOKIE ECHO Scan

**Beschreibung:**  
Fortschrittlicher SCTP Scan.

- Sendet COOKIE ECHO chunk.  
- Offene Ports verwerfen das Paket still (keine Antwort).  
- Geschlossene antworten mit ABORT.  
- Nur schwer von IDS erkennbar.  
- Keine Unterscheidung zwischen offen und gefiltert möglich.

**Zenmap Beispiel:**  
```bash
nmap -sZ <Ziel-IP>
```

---

## SSDP Scan

**Was ist SSDP?**  
Simple Service Discovery Protocol ist ein Protokoll, das UPnP-fähige Geräte über IPv4/IPv6 Multicast entdeckt.

**Scan-Einsatz:**  
- Ermittelt UPnP-Geräte im Netzwerk.  
- Kann Schwachstellen wie Buffer Overflow oder DoS aufdecken.

**Zenmap Beispiel:**  
```bash
nmap --script=upnp-info <Ziel-IP>
```

---

## List Scan

**Beschreibung:**  
List Scan generiert eine Liste von IP-Adressen oder Hostnamen ohne tatsächliches Pingen oder Scannen.  
Reverse DNS wird durchgeführt, um Namen zu ermitteln.  
Hilfreich für schnelle Prüfung und Erkennung von falsch konfigurierten IP-Adressen.

**Zenmap Beispiel:**  
```bash
nmap -sL 192.168.1.0/24
```

---

## IPv6 Scan

**Beschreibung:**  
IPv6-Adressen sind 128 Bit lang, was herkömmliche Scans wegen des enormen Adressraums praktisch unmöglich macht.  
Angreifer sammeln IPv6-Adressen meist aus Netzwerkverkehr, Logs oder E-Mails.

**Zenmap Beispiel:**  
```bash
nmap -6 2001:db8::/64
```

---

## Port Scanning mit KI

**Beispiele für Prompts an ChatGPT:**  
- „Perform stealth scan on target IP 10.10.1.11 and display the results“  
- „Perform an XMAS scan on target IP 10.10.1.11“  
- „Use Nmap to scan open ports and services against IPs in scan1.txt and output port, service, version info to scan3.txt“  
- „Use Metasploit to discover open ports on the IP address 10.10.1.22“

---

## XMAS Scan

**Beschreibung:**  
Sendet TCP-Pakete mit FIN, URG und PSH Flags gesetzt.  
Testet Reaktion des Ziels auf ungewöhnliche Pakete.

**Beispiel:**  
```bash
nmap -sX <Ziel-IP>
```

---

## Automatisierte Nmap-Scans mit Filterung

**Beispiel:**  
Scan einer IP-Liste mit Versionserkennung und Filterung auf offene Ports, Ausgabe in Datei:  
```bash
nmap -sV -iL scan1.txt --open | awk '/Nmap scan report for/{ip=$NF}/^[0-9]+\/tcp/{print ip " : " $0}' > scan3.txt
```

---

## Metasploit TCP Port Scan

**Beispiel:**  
Automatisierter TCP-Portscan via Metasploit-Konsole im Quiet Mode:  
```bash
msfconsole -q -x "use auxiliary/scanner/portscan/tcp; set RHOSTS 10.10.1.22; run; exit"
```

---

## Service Version Discovery

**Beschreibung:**  
Erkennung von Diensten und Versionen auf Zielsystemen, um gezielt Exploits auswählen zu können.  
Nutzt Nmap service-probes Datenbank für genaue Erkennung.

**Beispiel:**  
```bash
nmap -sV --reason -v -sT 10.10.1.11
```

---

## Nmap Scan Time Reduction Techniques

- Nicht-kritische Tests auslassen, nur benötigte Ports scannen.  
- Timing mit `-T` (1 bis 5) anpassen.  
- UDP-Scans separat durchführen.  
- Nmap aktuell halten wegen Bugfixes und neuen Features.  
- Parallele Scans und Gruppenbildung bei großen Netzen.  
- Vom internen Netzwerk scannen, wenn möglich.  
- Bandbreite und CPU-Ressourcen erhöhen zur Scan-Beschleunigung.


## Banner Grabbing / OS Fingerprinting

- **Definition:** Methode zur Bestimmung des Betriebssystems eines entfernten Systems.
- **Zweck:** Wissen über OS erhöht die Wahrscheinlichkeit erfolgreicher Angriffe.
- **Methoden:**
  - Auslesen von Bannern beim Verbindungsaufbau (z.B. FTP-Banner).
  - Herunterladen von Binärdateien zur Architekturprüfung.
  - Stack-Querying: Senden von Paketen und Auswertung der Antworten.
  - Initial Sequence Number (ISN) Analyse: Erkennung von Zufallszahlgeneratoren in TCP-Stacks.
  - ICMP-Response Analyse: Senden von ICMP-Nachrichten und Auswertung.

### Active Banner Grabbing

- Sendet speziell formatierte TCP/UDP Pakete an den Host.
- Vergleicht Antworten mit einer OS-Datenbank.
- Beispiel: Nmap führt 9 Tests durch, u.a. SYN + ECN-Echo, NULL-Pakete, URG/PSH/SYN/FIN Flags, UDP an geschlossenen Ports, TCP Sequence Ability Test.
- Erkennung der TCP Initial Sequence Number (ISN) Muster zur OS-Klassifikation.
- Verschiedene OS-Klassen: Alte UNIX, Solaris, Linux, Windows (zeitabhängige ISN).

### Passive Banner Grabbing

- Kein aktives Scannen, sondern Abfangen (Sniffing) von Paketen.
- Analyse von Fehlermeldungen, Netzwerkverkehr und URL-Erweiterungen.
- Typische passive OS-Signaturen:
  - TTL (Time To Live)
  - TCP Window Size
  - DF (Don’t Fragment) Bit
  - TOS (Type of Service)
- Kombination mehrerer Signaturen erhöht Genauigkeit.
- Beispiel Paket-Analyse:
  - TTL: 45
  - Window Size: 0x7D78 (32120 dezimal)
  - DF-Bit: gesetzt
  - TOS: 0x0

### Limitierungen passiver Fingerprinting

- Tools, die eigene Pakete erzeugen, zeigen andere Signaturen.
- TTL, Window Size, DF, TOS können vom Ziel manipuliert werden.
- Passive Fingerprinting kann Proxy Firewalls und Rogue Systeme erkennen.
- Stealth Fingerprinting durch Auswertung normaler Web-Requests möglich.

---

## OS Erkennung über Netzwerkprotokolle

| Betriebssystem | TTL  | TCP Window Size             |
|----------------|------|----------------------------|
| Linux          | 64   | 5840                       |
| FreeBSD        | 64   | 65535                      |
| OpenBSD        | 64   | 16384                      |
| Windows        | 255  | 65535                      |
| Cisco Router   | 128  | 4128                       |
| Solaris        | 255  | 8760                       |
| AIX            | 255  | 16384                      |

- TTL und Window Size sind wichtige Indikatoren zur OS-Erkennung.

---

## Tools zur OS-Erkennung

### Wireshark

- Paket-Sniffer zum Erfassen von Antwortpaketen.
- Analyse von TTL und TCP Window Size im ersten TCP-Paket.
- Vergleich mit bekannten OS-Signaturen.

### Nmap

- OS-Erkennung mit Parameter `-O` (Zenmap GUI).
- Zeigt Betriebssystemdetails des Zielhosts.
- Sehr verbreitet und effektiv.

### Unicornscan

- Analyse der TTL-Werte aus Scan-Ergebnissen.
- Beispiel: TTL 128 deutet auf Windows hin.
- Syntax: `unicornscan <target IP>`

### Nmap Script Engine (NSE)

- Automatisiert Netzwerkaufgaben mit Scripts.
- Beispielscript `smb-os-discovery` für OS-Erkennung via SMB.
- Standard-Skripte mit `-sC`, eigene mit `--script`.
- Ausgabe in normalem und XML-Format.

### IPv6 Fingerprinting

- Ähnlich wie IPv4 Fingerprinting, aber mit IPv6-spezifischen Probes.
- Nmap sendet ca. 18 Probes: Sequence generation (S1–S6), ICMPv6 echo (IE1, IE2), Node Info Query (NI), Neighbor Solicitation (NS), UDP (U1), TCP TECN, TCP (T2–T7).
- Befehl: `nmap -6 -O <target>`

### OS-Erkennung mit KI

- KI (z.B. ChatGPT) unterstützt bei Automatisierung und Verbesserung der OS-Erkennung.
- KI kann TTL-Ping, Nmap Script Engine und andere Tools anleiten.

---

### Beispiele für OS-Erkennung mit TTL-Ping

```bash
ping -c 1 10.10.1.11 && echo "Check the TTL value from the response to infer the OS (Linux/Unix: 64, Windows: 128)"

- Sendet einen Ping.
- TTL 64 → Linux/Unix, TTL 128 → Windows.

```bash
ping -c 1 10.10.1.9 | grep "ttl"

- Ping mit Ausgabe gefiltert auf TTL.

Beispiel Nmap Script Engine OS-Erkennung auf mehreren Zielen

```bash
nmap -iL scan1.txt -O --script=default --script-args=newtargets -oN os_discovery_results.txt

- -iL scan1.txt: Ziele aus Datei.
- -O: OS-Erkennung.
- --script=default: Standard-Skripte.
- --script-args=newtargets: Genauigkeit erhöhen.
- -oN: Ausgabe in Datei.

### Automatisierung von Netzwerkscans mit Bash-Skript

```bash
#!/bin/bash
# Ping Scan im Subnetz
nmap -sP 10.10.1.0/24 -oG - | awk '/Up$/{print $2}' > live_hosts.txt
# Service- und Versionserkennung der aktiven Hosts
nmap -iL live_hosts.txt -sV -oA scan_results
# Ausgabe der Ergebnisse
cat scan_results.nmap

- Findet aktive Hosts.
- Scannt offene Ports und Dienstversionen.
- Speichert Ergebnisse in mehreren Formaten.

### Erklärung Bash-Skript

- nmap -sP: Ping Scan zur Erkennung lebender Hosts.
- -oG -: Ausgabe im grepbaren Format.
- awk '/Up$/{print $2}': Filtert IP-Adressen.
- nmap -sV: Dienst- und Versionserkennung.
- -oA scan_results: Ergebnisse in verschiedenen Formaten.
- cat scan_results.nmap: Zeigt Ergebnisse an.


