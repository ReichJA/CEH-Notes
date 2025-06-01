
# Cheatsheet: Modul 9 – Social Engineering

---

## 1. Grundlagen und Konzepte

- **Social Engineering** ist die Manipulation von Menschen zur Preisgabe vertraulicher Informationen oder zur Durchführung sicherheitskritischer Handlungen.
- Keine Technologie kann vollständig vor Social Engineering schützen – **nur geschulte und wachsame Mitarbeiter** bieten effektiven Schutz.
- Angreifer recherchieren vorab öffentlich zugängliche Informationen: Websites, Social Media, Presse, Foren.

---

## 2. Zielpersonen und Auswirkungen

### Häufige Ziele:
- Empfangs- und Helpdeskpersonal
- Technischer Support
- Administratoren
- Führungskräfte (CxOs)
- Kunden und Partner

### Auswirkungen:
- Finanzielle Verluste
- Reputationsschäden
- Datenschutzverletzungen
- Betriebsausfälle
- Juristische Konsequenzen

---

## 3. Psychologische Prinzipien

| Prinzip           | Erklärung 						|
|------------------|------------------------------------------------------------|
| **Autorität**     | Täuschung durch scheinbare Machtposition (z. B. CEO) 	|
| **Dringlichkeit** | Zeitdruck → Nutzer handeln unüberlegt 			|
| **Knappheit**     | Vermeintlich einmalige Angebote 				|
| **Sympathie**     | Menschen helfen eher, wenn sie jemanden mögen 		|
| **Konsens**       | „Alle machen es“ → Nachahmung 				|
| **Vertrauen**     | Aufbau einer glaubhaften Beziehung 			|
| **Gier**          | Verlockung durch Belohnung oder Gewinnspiel 		|

| Principle         | Explanation                                           |
|------------------|-------------------------------------------------------|
| **Authority**     | Deception through an apparent position of power (e.g., CEO) |
| **Urgency**       | Time pressure → users act without thinking           |
| **Scarcity**      | Allegedly one-time offers                            |
| **Liking**        | People are more likely to help if they like someone  |
| **Consensus**     | “Everyone is doing it” → imitation                   |
| **Trust**         | Building a credible relationship                     |
| **Greed**         | Temptation through rewards or sweepstakes            |


---

## 4. Human-based Techniken

- **Impersonation (Vortäuschen von Identität)**
  - Als Mitarbeiter, Techniker, VIP auftreten
  - Varianten: Helpdesk-Manipulation, Vishing, Technischer Support, Lieferant

- **Eavesdropping / Shoulder Surfing**
  - Gespräche abhören oder über die Schulter schauen

- **Dumpster Diving**
  - Informationsgewinnung durch Müllsuche

- **Reverse Social Engineering**
  - Täter inszeniert Problem und bietet Lösung an

- **Piggybacking / Tailgating**
  - Zutritt durch Mitgehen mit berechtigter Person

- **Diversion Theft, Honey Trap, Quid Pro Quo, Baiting**

| Principle         | Explanation                                           		| Example 											|
|-------------------|-------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| **Authority**     | Deception through an apparent position of power (e.g., CEO) 	| An attacker pretends to be the CEO and requests urgent access to financial data. 		|
| **Urgency**       | Time pressure → users act without thinking           		| “You must verify your account within 10 minutes or it will be locked!” 			|
| **Scarcity**      | Allegedly one-time offers                            		| “Only 3 gift cards left – act now!” 								|
| **Liking**        | People are more likely to help if they like someone  		| A friendly fake recruiter chats casually before asking for a résumé. 				|
| **Consensus**     | “Everyone is doing it” → imitation                   		| “Join 2,000 satisfied users who already claimed this reward.” 				|
| **Trust**         | Building a credible relationship                     		| A scammer builds rapport over weeks before asking for sensitive data. 			|
| **Greed**         | Temptation through rewards or sweepstakes            		| “You’ve won a free iPhone – just enter your login details to claim it.” 			|


---

## 5. Computer-based Techniken

- **Phishing / Spear Phishing / Whaling / Clone Phishing**
- **Scareware / Pop-Ups / Fake-Warnungen**
- **Consent Phishing / OAuth-Missbrauch**
- **Search Engine Phishing**
- **Malware-Verbreitung via Social Media**
- **SPIM (Spam in Instant Messaging)**
- **Bait and Switch Angriffe**

