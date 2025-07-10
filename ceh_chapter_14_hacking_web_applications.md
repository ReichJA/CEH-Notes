# Module 14: Hacking Web Applications

## Lernziele

Am Ende dieses Moduls wirst du in der Lage sein:

- Webanwendungskonzepte zu beschreiben
- Verschiedene Angriffe auf Webanwendungen durchzuführen
- Die Methodik des Web Application Hacking zu beschreiben
- Verschiedene Tools zum Hacken von Webanwendungen zu nutzen
- Web-API- und Webhook-Konzepte zu erklären
- Zu verstehen, wie Webanwendungen über Web-APIs gehackt werden können

---

## Einführung in Webanwendungen

Webanwendungen sind Softwareprogramme, die in Webbrowsern laufen und als Schnittstelle zwischen Benutzern und Webservern über Webseiten dienen. Sie ermöglichen es den Benutzern, über eine benutzerfreundliche grafische Oberfläche (GUI) Daten zu senden, anzufordern und zu empfangen. Eingaben erfolgen über Tastatur, Maus oder Touch, abhängig vom Gerät.

Webanwendungen verwenden browserunterstützte Programmiersprachen wie:
- JavaScript
- HTML
- CSS  
und arbeiten oft mit SQL zur Datenbankanbindung.

Sie werden als dynamische Webseiten entwickelt und ermöglichen u.a.:
- Suchen
- E-Mails versenden
- Online-Shopping
- Verfolgung und Nachverfolgung

---

## Vorteile von Webanwendungen

- **Betriebssystemunabhängig**: Einfache Entwicklung und Wartung
- **Zugänglich überall mit Internetverbindung**
- **Anpassbare Benutzeroberfläche**
- **Plattformunabhängig**: Zugriff über PDAs, Smartphones etc.
- **Zentrale Verwaltung auf dedizierten Servern**
- **Verteilte Serverstandorte erhöhen Sicherheit**
- **Nutzung flexibler Technologien** wie JSP, Servlets, .NET, SQL Server

> ⚠️ Trotz Sicherheitsrichtlinien sind Webanwendungen anfällig für Angriffe wie:
> - SQL-Injection
> - Cross-Site-Scripting (XSS)
> - Session Hijacking

---

## Web Services

Ein Webdienst (Web Service) ist eine Anwendung, die über das Internet bereitgestellt wird. Er nutzt standardisierte Protokolle (z. B. SOAP), um plattformübergreifende Kommunikation zu ermöglichen.

**Beispiel:** Java-basierte Services interagieren mit PHP-Anwendungen.

Typische Standards:
- SOAP
- REST
- WSDL
- UDDI

---

### Web Service Architektur

Die Architektur besteht aus 3 Rollen:

- **Service Provider**: Bietet den Dienst an
- **Service Requester**: Fordert den Dienst an (z. B. ein Browser)
- **Service Registry**: Registriert und verwaltet Dienstbeschreibungen

---

### 3 Operationen der Webservice-Architektur

- **Publish**: Dienstbeschreibung wird veröffentlicht
- **Find**: Dienstbeschreibung wird gesucht
- **Bind**: Kommunikation mit dem Dienst wird hergestellt

---

### 2 Artefakte im Webservice

- **Service**: Softwaremodul, das den Dienst bereitstellt
- **Service Description**: Enthält Schnittstellen-, Netzwerk-, und Bindungsinformationen

---

### Ablaufdiagramm

```text
    [Service Provider]
           |
      (Publish WSDL)
           |
     v           ^
[Service Registry] <--- (Find WSDL) --- [Service Requester]
           |
        (Bind)
           v
    [Service Provider]
```

## Web Service Typen

### SOAP Web Services
- Nutzen das XML-Format zum Datenaustausch zwischen Service Provider und Requester
- Ermöglichen plattformübergreifenden Austausch zwischen Programmiersprachen
- Bauen auf dem Simple Object Access Protocol (SOAP) auf

