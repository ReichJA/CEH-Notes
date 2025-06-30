# Footprinting & Information Gathering – Zusammenfassung

## Lernziele des Moduls

- Footprinting-Konzepte beschreiben
- Nutzung von Suchmaschinen und Google-Hacking-Techniken
- Recherchen über Internetdienste und soziale Netzwerke
- Whois-, DNS-, Netzwerk- und E-Mail-Footprinting
- Social Engineering im Footprinting
- Nutzung diverser Tools
- Best Practices anwenden

---

## Whois Footprinting

### Whois Datenmodelle

| Modelltyp             | Beschreibung |
|-----------------------|--------------|
| **Thick Whois**       | Vollständige Whois-Daten von allen Registraren (verteiltes Modell) |
| **Thin Whois**        | Nur Verweis auf den Whois-Server des Registrars (zentralisiertes Modell) |
| **Decentralized Whois** | Mehrere unabhängige WHOIS-Verwalter speichern vollständige Informationen |

### Ergebnisse einer Whois-Abfrage

- Domain-Details, Registrar, Kontaktdaten
- Nameserver, NetRange
- Erstellungs- und Ablaufdatum
- Letzte Aktualisierung
- Domainstatus (verfügbar, registriert, gesperrt)
- IP-Adressinformationen

### Regionale Internet-Registrare (RIRs)

- **ARIN** – [arin.net](https://www.arin.net)
- **AFRINIC** – [afrinic.net](https://www.afrinic.net)
- **APNIC** – [apnic.net](https://www.apnic.net)
- **RIPE** – [ripe.net](https://www.ripe.net)
- **LACNIC** – [lacnic.net](https://www.lacnic.net)

---

## DNS Footprinting

Angreifer sammeln Infos zu DNS-Servern, -Einträgen und -Typen, um Hosts im Zielnetzwerk zu identifizieren und auszunutzen.

### DNS-Record-Typen

| Typ     | Beschreibung |
|---------|--------------|
| A       | IPv4-Adresse eines Hosts |
| AAAA    | IPv6-Adresse eines Hosts |
| MX      | Mailserver der Domain |
| NS      | Nameserver |
| CNAME   | Alias für einen Host |
| SOA     | Zuständige Instanz für Domain |
| SRV     | Dienstinformationen |
| PTR     | Reverse Lookup (IP → Hostname) |
| RP      | Verantwortliche Person |
| HINFO   | CPU und Betriebssystem |
| TXT     | Textinformationen |

### DNS Interrogation Tools

- **SecurityTrails**, **Fierce**, **DNSChecker**, **zdns**, **DNSdumpster**
- Nutzen IP-Routing-Lookups und Zonendaten (wenn verfügbar)

---

## Netzwerk- & E-Mail-Footprinting

### Netzwerk

- Netzbereich lokalisieren
- Traceroute-Analyse durchführen

### Traceroute-Varianten

| Typ          | Tool/OS       | Protokoll | Beispiel                  |
|--------------|---------------|-----------|---------------------------|
| ICMP         | Windows       | ICMP      | `tracert 216.239.36.10`   |
| TCP          | Linux         | TCP       | `sudo tcptraceroute www.google.com` |
| UDP          | Linux         | UDP       | `traceroute www.google.com` |

### Private IP-Ranges (RFC 1918)

| Bereich                      | Präfix       |
|-----------------------------|--------------|
| 10.0.0.0 – 10.255.255.255   | `10/8`       |
| 172.16.0.0 – 172.31.255.255 | `172.16/12`  |
| 192.168.0.0 – 192.168.255.255 | `192.168/16` |

---

## E-Mail-Tracking

### Tools

- IP2LOCATION Email Header Tracer
- MxToolbox
- eMailTrackerPro
- Holehe
- DNSChecker Email Header Analyzer
- Social Catfish

### Gewonnene Informationen

- IP-Adresse des Empfängersystems
- Geolocation
- Empfangs- und Lesezeit
- Lesezeitdauer
- Proxy-Erkennung
- Klickverhalten bei Links
- Betriebssystem & Browser

### E-Mail-Header enthält:

- Mailserver des Absenders
- Empfangsdatum/-zeit
- Authentifizierungsmethoden
- Versanddatum/-zeit
- Eindeutige Nachrichtennummer
- Name & IP des Absenders

---

*Stand: CEH Footprinting Modul*