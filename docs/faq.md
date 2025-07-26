# 🔍 FAQ - Häufig gestellte Fragen

## 📋 Übersicht

Diese Seite beantwortet die häufigsten Fragen zum Swiss RP Einreisebot.

---

## 🚀 Installation & Setup

### **Q: Wie installiere ich den Bot?**
**A:** 
1. Repository klonen: `git clone [repository-url]`
2. Abhängigkeiten installieren: `npm install`
3. `.env` Datei erstellen: `cp env.example .env`
4. Bot-Token in `.env` eintragen
5. Bot starten: `npm start`

### **Q: Welche Voraussetzungen brauche ich?**
**A:** 
- Node.js 16 oder höher
- Discord Bot Token
- Administrator-Berechtigungen auf dem Discord Server
- Git (für Installation)

### **Q: Wo bekomme ich einen Discord Bot Token?**
**A:** 
1. [Discord Developer Portal](https://discord.com/developers/applications) besuchen
2. "New Application" erstellen
3. Bot-Sektion aufrufen
4. "Add Bot" klicken
5. Token kopieren und in `.env` eintragen

### **Q: Welche Berechtigungen braucht der Bot?**
**A:** 
- **Erforderlich:** Nachrichten senden, Kanäle verwalten, Rollen verwalten
- **Empfohlen:** Administrator-Berechtigungen für vollständige Funktionalität

---

## ⚙️ Konfiguration

### **Q: Wie konfiguriere ich den Bot?**
**A:** 
```bash
# Automatische Konfiguration (empfohlen)
/setup applicant_role:@Bewerber roleplay_role:@Roleplay staff_role:@Moderator logs_channel:#logs

# Oder interaktiv
/setup
```

### **Q: Wie setze ich Zeitslots?**
**A:** 
```bash
# 24-Stunden Format
/settimeslots slots:"18:00-19:00, 19:00-20:00, 20:00-21:00"

# 12-Stunden Format
/settimeslots slots:"6:00 PM-7:00 PM, 7:00 PM-8:00 PM"
```

### **Q: Wie füge ich Staff-Rollen hinzu?**
**A:** 
```bash
/addstaffrole role:@Helper
/addstaffrole role:@Support
```

### **Q: Wie ändere ich die Willkommensnachricht?**
**A:** 
```bash
/setweltext message:"🎉 Willkommen {username} zu {servername}! 🎉"
```

**Verfügbare Platzhalter:**
- `{username}` - Benutzername
- `{servername}` - Server-Name

---

## 🎫 Ticket-System

### **Q: Wie erstelle ich ein Einreise-Panel?**
**A:** 
```bash
/sendentrypanel channel:#einreise
```

### **Q: Wie funktioniert das Ticket-Claiming?**
**A:** 
1. Moderator verwendet `/claimticket` im Ticket
2. Nur dieser Moderator kann das Ticket bearbeiten
3. Andere Moderatoren werden benachrichtigt
4. Nach Bearbeitung: `/releaseticket` verwenden

### **Q: Was passiert wenn ein Benutzer bereits ein Ticket hat?**
**A:** Der Bot verhindert die Erstellung eines zweiten Tickets und zeigt eine Fehlermeldung an.

### **Q: Wie kann ich ein Ticket manuell schließen?**
**A:** Verwende den 🔒 **Close** Button im Ticket oder verschiebe es manuell in die geschlossene Kategorie.

---

## 📅 Termin-Management

### **Q: Wie setze ich einen Termin für einen Benutzer?**
**A:** 
```bash
/setusertimeslot user:@Benutzername day:Freitag timeslot:18:00-19:00
```

### **Q: Was passiert wenn ein Benutzer seinen Termin nicht auswählen kann?**
**A:** Moderatoren können den Termin manuell mit `/setusertimeslot` setzen.

### **Q: Wie lange können Benutzer ihren Termin ändern?**
**A:** Standardmäßig 10 Minuten. Änderbar mit:
```bash
/setchangetime minutes:15
```

### **Q: Welche Zeitslot-Formate werden unterstützt?**
**A:** 
- **24-Stunden:** `18:00-19:00`
- **12-Stunden:** `6:00 PM-7:00 PM`
- **Gemischt:** `18:00-7:00 PM`

---

## 🛡️ Berechtigungen

### **Q: Wer kann den Bot verwenden?**
**A:** 
- **Administratoren:** Alle Befehle
- **Staff-Rollen:** Moderator-Befehle
- **Reguläre Benutzer:** Nur Bewerbungen erstellen

### **Q: Wie funktioniert die Staff-Erkennung?**
**A:** 
1. Prüft Administrator-Berechtigungen (automatisch Staff)
2. Prüft konfigurierte Staff-Rollen
3. Prüft zusätzliche Staff-Rollen

### **Q: Warum bekomme ich "Du bist kein Staff"?**
**A:** 
1. Prüfe ob du eine Staff-Rolle hast: `/liststaffroles`
2. Kontaktiere einen Administrator
3. Prüfe deine Administrator-Berechtigungen

### **Q: Kann ich mehrere Staff-Rollen haben?**
**A:** Ja, der Bot unterstützt unbegrenzte Staff-Rollen:
```bash
/addstaffrole role:@Helper
/addstaffrole role:@Support
/addstaffrole role:@Admin
```

---

## 🔧 Technische Fragen

### **Q: Welche Datenbank verwendet der Bot?**
**A:** Der Bot verwendet `pro.db` (SQLite-basiert) für die Datenspeicherung.

### **Q: Wie kann ich ein Backup erstellen?**
**A:** 
```bash
# Manuelles Backup
cp data/pro.db backup/pro.db.$(date +%Y%m%d_%H%M%S)

# Automatisches Backup-Skript
#!/bin/bash
DATE=$(date +%Y%m%d_%H%M%S)
cp data/pro.db backup/pro.db.$DATE
echo "Backup erstellt: pro.db.$DATE"
```

### **Q: Wie kann ich die Datenbank zurücksetzen?**
**A:** 
```bash
# Vorsicht: Alle Daten gehen verloren!
rm data/pro.db
npm start
/setup applicant_role:@Bewerber roleplay_role:@Roleplay staff_role:@Moderator logs_channel:#logs
```

### **Q: Wie kann ich Logs einsehen?**
**A:** 
```bash
# Live-Logs
tail -f logs/bot.log

# Letzte 100 Zeilen
tail -n 100 logs/bot.log

# Fehler anzeigen
grep -i "error" logs/bot.log
```

---

## 🚨 Probleme & Fehler

### **Q: Der Bot startet nicht - was tun?**
**A:** 
1. **Token prüfen:** Ist der Bot-Token korrekt?
2. **Abhängigkeiten:** `npm install` ausführen
3. **Node.js Version:** `node --version` (mindestens 16)
4. **Logs prüfen:** `cat logs/bot.log`

### **Q: "Invalid token provided" - was bedeutet das?**
**A:** Der Bot-Token ist falsch oder ungültig. Lösungen:
1. Token in Discord Developer Portal zurücksetzen
2. Neuen Token in `.env` eintragen
3. Bot neu starten

### **Q: "Bot hat keine Berechtigungen" - was tun?**
**A:** 
1. Bot-Rolle über Staff-Rollen positionieren
2. Administrator-Berechtigungen gewähren
3. Erforderliche Berechtigungen prüfen:
   - Nachrichten senden
   - Kanäle verwalten
   - Rollen verwalten

### **Q: "Benutzer hat kein aktives Ticket" - warum?**
**A:** Der Benutzer muss zuerst ein Ticket über das Einreise-Panel erstellen. Der Bot kann nur Termine für aktive Tickets setzen.

### **Q: Autocomplete funktioniert nicht - was tun?**
**A:** 
1. Zeitslots konfiguriert? `/gettimeslots`
2. Bot-Berechtigungen prüfen
3. Discord.js Version aktuell? `npm update`

---

## 📊 Monitoring & Wartung

### **Q: Wie überwache ich den Bot?**
**A:** 
```bash
# Bot-Status
pm2 status

# Memory-Verbrauch
pm2 monit

# Logs überwachen
tail -f logs/bot.log
```

### **Q: Wie oft sollte ich Backups erstellen?**
**A:** 
- **Täglich:** Für aktive Server
- **Wöchentlich:** Für weniger aktive Server
- **Vor Updates:** Immer vor größeren Änderungen

### **Q: Wie kann ich alte Logs löschen?**
**A:** 
```bash
# Logs rotieren
mv logs/bot.log logs/bot.log.$(date +%Y%m%d)
gzip logs/bot.log.$(date +%Y%m%d)

# Alte Logs löschen (älter als 90 Tage)
find logs/ -name "bot.log.*" -mtime +90 -delete
```

### **Q: Wie kann ich die Datenbank optimieren?**
**A:** 
```bash
# Datenbank optimieren
sqlite3 data/pro.db "VACUUM;"

# Indizes analysieren
sqlite3 data/pro.db "ANALYZE;"
```

---

## 🌍 Mehrsprachigkeit

### **Q: Welche Sprachen werden unterstützt?**
**A:** 
- **Deutsch** (Standard)
- **Englisch**

### **Q: Wie ändere ich die Sprache?**
**A:** In der `.env` Datei:
```env
# Deutsch
LOCAL=de

# Englisch
LOCAL=en
```

### **Q: Kann ich eigene Übersetzungen hinzufügen?**
**A:** Ja, bearbeite die Dateien in `locals/`:
- `locals/de.json` - Deutsche Übersetzungen
- `locals/en.json` - Englische Übersetzungen

---

## 🔄 Updates & Migration

### **Q: Wie aktualisiere ich den Bot?**
**A:** 
```bash
# Backup erstellen
cp data/pro.db backup/pro.db.$(date +%Y%m%d_%H%M%S)

# Repository aktualisieren
git pull origin main

# Abhängigkeiten aktualisieren
npm install

# Bot neu starten
npm restart
```

### **Q: Was passiert bei einem Update?**
**A:** 
- Neue Features werden hinzugefügt
- Bugs werden behoben
- Datenbank-Schema bleibt kompatibel
- Konfiguration bleibt erhalten

### **Q: Kann ich auf eine ältere Version zurücksetzen?**
**A:** 
```bash
# Spezifische Version auschecken
git checkout v1.0.0

# Abhängigkeiten installieren
npm install

# Bot neu starten
npm restart
```

---

## 📞 Support

### **Q: Wo bekomme ich Hilfe?**
**A:** 
1. **Dokumentation:** Diese FAQ und andere Dokumentationsseiten
2. **Logs:** `cat logs/bot.log` für Fehlerdetails
3. **Community:** Discord Server besuchen
4. **Issues:** GitHub Issues erstellen

### **Q: Welche Informationen brauche ich für Support?**
**A:** 
- **Fehlermeldung:** Vollständiger Error-Text
- **Schritte:** Was wurde gemacht?
- **Erwartung:** Was sollte passieren?
- **System:** Node.js Version, OS, Bot-Version

### **Q: Wie erstelle ich ein Issue?**
**A:** 
```markdown
## Problem
Kurze Beschreibung

## Schritte zum Reproduzieren
1. Schritt 1
2. Schritt 2

## Fehlermeldung
```
Error: Vollständiger Error-Text
```

## System-Informationen
- Node.js: v16.15.0
- OS: Ubuntu 20.04
- Bot-Version: 1.0.0
```

---

## 🎯 Best Practices

### **Q: Wie organisiere ich Staff-Rollen am besten?**
**A:** 
```
👑 Server Owner
├── 🤖 Bot (Administrator)
├── 🛡️ Head-Moderator
├── 🛡️ Moderator
├── 🛡️ Helper
├── 🎭 Roleplay
└── 📝 Bewerber
```

### **Q: Welche Zeitslots sind empfehlenswert?**
**A:** 
- **Wochentags:** 18:00-21:00 (nach der Arbeit)
- **Wochenende:** 14:00-22:00 (mehr Flexibilität)
- **Dauer:** 1-2 Stunden pro Slot

### **Q: Wie oft sollte ich Tickets überprüfen?**
**A:** 
- **Aktive Server:** Täglich
- **Weniger aktive Server:** Wöchentlich
- **Geschlossene Tickets:** Monatlich löschen

### **Q: Wie kann ich die Performance optimieren?**
**A:** 
- Regelmäßige Backups
- Log-Rotation
- Datenbank-Optimierung
- Memory-Monitoring

---

## 🔮 Zukünftige Features

### **Q: Welche Features sind geplant?**
**A:** 
- Erweiterte Statistiken
- Mehr Sprachen
- Webhook-Integration
- Erweiterte Zeitslot-Features

### **Q: Kann ich Features vorschlagen?**
**A:** Ja, erstelle ein GitHub Issue mit dem Label "enhancement".

### **Q: Wie kann ich zum Projekt beitragen?**
**A:** 
1. Fork des Repositories
2. Feature-Branch erstellen
3. Änderungen implementieren
4. Pull Request erstellen

---

**Weitere Fragen? Kontaktiere uns über GitHub Issues oder den Discord Server! 🛡️** 