### RESTful Web Services
- Nutzen HTTP-Konzepte (z. B. GET, POST)
- Architekturansatz, kein Protokoll
- REST = Representational State Transfer

## Komponenten der Web Service Architektur

- **UDDI**: Verzeichnisdienst für verfügbare Services
- **WSDL**: XML-basierte Beschreibung von Webdiensten
- **WS-Security**: Sicherheitsstandard für SOAP zur Wahrung von Integrität und Authentizität

---

## Angriffsvektoren nach Netzwerk-Schichten

### Layer 7: Anwendungsschicht
- Schwächen in Businesslogik (z. B. .NET, Java)
- XSS durch fehlende Input-Validierung

### Layer 6: Präsentationsschicht
- Angriffe über Drittanbieter (z. B. Zahlungs-Gateways)

### Layer 5: Sitzungsschicht
- Footprinting von Webservern (Banner Grabbing)
- Nutzung der CVE-Datenbank

### Layer 4: Transportschicht
- Datenbankangriffe (z. B. sqlmap)

### Layer 3: Netzwerkschicht
- Malware über offene Ports
- Viren/Backdoors

### Layer 2: Sicherungsschicht
- Switch-Flooding (CAM-Tabelle)
- Sniffing von Daten

### Layer 1: Bitübertragungsschicht
- IDS/IPS umgehen mittels Evasion-Techniken

---

## OWASP Top 10 Sicherheitslücken

### A01 – Broken Access Control
- Fehlende Zugriffsbeschränkungen bei Authentifizierung
- Angriffe:
  - Directory Traversal
  - Hidden Field Manipulation

### A02 – Cryptographic Failures
- Schwache oder fehlende Verschlüsselung
- Angriffe:
  - Cookie Snooping
  - RC4 NOMORE Attack
  - Same-Site Attack
  - Pass-the-Cookie Attack

### A03 – Injection
- Einschleusen von Befehlen (SQL, LDAP, XSS, etc.)
- Angriffe:
  - SQL Injection
  - Command Injection
  - LDAP Injection
  - XSS
  - Buffer Overflow

### A04 – Insecure Design
- Fehlendes Sicherheitskonzept im Design
- Angriffe:
  - Business Logic Bypass
  - Timing Attacks
  - CAPTCHA Attacks
  - Platform Exploits

### A05 – Security Misconfiguration
- Fehlkonfiguration von Systemen und Komponenten
- Angriffe:
  - XXE
  - Unvalidated Redirects
  - Directory Traversal
  - Hidden Field Manipulation

### A06 – Vulnerable and Outdated Components
- Nicht gepatchte oder veraltete Softwarekomponenten
- Angriffe:
  - Platform Exploits
  - Magecart Attack
  - Buffer Overflow

### A07 – Identification and Authentication Failures
- Schwache Authentifizierungsmechanismen
- Angriffe:
  - CSRF
  - Cookie/Session Poisoning
  - Cookie Snooping

### A08 – Software and Data Integrity Failures
- Unsichere Updates, fehlende Integritätsprüfungen
- Angriffe:
  - Insecure Deserialization
  - Watering Hole Attack
  - DoS
  - Web Service Attacks
  - Magecart Attack

### A09 – Security Logging and Monitoring Failures
- Fehlende oder unzureichende Protokollierung
- Angriff:
  - Web Service Attacks

### A10 – Server-Side Request Forgery (SSRF)
- Server fordert Daten von internen Ressourcen ohne Prüfung an
- Angriffe:
  - SSRF Payload Injection
  - XSPA
  - DNS Rebinding
  - H2C Smuggling

---

# Web Application Attacks – Übersicht & Beispiele

---

## 1. Directory Traversal
**Ziel des Angriffs:** Zugriff auf sensible Dateien wie:

- `/etc/passwd` (unter Linux)
- `C:\Windows\System32\config\SAM` (unter Windows)
- Konfigurationsdateien mit Zugangsdaten

## Wie funktioniert der Angriff?

