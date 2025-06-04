
# Netzwerk- und Sicherheitsübersicht

## 🔌 Übersicht: Services und Ports

| **Service**   | **Protokoll(e)**       | **Port** | **Beschreibung**                          |
|---------------|------------------------|----------|-------------------------------------------|
| **SSH**       | TCP                    | 22       | Secure Shell für verschlüsselte Fernzugriffe |
| **DNS**       | UDP / TCP              | 53       | Domain Name System (Nameauflösung)        |
| **HTTP**      | TCP                    | 80       | Hypertext Transfer Protocol (Webseiten)   |
| **HTTPS**     | TCP                    | 443      | HTTP Secure (verschlüsselte Webseiten)    |
| **FTP**       | TCP                    | 21       | File Transfer Protocol (Steuerverbindung) |
|               | TCP                    | 20       | FTP Datenübertragung (aktive Verbindung)  |
| **TFTP**      | UDP                    | 69       | Trivial File Transfer Protocol            |
| **VNC**       | TCP                    | 5900+N   | Virtual Network Computing (Fernzugriff)   |
| **RDP**       | TCP                    | 3389     | Remote Desktop Protocol (Windows)         |
| **Kerberos**  | UDP / TCP              | 88       | Authentifizierungsprotokoll               |
| **LDAP**      | TCP / UDP              | 389      | Lightweight Directory Access Protocol     |
| **NetBIOS**   | UDP                    | 137, 138 | Name Service und Datagramm Service        |
|               | TCP                    | 139      | Session Service (Dateifreigabe etc.)      |
| **SMB**       | TCP                    | 445      | Server Message Block (Netzwerkfreigaben)  |

---

## 🛡️ Übersicht: Firewalls, IDS, IPS

| **Komponente**     | **Typ**            | **Merkmale**                                                                 | **Beispielhafte Funktionen**                                         |
|--------------------|--------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|
| **Firewall**        | Klassisch          | Paketfilterung (IP, Port, Protokoll)                                         | Portfilter, einfache Regelwerke                                     |
| **Next-Gen Firewall** | Stateful & DPI    | Kombiniert Firewall, IDS/IPS, App Control                                   | Malware-Filter, SSL Inspection, User-ID                             |
| **Stateless Firewall** | Paketbasiert     | Prüft Pakete unabhängig voneinander                                          | Schnell, aber kontextlos                                            |
| **Stateful Firewall** | Verbindungsbezogen| Merkt sich Verbindungskontext (z. B. TCP-Session)                            | Rückantworten nachvollziehen, zuverlässiger                         |
| **IDS**             | Passiv             | Erkennt Angriffe, meldet sie, ohne Eingriff                                 | Signatur-/Verhaltensbasierte Erkennung, Logging                     |
| **IPS**             | Aktiv              | Erkennt und **blockiert** Angriffe automatisch                              | Paketfilterung, Session-Reset, Regelbasierte Reaktion               |

---

## 🔐 Symmetrisch vs. Asymmetrisch

| **Verfahren** | **Typ**         | **Schlüsselart**              | **Typische Schlüsselgröße**       | **Verwendungszweck**                  | **Bemerkung** |
|---------------|------------------|-------------------------------|-----------------------------------|----------------------------------------|----------------|
| **AES**       | Symmetrisch       | Ein Schlüssel (gleich)        | 128, 192, 256 Bit                 | Datenverschlüsselung (VPN, TLS)       | Sehr sicher, schnell |
| **DES**       | Symmetrisch       | Ein Schlüssel                 | 56 Bit                            | Veraltet, früher Standard             | Heute unsicher |
| **Blowfish**  | Symmetrisch       | Ein Schlüssel                 | 32–448 Bit                        | Alternative zu DES                    | Schnell, aber selten |
| **RC4**       | Symmetrisch       | Ein Schlüssel                 | 40–2048 Bit                       | TLS, WEP, heute unsicher              | Veraltet      |
| **DH**        | Asymmetrisch      | Zwei Schlüssel (pub/priv)     | Variabel (oft >2048 Bit)         | Schlüsselaustausch                    | Kein Datencrypto direkt |

---

## 🧮 Übersicht: Hashverfahren

| **Algorithmus** | **Hashlänge (Bit)** | **Hex-Zeichen** | **Sicherheitsstatus**     | **Verwendung / Bemerkung**                                     |
|------------------|----------------------|------------------|----------------------------|------------------------------------------------------------------|
| **MD5**          | 128                  | 32               | Unsicher                   | Veraltet, nicht mehr empfohlen                                 |
| **SHA-1**        | 160                  | 40               | Unsicher                   | Kollisionen bekannt                                            |
| **SHA-2 (256)**  | 256                  | 64               | Sehr sicher                | TLS, Signaturen, Blockchain                                    |
| **SHA-2 (512)**  | 512                  | 128              | Sehr sicher                | HMACs, Zertifikate                                             |
| **SHA-3 (256)**  | 256                  | 64               | Sehr sicher                | Alternative zu SHA-2 (Keccak)                                  |

