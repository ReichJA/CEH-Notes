# Sniffing Cheatsheet – Techniken, Tools & Gegenmaßnahmen
**Stand:** 17.05.2025

---

## 📘 Kapitelübersicht

1. Sniffing Concepts  
2. MAC Sniffing  
3. DHCP Attacks  
4. ARP Poisoning  
5. Spoofing Attacks  
6. DNS Poisoning  
7. Sniffing Tools  
8. Sniffing Countermeasures (Platzhalter – STPÜ wird noch spezifiziert)

---

## 📘 1. Sniffing Concepts

### 🔍 Erklärung:
Sniffing bezeichnet das Überwachen und Abfangen von Datenpaketen, die sich durch ein Netzwerk bewegen. Es wird genutzt zur Fehlersuche, Netzwerkdiagnose – oder von Angreifern zum Auslesen sensibler Daten.

### 🧪 Beispiel:
Ein Sniffer wie Wireshark fängt HTTP-Pakete ab. In einem unverschlüsselten Netzwerk kann der Angreifer damit Login-Daten sehen:
```
GET /login.php?user=admin&pass=123456
```

- Sniffing = Abfangen von Datenpaketen auf Layer 2/3.
- **Shared Ethernet**: Verkehr wird an alle Hosts gesendet → passives Sniffing möglich.
- **Switched Ethernet**: Switch leitet Verkehr gezielt anhand der CAM-Tabelle weiter.
- **ARP-Spoofing** & **MAC-Flooding** unterlaufen Switches.
- Tools: `macof`, `dsniff`, Wireshark.

---

## 📘 2. MAC Sniffing

### 🔍 Erklärung:
MAC Sniffing fokussiert sich auf die Identifikation und Manipulation von MAC-Adressen im Netzwerk. Es wird genutzt, um Traffic gezielt umzuleiten.

### 🧪 Beispiel:
Ein Angreifer nutzt `macof`, um 100.000 MAC-Adressen in die CAM-Tabelle eines Switches zu fluten:
```
macof -i eth0
```
Ergebnis: Switch broadcastet Traffic → Sniffing möglich.

- **MAC-Adresse** = 48-Bit-Adresse: 24 Bit Hersteller (OUI), 24 Bit Seriennummer.
- **CAM-Tabelle**: Switch-Zuordnung MAC → Port.
- **Angriffe:**
  - **MAC Flooding**: CAM-Tabelle überfüllen → Switch agiert wie Hub.
  - **Switch Port Stealing**: ARP-Race-Condition zur Port-Übernahme.
- Tool: `macof`, `dsniff`

---

## 📘 3. DHCP Attacks

### 🔍 Erklärung:
DHCP weist automatisch IP-Adressen zu. Angreifer können dies ausnutzen, um IPs zu blockieren (Starvation) oder Opfer auf einen Rogue-DNS zu leiten.

### 🧪 Beispiel:
Ein Angreifer sendet hunderte DHCPREQUESTs mit gefälschten MACs:
```
python dhcpStarvation.py
```

- **DHCP Starvation**: IP-Pool durch gefälschte MAC-Adressen erschöpfen → DoS.
- **Rogue DHCP Server**: Bösartiger Server liefert falsche Konfiguration.
- Tools: `Yersinia`, `DHCPig`, `Gobble`, `Metasploit`, `dhcpStarvation.py`, `Ettercap`

---

## 📘 4. ARP Poisoning

### 🔍 Erklärung:
Durch gefälschte ARP-Replies kann ein Angreifer sich als Gateway ausgeben und MITM-Angriffe durchführen.

### 🧪 Beispiel:
```
arpspoof -i eth0 -t 192.168.0.10 192.168.0.1
arpspoof -i eth0 -t 192.168.0.1 192.168.0.10
```
Ergebnis: Der Traffic zwischen Client und Router läuft über den Angreifer.

- ARP ist zustandslos → keine Authentifizierung.
- **ARP Spoofing**: Falsche Zuordnung von IP ↔ MAC.
- Ermöglicht MITM, Session Hijacking, Passwortdiebstahl.
- Tools: `arpspoof`, `ettercap`, `bettercap`, `larp`, `RITM`, `Habu`, `Cain & Abel`