Viele Webanwendungen laden Dateien basierend auf Benutzereingaben (z. B. `GET /view.php?file=report.pdf`). Wenn diese Eingabe nicht korrekt gefiltert wird, kann ein Angreifer Pfade wie `../../../../etc/passwd` einfügen, um sich durch das Dateisystem „hochzunavigieren“.

### Beispiel-URL:
```
http://example.com/view.php?file=../../../../etc/passwd
```

Wenn das Skript `file=...` direkt einfügt in:

```php
include($_GET["file"]);
```

...und keine Filterung erfolgt, kann das gefährlich sein.


## Typische Payloads

```text
../../../../etc/passwd
..%2F..%2F..%2F..%2Fetc%2Fpasswd      ← URL-Encoded
..\..\..\..\windows\win.ini      ← Windows Beispiel
```

### Wie testen?

### Manuell mit `curl` oder im Browser:

```bash
curl "http://target.com/index.php?page=../../../../etc/passwd"
```

### Tools

- **Burp Suite** → Repeater + Intruder (z. B. Payloads automatisch testen)
- **dirb** → testet Pfade auf Schwachstellen (indirekt)
- **dotdotpwn** → spezialisiertes Traversal-Fuzzer-Tool
- **wfuzz** → generisches Fuzzing-Tool
- **OWASP ZAP** → Scanner für Directory Traversal
```

---

## 2. Hidden Field Manipulation

## 📌 Was ist das?

Ein **Hidden Field Manipulation Attack** liegt vor, wenn ein Angreifer versteckte HTML-Felder (hidden fields) einer Webanwendung verändert, um das Verhalten der Anwendung zu manipulieren.

Hidden Fields werden oft verwendet, um **nicht sichtbare, aber entscheidende Informationen** zwischen Client und Server zu übertragen – z. B.:

- Produktpreise
- Benutzerrollen
- Rabattwerte
- Session-Daten (z. B. in alten Systemen)

➡ Wenn diese Felder **nicht auf Serverseite validiert** werden, kann der Angreifer durch einfache Manipulation z. B. **den Preis senken, Admin-Zugriff erlangen oder Rabatte erschleichen**.


## 🔍 Beispiel

### Originales HTML (unsicher):
```html
<form action="/checkout" method="POST">
  <input type="hidden" name="price" value="99.99">
  <input type="hidden" name="role" value="user">
  <input type="submit" value="Buy">
</form>
```

### Angreifer manipuliert im Browser (Dev Tools):
```html
<input type="hidden" name="price" value="0.01">
<input type="hidden" name="role" value="admin">
```

➡ Wenn der Server das akzeptiert, hat der Angreifer erfolgreich manipuliert.


## 🧪 Wie kann man darauf testen?

### 🔧 Manuell im Browser

1. Rechtsklick → **Untersuchen** (Dev Tools öffnen)
2. Suche nach `<input type="hidden">` Feldern
3. Werte ändern und Formular absenden
4. Beobachte: wird die Manipulation übernommen?

### 📦 Automatisiert mit Tools

| Tool          | Funktion                          |
|---------------|-----------------------------------|
| **Burp Suite**| Abfangen & Manipulation via Proxy |
| **OWASP ZAP** | Automatisierte Erkennung          |
| **Fiddler**   | HTTP-Manipulation                 |
| **curl**      | Direktes Senden modifizierter POST-Daten |

#### Beispiel mit curl:
```bash
curl -X POST http://example.com/checkout \
  -d "price=0.01&role=admin"
