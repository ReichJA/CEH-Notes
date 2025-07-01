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