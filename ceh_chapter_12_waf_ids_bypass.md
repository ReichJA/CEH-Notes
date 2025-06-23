# Techniken zur Umgehung von IDS/Firewall/WAF

Diese Datei fasst verschiedene Methoden zur Umgehung von Intrusion Detection Systems (IDS), Firewalls und Web Application Firewalls (WAF) zusammen. Die Techniken sind thematisch sortiert und enthalten Erklärungen, Beispiele und Tools.

---

## 🔍 1. Port Scanning
**Beschreibung:**  
Systematisches Scannen von Netzwerkports, um offene Ports und laufende Dienste zu identifizieren.

**Ziel:**  
Schwachstellen aufdecken, Einstiegspunkte finden.

**Beispieltools:** `nmap`, `masscan`

**Typischer Ablauf:**
- Senden von Paketen an verschiedene Ports
- Analyse der Antworten
- Identifikation von Diensten & Versionen

---

## 🔥 2. Firewalking
**Beschreibung:**  
Verfahren zur Analyse von Firewall-Regeln durch gezieltes TTL-Manipulieren (ähnlich Traceroute).

**Ziel:**  
Erkennen, welche Protokolle/Ports von der Firewall durchgelassen werden.

**Tool:** `firewalk`, `nmap --script=firewalk.nse`

---

## 🏷️ 3. Banner Grabbing
**Beschreibung:**  
Auslesen von Dienstinformationen durch einfache Verbindungen zu offenen Ports (z. B. mit Telnet, Netcat).

**Beispiel:**  
```bash
telnet target.com 25
```

**Ziel:**  
Versionen und Schwachstellen ermitteln.

---

## 🧻 4. IP Address Spoofing
**Beschreibung:**  
Fälschen der Absender-IP-Adresse, um vertrauenswürdige Identität vorzutäuschen.

**Ziel:**  
Zugriff auf geschützte Systeme, Umgehung von Quell-IP-Filtern.

**Tool:** `hping3 -a <gefälschte IP>`

---

## 🗺️ 5. Source Routing
**Beschreibung:**  
Angreifer bestimmt den Pfad der Pakete durch das Netzwerk, um unsichere oder unüberwachte Pfade auszunutzen.

**Typen:**
- Loose Source Routing
- Strict Source Routing

---

## 🧩 6. Tiny Fragments
**Beschreibung:**  
Zerlegen von Paketen in extrem kleine Fragmente, um IDS-Analyse zu umgehen.

**Tool:** `fragroute`

---

## 🌐 7. DNS Tunneling
**Beschreibung:**  
Verstecken von Nutzdaten in DNS-Anfragen/-Antworten.

**Tools:** `iodine`, `dnscat2`

**Ziel:**  
Datenübertragung durch Port 53 ohne Firewall-Erkennung.

---

## 📨 8. ICMP Tunneling
**Beschreibung:**  
Tunneln von Nutzdaten in ICMP Echo Requests (z. B. ping).

**Tool:** `ICMPTX`

---

## 📦 9. ACK Tunneling
**Beschreibung:**  
Verwendung von ACK-Paketen (die weniger überprüft werden), um Daten verdeckt zu übertragen.

**Tool:** `hping3`

---

## 🌍 10. HTTP Tunneling
**Beschreibung:**  
Verpackung beliebiger Nutzdaten in HTTP-Anfragen (meist über Port 80).

**Tools:** `HTTPTunnel`, `Tunna`

---

## 🔒 11. SSH Tunneling
**Beschreibung:**  
Verwenden von verschlüsselten SSH-Tunneln zum Umgehen von Firewall-Regeln.

**Tools:** `ssh -L`, `Bitvise`

---

## 🧠 12. Durch externe Systeme
**Beschreibung:**  
Einfallstor über zugelassene Remote- oder Home-Systeme (z. B. über Session Hijacking, OpenURL-Tricks).

---

## 🕵️ 13. MITM über DNS Spoofing
**Beschreibung:**  
Man-in-the-Middle-Angriff über DNS-Manipulation (z. B. DNS Poisoning).

**Ziel:**  
Tarnung des Angriffs als legitimer Datenverkehr.

---

## 🎭 14. Schadcode im Inhalt (Content-based)
**Beschreibung:**  
Einbettung von Schadcode in legitimen Dateien (Office, PDF, AutoCAD usw.)

**Techniken:**
- Steganografie
- Obfuskation
- Makro-Exploits

---

## 💡 15. XSS-BYPASS-TECHNIKEN

### ▪ ASCII-Encoding
```html
<script>String.fromCharCode(97,108,101,114,116,40,34,88,83,83,34,41)</script>
```

### ▪ Hex-Encoding
```html
%3C%73%63%72%69%70%74%3E%61%6C%65%72%74%28%22%58%53%53%22%29%3C%2F%73%63%72%69%70%74%3E
```

### ▪ Obfuskation
```html
<sCRiPt>aLeRT("XSS")</sCriPT>
```

---

## 🔤 16. HTTP Header Spoofing
**Ziel:**  
Tarnung als interner Host durch Header wie:
```
X-Forwarded-For: 127.0.0.1
X-Remote-IP: 127.0.0.1
```

**Tools:** `Burp Suite`, `curl`

---

## 🧪 17. Blacklist Detection Bypass
**Ziel:**  
Erkennen und Umgehen von WAF-Blacklist-Keywords (z. B. `script`, `alert`, `union`).

**Techniken:**  
- Payloads umformen (z. B. `GROUP BY HAVING` statt `WHERE`)
- Regex-freundliche Codierung

---

## 🔁 18. Fuzzing & Brute-Force gegen WAF
**Tools:**  
- [`ffuf`](https://github.com/ffuf/ffuf)
- [`wfuzz`](https://github.com/xmendez/wfuzz)
- [`SecLists`](https://github.com/danielmiessler/SecLists)

**Ziel:**  
Funktionierende Payloads durch Massentests identifizieren.

---

## 🔐 19. SSL/TLS Cipher Bypass
**Ziel:**  
Verbindung über Cipher-Suites, die **vom Webserver**, aber **nicht von der WAF unterstützt** werden.

**Tools:**  
- `sslscan2`
- `curl --ciphers`
- `abuse-ssl-bypass-waf.py`

---

*Diese Datei dient ausschließlich Bildungs- und Testzwecken in sicheren Testumgebungen.*