---

## 🔐 WLAN-Sicherheit: WEP, WPA, WPA2, WPS

| **Technologie** | **Typ**           | **Verschlüsselung**     | **Sicherheitsstatus** | **Bemerkung** |
|------------------|-------------------|--------------------------|------------------------|----------------|
| **WEP**          | Verschlüsselung    | RC4 (statisch)           | Unsicher               | Veraltet       |
| **WPA**          | Übergangsstandard | TKIP (RC4-basiert)       | Mittel                 | Rückwärtskompatibel |
| **WPA2**         | Sicherer Standard | AES (CCMP)               | Sicher                 | Heutiger Standard |
| **WPS**          | Verbindungsmethode | Nutzt WPA/WPA2 intern    | Unsicher (PIN)         | Deaktivieren empfohlen |

---

## 🧷 IEEE 802.1X

| **Aspekt**                   | **Beschreibung**                                                                 |
|-----------------------------|----------------------------------------------------------------------------------|
| **Typ**                      | Authentifizierungsprotokoll für Netzwerke                                       |
| **Verwendung**               | Netzwerkzugang (LAN/WLAN)                                                       |
| **Komponenten**              | Supplicant, Authenticator, Authentication Server (z. B. RADIUS)                |
| **Protokollbasis**           | EAP (z. B. EAP-TLS)                                                             |
| **Sicherheit**               | Starke Authentifizierung möglich (Zertifikate etc.)                            |

---

## 📄 X.509-Zertifikate

| **Aspekt**             | **Beschreibung**                                                    |
|------------------------|---------------------------------------------------------------------|
| **Typ**                | Standard für digitale Zertifikate                                  |
| **Verwendung**         | HTTPS, VPN, E-Mail, Code Signing                                    |
| **Bestandteile**       | Seriennummer, öffentlicher Schlüssel, Aussteller, Signatur, Gültigkeit |
| **PKI-Integration**    | Bestandteil einer Zertifikatskette (Root → Intermediate → Client)  |
| **Formate**            | PEM, DER, PKCS#12 (.pfx, .p12)                                      |

## IPSec (Internet Protocol Security)
- Protokollpaket zur Sicherung von IP-Kommunikation auf Schicht 3 (Netzwerkschicht)
- Schützt vor: Ausspähen, Manipulation, Replay-Angriffen
- Besteht aus:
  - **AH (Authentication Header)**: Authentifizierung & Integrität
  - **ESP (Encapsulating Security Payload)**: Authentifizierung, Integrität & **Verschlüsselung**
- Zwei Modi:
  - **Transport-Modus**: Nur Payload wird geschützt
  - **Tunnel-Modus**: Ganzes IP-Paket wird geschützt (z. B. bei VPNs)

## ISAKMP (Internet Security Association and Key Management Protocol)
- Framework zur Verwaltung von Sicherheitsparametern (Security Associations)
- Definiert den Ablauf für Authentifizierung, Schlüsselaushandlung und Verwaltung
- Grundlage für **IKE**, beschreibt den Ablauf, aber keine Kryptografie

## IKE (Internet Key Exchange)
- Implementierung von ISAKMP mit kryptografischen Verfahren
- Aufgabe: Sichere **Aushandlung von Schlüsseln** und Aufbau einer **Security Association (SA)**
- Zwei Phasen:
  1. Aufbau eines sicheren Kanals (IKE SA)
  2. Aushandlung von IPSec-Schlüsseln (IPSec SA)

## HMAC (Hash-based Message Authentication Code)
- Gewährleistet **Integrität und Authentizität** von Nachrichten
- Kombination aus:
  - Hash-Funktion (z. B. SHA-256)
  - Geheimer Schlüssel
- Einsatz in: **IPSec**, **TLS**, **SSH**, **JWTs**

---

## SSL (Secure Sockets Layer)
- Ursprüngliches Verschlüsselungsprotokoll für die sichere Kommunikation im Internet
- Heute **veraltet und unsicher** (SSL 2.0, 3.0)
- Vorgänger von TLS

## TLS (Transport Layer Security)
- Nachfolger von SSL, aktuelles Standardprotokoll zur **Ende-zu-Ende-Verschlüsselung** im Web
- Wird verwendet bei: **HTTPS**, **E-Mail-Verschlüsselung**, **VoIP**
- Schützt auf Schicht 4 (Transportschicht)
- Unterstützt:
  - Authentifizierung über Zertifikate
  - Verschlüsselung (z. B. AES)
  - Integritätsprüfung (z. B. HMAC)

## JWT (JSON Web Token)
- Kompakter Token zur sicheren Übertragung von Informationen als **JSON-Objekt**
- Besteht aus drei Teilen:
  1. Header (z. B. Algorithmus: HS256)
  2. Payload (z. B. Benutzer-ID, Rollen)
  3. Signature (z. B. HMAC mit geheimem Schlüssel oder RSA)
- Einsatz z. B. in **Authentifizierungsmechanismen** von Webanwendungen
- Vorteil: Kann **serverseitig stateless** validiert werden