```

---

## 3. Cookie Snooping
**Beschreibung**: Auslesen oder Abfangen von Cookies (z. B. via JavaScript oder MITM).
**Beispiel**:
```javascript
document.cookie // zeigt alle Cookies
```

---

## 4. RC4 NOMORE Attack
**Beschreibung**: Angriff auf den alten RC4-Verschlüsselungsalgorithmus durch Bias-Ausnutzung.
**Beispiel**: Verwendet bei alten TLS-Implementierungen – unbedingt deaktivieren!

---

## 5. Pass-the-Cookie Attack


Bei einer **Pass-the-Cookie-Attacke** verwendet ein Angreifer **ein gültiges Session-Cookie**, das von einem anderen Benutzer erfasst wurde, um sich **als dieser Benutzer auszugeben** – ohne dass Username oder Passwort benötigt werden.

Das Ziel ist **Session Hijacking**: der Angreifer übernimmt die aktive Sitzung eines Opfers.


## 🧠 Voraussetzungen für den Angriff

1. **Ein gültiges Session-Cookie muss abgefangen werden**, z. B. durch:
   - XSS (z. B. `document.cookie`)
   - Unsichere Übertragung (kein HTTPS)
   - Zugriff auf lokale Dateien (z. B. `cookies.sqlite`)
   - Malware oder infizierte Browser-Extensions

2. **Session Management ist schwach**:
   - Kein IP- oder User-Agent-Binding
   - Session läuft nicht sofort ab, wenn sie übernommen wurde

## 🧪 Beispiel-Ablauf

### 1. Opfer hat gültiges Cookie:
```http
Cookie: sessionid=ABC123XYZ
```

### 2. Angreifer kopiert diesen Cookie und sendet ihn manuell:
```bash
curl -b "sessionid=ABC123XYZ" https://target.com/profile
```

➡ Der Server akzeptiert das Cookie und der Angreifer ist **eingeloggt als das Opfer**.


## 🔧 Tools zur Durchführung

| Tool           | Zweck                                 |
|----------------|----------------------------------------|
| **Burp Suite** | Cookie einfügen & Requests senden      |
| **curl / httpie** | Cookies manuell setzen              |
| **Firefox + Cookie-Editor Plugin** | Cookies importieren |
| **Wireshark**  | Cookies in HTTP-Traffic abfangen (wenn kein HTTPS) |


## 📋 Beispiel mit curl

```bash
curl -b "PHPSESSID=xyz123" https://vulnerable.site/dashboard
```

➡ „-b“ steht für „cookie jar“.


## 🛡️ Schutzmaßnahmen

| Maßnahme                       | Beschreibung                                                |
|--------------------------------|-------------------------------------------------------------|
| ✅ **HTTPS erzwingen**         | Cookies dürfen nie unverschlüsselt übertragen werden        |
| ✅ **`HttpOnly` & `Secure` Flags** | Verhindert JavaScript-Zugriff & erzwungene HTTPS-Übertragung |
| ✅ **IP/User-Agent Binding**   | Session ist an spezifische IP/User-Agent gebunden          |
| ✅ **Session Timeout**         | Nach Inaktivität oder Login von anderem Ort: Session beenden |
| ✅ **Token Rotation**          | Neue Session-ID nach Login, Rollenwechsel etc.              |


## 🧪 Wie testen?

### Manuell mit Burp:

1. Cookie aus validem Login kopieren
2. In Repeater einfügen
3. Request senden und prüfen, ob Zugriff gewährt wird

### Mit curl:

```bash
curl -H "Cookie: session=abc123" https://target.site
```

---

## 6. Same-Site Attack

Same-Site Attacks – auch bekannt als **Related-Domain Attacks** – zielen auf **Subdomains einer legitimen Domain**, die fehlerhaft oder nicht (mehr) kontrolliert werden.  
Angreifer registrieren diese Subdomains oder nutzen DNS-Misskonfigurationen, um **Nutzer umzuleiten** und Daten zu stehlen.


## 🔍 Beispiel:

Ein Angreifer registriert:

```
rans.certifiedhacker.com
```

Die Hauptdomain `certifiedhacker.com` gehört einer legitimen Firma.  
Die Subdomain `rans.` war jedoch **nicht aktiv konfiguriert**, der DNS-Eintrag zeigt noch auf einen Hosting-Dienst (z. B. GitHub Pages).

Der Angreifer übernimmt den Service dort → **Dangling DNS Exploit**


## ⚠️ Risiken:

- **Nutzer vertrauen der Subdomain**, da sie zur legitimen Hauptdomain gehört.
- **Session Hijacking**, **Credential Theft**, **Phishing**, **Malware-Verteilung** sind möglich.
- Sicherheitsmechanismen wie Cookies mit `Domain=certifiedhacker.com` gelten **auch für Subdomains** → potenzielles Cookie-Leak.


## 🛠️ Schutzmaßnahmen:

- 🔒 **DNS-Hygiene**: Alle Subdomains regelmäßig prüfen.
- 🚫 **Dangling Records entfernen**: Nicht mehr genutzte DNS-Einträge löschen.
- 🧾 **Content Security Policy (CSP)** & **Subresource Integrity (SRI)** einsetzen.
- 🍪 **Cookies mit `SameSite=strict` oder `secure`** und nach Möglichkeit auf Root-Domain beschränken.

---

## 7. SQL Injection

SQL Injection (SQLi) ist eine Schwachstelle, bei der ein Angreifer **SQL-Befehle in eine Eingabe einschleust**, die dann vom Backend-Datenbankserver **ungefiltert ausgeführt** werden. Dadurch kann er Daten lesen, verändern oder löschen – oder sogar vollständigen Zugriff auf das System erhalten.


## 🔍 Beispiel

### 🧑‍💻 Angreifer-Eingabe:

```sql
test'); DROP TABLE Messages;--
```

### Unsicherer PHP-Code:

```php
$sql = "INSERT INTO Messages (user, message) 
        VALUES ('$user', '$message')";