| Attack Type                                  | Explanation                                                                                                 | Example                                                                                  |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| **Phishing / Spear Phishing / Whaling / Clone Phishing** | Deceptive emails or messages to steal sensitive data. "Spear Phishing" targets individuals, "Whaling" targets executives, "Clone Phishing" mimics legitimate emails. | A seemingly legitimate email from “PayPal” asks the user to enter their password.        |
| **Scareware / Pop-Ups / Fake Warnings**      | Software or websites that use panic messages to manipulate users into acting (e.g., “Virus detected!”).     | A pop-up claims the PC is infected and urges the user to click “Clean Now.”             |
| **Consent Phishing / OAuth Abuse**           | Users are tricked into granting excessive permissions to an app – often via legitimate login pages.         | An app asks for access to emails and contacts via Google login.                         |
| **Search Engine Phishing**                   | Fake websites placed in search engine results to trick users.                                               | A fake support page ranks high on Google and asks for login credentials.                |
| **Malware Distribution via Social Media**    | Malware is spread through social media profiles or shared links.                                           | A friend shares a video that installs malware when clicked.                             |
| **SPIM (Spam in Instant Messaging)**         | Unwanted messages with phishing links or ads sent via messaging platforms.                                  | A WhatsApp message offers “free Netflix” but asks for personal info.                    |
| **Bait and Switch Attacks**                  | Users are lured by a harmless offer but redirected to something harmful.                                     | A download link claims to be a PDF but delivers a trojan.                               |


---

## 6. Tools

- **ShellPhish** – Fake-Login-Webseiten
- **SET (Social-Engineer Toolkit)** – umfassendes Framework für SE-Angriffe
- **Deepfake Tools** – DeepFaceLab, DeepfakesWeb, Synthesia
- **Voice Cloning Tools** – z. B. VEED.IO

---

## 7. KI-gestützte Methoden

- **KI-generierte Phishing-Mails**: z. B. ChatGPT-Texte im Stil von Mitarbeitern
- **Voice Cloning**: Imitation echter Stimmen (RNN, CNN)
- **Deepfake Videos**: Täuschend echte Video-Imitationen für Betrug, CEO-Fraud
- **Stil-Imitation**: KI lernt Textstil und täuscht glaubhafte Kommunikation vor

---

## 8. Social Media-basierte Angriffe

- **Catfishing**: Aufbau falscher Identitäten für romantische oder geschäftliche Täuschung
- **Angler Phishing**: Fake-Support-Accounts antworten auf Nutzerbeschwerden
- **Plattform-Impersonation**: Fake-Profile von Unternehmen/Mitarbeitern

---

## 9. Risiken für Unternehmen durch soziale Netzwerke

- **Data Theft / Reconnaissance**
- **Involuntary Data Leakage**
- **Targeted Attacks**
- **Spam / Phishing / Malware**
- **Content Manipulation**
- **Reputationsverlust**
- **Produktivitätsverlust / Kosten**

---

## 10. Identity Theft (Identitätsdiebstahl)

### Häufig gestohlene Daten:
- Name, Adresse, Telefonnummer
- SSN, Kreditkarten, Konten
- Biometrie, Führerschein, medizinische Daten

### Arten von Identitätsdiebstahl:
- **Child Identity Theft**
- **Criminal Identity Theft**
- **Financial Identity Theft**
- **Driver’s License Theft**
- **Medical / Insurance Theft**
- **Tax Identity Theft**
- **Synthetic Identity Theft**
- **Social Security Identity Theft**
- **Identity Cloning**

### Methoden zur Informationsgewinnung:
- **Diebstahl von Geräten**
- **Internetrecherche**
- **Social Engineering**
- **Dumpster Diving / Shoulder Surfing**

---


## 🛡️ Ergänzungen zu Social Engineering Gegenmaßnahmen

### Physische Sicherheitsrichtlinien
- Besucher müssen von Sicherheitspersonal begleitet werden.
- Zugang zu sensiblen Bereichen einschränken.
- Dokumente mit sensiblen Informationen sicher vernichten (z. B. durch Schreddern).
- Geräte sicher entsorgen (z. B. durch Überschreiben mit 0/1/Random).
- Sicherheitspersonal, Alarmsysteme und Überwachung einsetzen.

### Strategien zur Verteidigung
- **Social Engineering Kampagnen** zur Testung realer Reaktionen.
- **Gap Analysis** zur Identifikation von Schwachstellen.
- **Remediation Plan** zur Schließung der Sicherheitslücken.

