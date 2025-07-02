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