```

Wenn `$message` den Angriffscode enthält, ergibt das:

```sql
INSERT INTO Messages (user, message) 
VALUES ('test', 'test'); DROP TABLE Messages;--');
```

➡️ Die Folge: **Die Tabelle `Messages` wird gelöscht!**


## 🛠️ Schutzmaßnahmen

1. **Prepared Statements / Parameterized Queries**  
   Beispiel mit PDO:
   ```php
   $stmt = $pdo->prepare("INSERT INTO Messages (user, message) VALUES (?, ?)");
   $stmt->execute([$user, $message]);
   ```

2. **Input-Validierung und -Filterung**  
   Erlaube nur erlaubte Zeichen oder Längen.

3. **Least Privilege-Prinzip für Datenbank-Benutzer**

4. **Web Application Firewalls (WAFs)**


## 🔧 Tools zum Testen von SQLi

| Tool         | Beschreibung                              |
|--------------|-------------------------------------------|
| `sqlmap`     | Automatisches Test- und Exploit-Tool      |
| `Burp Suite` | Manuelles Testen von Anfragen/Antworten   |
| `FuzzDB`     | Payload-Datenbank für Fuzzing             |
| `OWASP ZAP`  | Automatisches und manuelles Testing       |

---

## 8. Command Injection

### 🐚 Shell Injection (Command Injection)

**Beschreibung:**  
Shell Injection tritt auf, wenn ein Angreifer Eingaben an ein System sendet, das diese Eingaben ungefiltert an ein Betriebssystem-Kommando (z. B. Bash, CMD) übergibt.

**Ziel:**  
Ausführung beliebiger Befehle auf dem Server, z. B. zum Abgreifen von Passwörtern oder zur Übernahme des Systems.

**Beispiel:**
```bash
http://example.com/search.php?query=test;cat /etc/passwd
```

**Verwundbarer Code (PHP):**
```php
$query = $_GET['query'];
system("grep $query data.txt");
```

**Schutzmaßnahmen:**
- Eingaben validieren (Whitelist).
- Keine direkte Übergabe an `system()`, `exec()`, `popen()`.
- Escape der Eingaben, falls systemnahe Befehle notwendig sind.

---

### 🖼️ HTML Embedding (HTML Injection)

**Beschreibung:**  
Ein Angreifer injiziert HTML-Code in eine Anwendung, der dann von anderen Benutzern interpretiert wird. Dies kann für Social Engineering oder zur Vorbereitung eines XSS genutzt werden.

**Ziel:**  
Manipulation des DOM, Einfügen von Buttons, Formularen oder Weiterleitungen.

**Beispiel:**
```html
<input name="comment" value="<h1>Hacked!</h1>">
```

**Verwundbarer Code (PHP):**
```php
echo $_GET["comment"];
```

**Schutzmaßnahmen:**
- HTML-Entities encodieren (z. B. `htmlspecialchars()` in PHP).
- Keine ungesicherten Benutzereingaben direkt im DOM anzeigen.

---

### 📁 File Injection

**Beschreibung:**  
File Injection ermöglicht es Angreifern, manipulierte Dateinamen oder Pfade an eine Anwendung zu übergeben, sodass fremde Dateien eingebunden oder ausgeführt werden.

**Varianten:**
- **Local File Inclusion (LFI)**
- **Remote File Inclusion (RFI)**

**Beispiel (LFI):**
```http
http://example.com/index.php?page=../../../../etc/passwd
```

**Verwundbarer Code (PHP):**
```php
$page = $_GET['page'];
include($page . ".php");
```

**Ziel:**
- Zugriff auf sensitive Dateien.
- Code-Ausführung durch eingeschleuste PHP-Dateien.

**Schutzmaßnahmen:**
- Whitelist erlaubter Dateien.
- `basename()` und `realpath()` verwenden.
- Keine User-Eingaben in `include()`, `require()` oder `file_get_contents()`.

---

## 9. LDAP Injection
**Beschreibung**: Einschleusen von LDAP-Befehlen.
**Beispiel**:
```ldap
(&(user=*)(password=*))  // statt sicherer Query
```

---

## 10. Cross-Site Scripting (XSS)

### Typen
- Stored XSS
- Reflected XSS
- DOM-Based XSS

### Beispiel (Reflected XSS)
```html
<script>alert('XSS')</script>
```

### Filter-Evasion Techniken

#### 🔤 Encoding
```html
<a href=“&#106;avascript:alert(‘XSS Successful’)”>Click</a>
```

#### 📦 Base64
```html
<body onload="eval(atob('U3VjY2Vzc2Z1bCBYU1M='))">
```

#### ⚪ Unicode / ASCII
```html
<a href="jav&#x0A;ascript:alert('XSS')">Click</a>
```

#### 🔧 Tag-Manipulation
```html
<scr<script>ipt>alert('XSS')</scr<script>ipt>
```

### Tools
- XSS Hunter
- XSStrike
- OWASP ZAP
- Burp Suite

---

## 📋 Testen auf Schwachstellen

### Tools
- **Burp Suite (Community/Pro)**
- **curl / httpie** für manuelle Tests
- **dirb / gobuster** → Directory Traversal
- **sqlmap** → SQLi
- **Commix** → Command Injection
- **wfuzz / ffuf** → Bruteforce / Fuzzing

### Vorgehensweise
- Eingabefelder analysieren (HTML-Quelltext, Parameter)
- Manuelle Payloads testen (z. B. `' OR 1=1 --`)
- Burp Repeater + Intruder für systematische Tests
- Header, Cookies, Hidden Fields untersuchen