### Weitere Maßnahmen
- Schulungen zu Richtlinien und Awareness.
- Zugriffskontrolle nach Rollen (Admin/User/Gast).
- Incident-Response-Richtlinien aufstellen.
- Informationsklassifizierung und -einschränkung.
- Hintergrundüberprüfungen und Offboarding-Prozesse.

---

## 🔐 Technische & administrative Maßnahmen

### Technische Schutzmaßnahmen
- Anti-Virus & Anti-Phishing-Systeme nutzen.
- Spamfilter aktivieren.
- Regelmäßige Softwareupdates.
- Zwei-Faktor-Authentifizierung (2FA).
- Verschlüsselte Kommunikationskanäle (z. B. HTTPS, VPN).

### Administrative Schutzmaßnahmen
- Hardware- und Software-Richtlinien durchsetzen.
- Identitätsprüfung und Absenderverifikation.
- Dokumentiertes Change-Management nutzen.

---

## 🎯 Phishing Countermeasures

- Schulungen mit Phishing-Simulationen.
- Spamfilter und Sicherheitsplugins nutzen.
- Keine Daten per E-Mail oder Telefon preisgeben.
- Links vor dem Klicken prüfen („hovern“).
- HTTPS nutzen, Absender verifizieren.
- MFA aktivieren.
- Reverse-Image-Suche bei verdächtigen Profilen.
- Cybercrime-Stellen informieren.
- Backups regelmäßig durchführen.

---

## 🧾 Identity Theft Countermeasures

### Praktische Schutzmaßnahmen
- Briefkasten regelmäßig leeren.
- Kreditangebote vernichten.
- Keine Finanzdaten auf Rechner speichern.
- Telefonrechnungen prüfen.
- SSN-Karte, Pass & Führerschein sicher verwahren.
- Datenschutzrichtlinien prüfen.
- Nur HTTPS nutzen, keine Daten über Links eingeben.
- Betrugswarnungen aktivieren.
- Keine Konten für Dritte eröffnen.
- Digitale Wallets & Kredit-Freeze nutzen.
- Papierlose Kontoauszüge bevorzugen.

---

## 🎙️ Voice Cloning Countermeasures

- Vorsicht bei unerwarteten Anrufen & Sprachaufforderungen.
- Verifizierung durch Sicherheitsfragen oder Codes.
- Aufklärung über Risiken von Voice Cloning.
- Nutzung von Voice-Biometrie und Anti-Spoofing.
- Sprachverschlüsselung aktivieren.
- Verifizierungsverfahren für Sprachkommunikation einführen.

# Ergänzende Inhalte: Social Engineering Countermeasures (mit Beispielen)

---

## 🛡️ Ergänzungen zu Social Engineering Gegenmaßnahmen

### Physische Sicherheitsrichtlinien

- **Beispiel:** Ein Besucher gibt sich als Techniker aus – wird aber zur Sicherheitslounge begleitet und darf nicht allein herumlaufen.
- **Erläuterung:** Durch Kontrolle des Zutritts wird verhindert, dass sich Social Engineers frei in einem Unternehmen bewegen.

### Strategien zur Verteidigung

- **Social Engineering Kampagnen:** Mitarbeiter erhalten gefälschte Phishing-Mails. Reaktionen werden anonym ausgewertet.
- **Gap Analysis:** Bewertung nach dem NIST Framework ergibt Schwächen im Umgang mit Mail-Anhängen.
- **Remediation Plan:** Neue Schulungen, restriktivere E-Mail-Richtlinien und technische Filter werden eingeführt.

### Weitere Maßnahmen

- **Beispiel:** Nur Admins dürfen Software installieren.
- **Erläuterung:** Verhindert die versehentliche Installation kompromittierter Tools.

---

## 🔐 Technische & administrative Maßnahmen

### Technische Schutzmaßnahmen

- **Beispiel:** Mitarbeiter greifen auf HR-Portal nur via 2FA mit Authenticator-App zu.
- **Erläuterung:** Selbst bei gestohlenem Passwort bleibt der Zugang geschützt.

### Administrative Schutzmaßnahmen

- **Beispiel:** USB-Sticks sind durch GPO-Richtlinien deaktiviert.
- **Erläuterung:** Verhindert Datendiebstahl und Malware-Einschleusung.

---

## 🎯 Phishing Countermeasures

- **Beispiel:** Eine gefälschte Mail eines vermeintlichen „IT-Leiters“ fordert zur Passwort-Änderung auf.
- **Gegenmaßnahme:** Mitarbeiter erkennt fehlende persönliche Anrede & prüft Link → meldet Mail als Phishing.

---

## 🧾 Identity Theft Countermeasures