---

## 📘 5. Spoofing Attacks

### 🔍 Erklärung:
Spoofing bedeutet, sich als ein anderer im Netzwerk auszugeben – etwa durch MAC oder IP-Adressen.

### 🧪 Beispiel (MAC-Spoofing unter Linux):
```
ifconfig eth0 down
macchanger -m 00:11:22:33:44:55 eth0
ifconfig eth0 up
```

- **MAC Spoofing**: Angreifer übernimmt fremde Identität durch MAC-Fälschung.
- Windows-Spoofing über Netzwerkadapter-Einstellungen oder Registry.
- Tools: `SMAC`, `Technitium MAC`, `macchanger`, `AMC`, `Change MAC Address`, `MAC Address Changer`

---

## 📘 6. DNS Poisoning

### 🔍 Erklärung:
DNS Poisoning täuscht einer Anwendung falsche IP-Adressen für Domainnamen vor. Ziel ist meist Phishing, Umleitung oder Kontrolle über Traffic.

### 🧪 Beispiel:
Ein infizierter Rechner nutzt als primären DNS-Server die IP des Angreifers. `www.bank.de` → 10.0.0.66 → Angreiferseite.

- DNS → Domainauflösung.
- **Angriffstypen:**
  - Intranet DNS Spoofing (ARP + DNS Manipulation im LAN)
  - Internet DNS Spoofing (Trojaner ersetzt DNS-Eintrag)
  - Proxy DNS Poisoning
  - DNS Cache Poisoning
- Ziel: Umleitung auf gefälschte Server → Phishing, MITM, Malware

---

## 📘 7. Sniffing Tools

### 🔍 Erklärung:
Sniffing-Tools erfassen, analysieren und dekodieren Netzwerkverkehr. Sie sind in legitimen wie kriminellen Kontexten einsetzbar.

### 🧪 Beispiel (Wireshark):
1. Filter setzen: `http.request.method == "POST"`
2. Analyse: Zugangsdaten, Cookies, Klartext-Inhalte sichtbar machen

- **Wireshark**: GUI, Filter, Analyse (Ethernet, WLAN, USB etc.)
- **Capsa**: Business-Netzwerküberwachung (GUI)
- **OmniPeek**: Echtzeitanalyse, Geo-IP via Maps
- **Xplico**: Extrahiert Inhalte aus .pcap (HTTP, VoIP etc.)
- **RITA**: Beaconing Detection für C2-Verkehr
- **PRTG**, **SolarWinds**, **Observer Analyzer**: Performance Monitoring

---

## 📘 8. Sniffing Countermeasures (STPÜ*)

### 🔍 Erklärung:
Schutzmaßnahmen gegen Sniffing wirken auf mehreren Ebenen – durch Netzwerkkonfiguration, Authentifizierung und Verschlüsselung.

### 🛡 Beispiele:
- **Port Security:** Max. 1 MAC pro Port erlaubt
- **DHCP Snooping:** Legitimen DHCP-Verkehr kontrollieren
- **802.1X / NAC:** Authentifizierung pro Port erzwingen
- **TLS / HTTPS:** Verschlüsselt HTTP-Kommunikation → Sniffing sinnlos
- **VLAN-Trennung:** Angreifer sitzt in isoliertem Netz

*STPÜ wurde nicht spezifiziert – vermutete Inhalte:*

- **STP aktivieren (Spanning Tree Protocol)**: verhindert MAC-Flooding-Loops
- **Port-Security**: Begrenzung erlaubter MAC-Adressen pro Port
- **DHCP Snooping**: blockiert Rogue-DHCP-Server
- **Dynamic ARP Inspection (DAI)**: verhindert ARP-Spoofing
- **VLAN-Segmentierung**: isoliert sensible Netzbereiche
- **Verschlüsselung**: TLS, SSH, VPN gegen Sniffing auf Layer 3

---

© 17.05.2025 – Zusammenstellung durch ChatGPT für JR | Alle Angaben ohne Gewähr.
