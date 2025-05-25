# 🛠️ Anleitung: Windows Kiosk Mode mit Flipper Zero (BadUSB) verlassen

## 📦 Voraussetzungen

- Flipper Zero mit aktueller Firmware
- BadUSB-Funktion aktiviert
- Zugriff auf das USB-Laufwerk des Flipper
- [Datei: escape_kiosk_mode.txt](https://github.com/ReichJA/CEH-Notes/edit/main/anleitung_kiosk_escape.md#:~:text=escape_kiosk_mode.txt)

---

## 📁 Schritt 1: Datei auf Flipper kopieren

1. Schließe den Flipper per USB an den Computer an.
2. Öffne den Datei-Explorer.
3. Kopiere die Datei `escape_kiosk_mode.txt` in folgenden Ordner:

```
/apps_data/BadUSB/
```

---

## 🧪 Schritt 2: Skript ausführen

1. Navigiere im Flipper-Menü:
   ```
   BadUSB → escape_kiosk_mode.txt
   ```
2. Drücke **OK** zum Ausführen.
3. Der Flipper simuliert eine Tastatur und führt folgende Schritte durch:
   - Öffnet den Task-Manager (`Strg + Shift + Esc`)
   - Versucht einen neuen Task `explorer.exe` zu starten
   - Versucht über `Win + R` nochmals `explorer.exe` zu starten

---

## 🧩 Alternative Methoden (manuell oder durch Anpassung)
- Sticky Keys (`Shift` 5×)
- STRG + ALT + ENTF (über SCANCODE)

---

## 📝 Empfehlung
Teste dieses Skript in einer VM oder Testumgebung, um das Verhalten zu prüfen. Unterschiedliche Kiosk-Konfigurationen blockieren ggf. bestimmte Tastenkombinationen.

---

## 🔚 Ziel
Bei Erfolg wird die Windows Shell (`explorer.exe`) geladen, wodurch Zugriff auf Desktop und Dateiexplorer möglich wird.