- **Beispiel:** Ein Mitarbeiter speichert seine Kreditkartendaten in einem unverschlüsselten Notizdokument.
- **Erläuterung:** Solche Informationen gehören in einen Passwortmanager, nicht auf den Desktop.

- **Beispiel:** Durch Kredit-Freeze bei Schufa kann ein Angreifer trotz gestohlener SSN keinen Kredit eröffnen.
- **Erläuterung:** Einfache und effektive Maßnahme zur Prävention.

---

## 🎙️ Voice Cloning Countermeasures

- **Beispiel:** Ein vermeintlicher CEO ruft an und fordert eine dringende Überweisung – mit täuschend echter Stimme.
- **Gegenmaßnahme:** Buchhalter verlangt Rückruf über offizielle Firmenleitung – Angriff scheitert.

- **Erläuterung:** Zusätzliche Verifizierung schützt vor Deepfake-Sprachanrufen, selbst wenn Stimme realistisch klingt.
# Social Engineering Cheatsheet

---

# Lab

## **Objective**
- Sniff user/employee credentials such as IDs, names, and emails  
- Obtain personal and organizational information  
- Capture usernames and passwords  
- Perform and detect phishing  
- Use AI to craft phishing emails  

---

## **Overview of Social Engineering**
Social engineering manipulates individuals into divulging confidential information. Even well-protected organizations are susceptible due to human error.

**Organizational vulnerabilities include:**
- Insufficient security training  
- Unregulated access to information  
- Complex organizational structure  
- Missing/inadequate security policies  

**Potential impacts:**
- Economic loss  
- Reputational damage  
- Privacy loss  
- Risk of terrorism  
- Legal consequences  
- Operational shutdown  

---

## **Types of Social Engineering Attacks**
1. **Human-based**: Impersonation, vishing, eavesdropping  
2. **Computer-based**: Phishing, spamming, instant messaging  
3. **Mobile-based**: Malicious apps, fake security apps, SMiShing  

---

## **Lab Tasks Overview**
- Perform social engineering using various techniques  
- Sniff credentials using SET  
- Detect phishing using Netcraft  
- Use AI to craft phishing mails  

---

## **Lab 1: Perform Social Engineering using Various Techniques**

### **Tool:** Social-Engineer Toolkit (SET)

**About SET:**
- Open-source, Python-based  
- Used for spear phishing, credential harvesting, tabnabbing  
- Supports multi-attack vectors: email, web, USB  
- Industry standard for social engineering tests  

**Steps:**
1. Login to Parrot Security as `attacker/toor`  
2. Open terminal → `sudo su` → `setoolkit`  
3. Agree to terms with `y`  
4. Select options:  
   - `1`: Social-Engineering Attacks  
   - `2`: Website Attack Vectors  
   - `3`: Credential Harvester Attack Method  
   - `2`: Site Cloner  
5. Enter IP: `10.10.1.13`  
6. Clone URL: `http://www.moviescope.com`  
7. Send phishing mail with spoofed link  
8. On victim machine (Windows 11), access the fake site and enter credentials  
9. View credentials in Parrot terminal  

**Question 9.1.1.1:**  
- **Q:** What is the third method besides Web Templates and Site Cloner in SET for credential harvesting?  
- **A:** Manual Entry  

---

## **Lab 2: Detect a Phishing Attack**

### **Tool:** Netcraft Extension (in Firefox)

**Steps:**
1. Install Netcraft via `https://www.netcraft.com/apps-extensions`  
2. Enable extension and grant permissions  
3. Analyze `https://www.certifiedhacker.com`  
   - View site report: background, network, SSL/TLS info  
4. Visit phishing site (e.g., `https://end-authenticat.tftpd.net/`)  
5. Observe **"Suspected Phishing"** message  

**Question 9.2.1.1:**  
- **Q:** What message does Netcraft show for phishing sites?  
- **A:** "Suspected Phishing"  

---

## **Lab 3: Social Engineering using AI**

### **Tool:** ChatGPT

**Steps:**
1. Login to ChatGPT at `https://chatgpt.com`  
2. Use prompt to generate phishing email:  
   ```plaintext
   Pose as a genuine Microsoft support executive and write a mail about suspicious login. Ask for password reset. Use [Fake Reset Link].
ChatGPT generates realistic phishing content
Try variation:
IT admin mail requiring software install
Impersonation of a user’s writing style (e.g., Sam to John)
Caution:

Important ethical note: Using AI for phishing is illegal and unethical. This simulation serves solely for awareness and defense training.