---

---

## 11. Buffer Overflow
**Beschreibung**: Überschreiben von Speicherbereichen durch zu große Eingaben.
**Beispiel**:
```c
char buf[10];
strcpy(buf, "AAAA...AAAA"); // 1000 Zeichen
```

---

## 12. Business Logic Bypass Attack
**Beschreibung**: Umgehung der beabsichtigten Geschäftslogik.
**Beispiel**: Rabatt mehrfach anwendbar machen durch Manipulation der URL.

---

## 13. Web-based Timing Attacks
**Beschreibung**: Auslesen von sensitiven Daten durch Messung der Antwortzeit.
**Beispiel**: Prüfen, ob ein Passwort-Zeichen korrekt ist anhand von Latenz.

---

## 14. CAPTCHA Attacks
**Beschreibung**: Automatisierte Umgehung von CAPTCHA (z. B. OCR, Replay).
**Beispiel**: Bots lösen einfache CAPTCHAs durch Bildverarbeitung.

---

## 15. Platform Exploits
**Beschreibung**: Ausnutzung von Betriebssystem-/Framework-Schwachstellen.
**Beispiel**: Exploit gegen alte Java- oder Apache-Versionen.

---

## 16. XML External Entity (XXE) Attack
**Beschreibung**: Auslesen interner Dateien über XML-Verarbeitung.
**Beispiel**:
```xml
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///etc/passwd">]>
<user>&xxe;</user>
```

---

## 17. Unvalidated Redirects and Forwards
**Beschreibung**: Umleiten von Benutzern auf bösartige Seiten.
**Beispiel**:
```http
GET /redirect?url=http://evil.com
```

---

## 18. Magecart Attack
**Beschreibung**: Skimming von Kreditkartendaten durch gehackte JS-Dateien.
**Beispiel**: Injected Skript auf Checkout-Seite.

---

## 19. Cross-Site Request Forgery (CSRF)
**Beschreibung**: Ausführen von Aktionen im Namen eines eingeloggten Nutzers.
**Beispiel**:
```html
<img src="https://example.com/delete?id=1">
```

---

## 20. Cookie/Session Poisoning
**Beschreibung**: Manipulation von Cookies oder Sessions.
**Beispiel**:
```http
Cookie: role=admin
```

---

## 21. Insecure Deserialization
**Beschreibung**: Unsicheres Laden von serialisierten Objekten.
**Beispiel**: Einschleusen von Objekten mit bösartigen Methoden.

---

## 22. Watering Hole Attack
**Beschreibung**: Kompromittierung legitimer Websites, um gezielt Besucher anzugreifen.
**Beispiel**: Malicious JS auf einer Entwicklerseite.

---

## 23. Denial-of-Service (DoS)
**Beschreibung**: Überlastung eines Dienstes.
**Beispiel**: Viele gleichzeitige Requests blockieren Server.

---

## 24. Web Service Attacks
**Beschreibung**: Angriffe auf SOAP/REST APIs (z. B. überlange Payloads).
**Beispiel**: SOAP Request mit rekursiven Tags.

---

## 25. Injecting an SSRF Payload
**Beschreibung**: Server fragt URLs im internen Netz ab.
**Beispiel**:
```http
url=http://127.0.0.1:8000/admin
```

---

## 26. Cross-Site Port Attack (XSPA)
**Beschreibung**: Erkennung offener Ports via Webanwendung.
**Beispiel**: Request an internen Dienst, der durch Reaktionszeit Rückschlüsse erlaubt.

---

## 27. DNS Rebinding Attack
**Beschreibung**: DNS-Antworten werden manipuliert, um interne IPs über den Browser zugänglich zu machen.

---

## 28. H2C Smuggling Attack
**Beschreibung**: Ausnutzung von HTTP/2-zu-HTTP/1.1-Konvertierung zur Umgehung von Sicherheitsprüfungen.

---

## 29. Clickjacking Attack
**Beschreibung**: Benutzer klicken auf versteckte Elemente (z. B. Buttons).
**Beispiel**: Iframe mit `opacity: 0` über Facebook-Button.

---

## 30. JavaScript Hijacking
**Beschreibung**: Abgreifen von JS-Antworten (z. B. via JSONP) von fremden Ursprüngen.

---

## 31. Cross-Site WebSocket Hijacking
**Beschreibung**: Missbrauch von WebSocket-Verbindungen über manipulierte Webseiten.

---

## 32. Obfuscation Application
**Beschreibung**: Tarnung von schädlichem Code durch Verschleierung.

---

## 33. Network Access Attacks
**Beschreibung**: Angriffe auf Netzwerkzugriffe, z. B. Sniffing, ARP-Spoofing.

---

## 34. DMZ Protocol Attacks
**Beschreibung**: Protokollbasierte Angriffe auf Dienste in der DMZ.

---

## 35. MarioNet Attack
**Beschreibung**: Aufbau eines Botnets im Browser über persistente Verbindungen.

---

