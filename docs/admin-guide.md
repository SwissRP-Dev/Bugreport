# 📖 Administrator Guide

## 🎯 Übersicht

Diese Anleitung ist für **Administratoren** gedacht, die den Swiss RP Einreisebot auf ihrem Discord Server einrichten und konfigurieren möchten.

## 🚀 Erste Einrichtung

### Voraussetzungen

- **Discord Bot Token** - Von der Discord Developer Portal
- **Administrator-Berechtigungen** - Auf dem Discord Server
- **Node.js 16+** - Auf dem Hosting-System

### Installation

1. **Repository klonen:**
```bash
git clone [repository-url]
cd swiss-rp-einreisebot
```

2. **Abhängigkeiten installieren:**
```bash
npm install
```

3. **Umgebungsvariablen konfigurieren:**
```bash
cp env.example .env
```

4. **`.env` Datei bearbeiten:**
```env
BOT_TOKEN=your_discord_bot_token_here
LOCAL=de
```

5. **Bot starten:**
```bash
npm start
```

## ⚙️ Bot-Konfiguration

### Automatische Setup (Empfohlen)

Der einfachste Weg zur Konfiguration ist der automatische Setup:

```bash
/setup applicant_role:@Bewerber roleplay_role:@Roleplay staff_role:@Moderator logs_channel:#logs
```

**Was passiert:**
- ✅ Kategorien werden erstellt (Offene/Geschlossene Tickets)
- ✅ Rollen werden konfiguriert
- ✅ Logs-Kanal wird eingerichtet
- ✅ Berechtigungen werden automatisch gesetzt
- ✅ Standard-Einstellungen werden konfiguriert

### Interaktive Setup

Für eine detailliertere Konfiguration:

```bash
/setup
```

**Setup-Schritte:**
1. **Setup-Typ wählen** - Quick Setup oder Custom Setup
2. **Rollen konfigurieren** - Bewerber, Roleplay, Staff
3. **Logs-Kanal wählen** - Für Protokollierung
4. **Willkommensnachricht** - Anpassbare Nachricht
5. **Ban-Dauer** - Stunden für abgelehnte Bewerber
6. **Änderungszeit** - Minuten für Termin-Änderungen

## 🎛️ Erweiterte Konfiguration

### Rollen-Management

#### Staff-Rollen hinzufügen:
```bash
/addstaffrole role:@Helper
/addstaffrole role:@Support
```

#### Staff-Rollen entfernen:
```bash
/removestaffrole role:@Helper
```

#### Staff-Rollen auflisten:
```bash
/liststaffroles
```

### Zeitslot-Management

#### Zeitslots setzen:
```bash
/settimeslots slots:"18:00-19:00, 19:00-20:00, 20:00-21:00"
```

**Unterstützte Formate:**
- **24-Stunden:** `18:00-19:00`
- **12-Stunden:** `6:00 PM-7:00 PM`
- **Gemischt:** `18:00-7:00 PM`

#### Zeitslots anzeigen:
```bash
/gettimeslots
```

#### Zeitslots zurücksetzen:
```bash
/cleartimeslots
```

### Zeitzone-Konfiguration

#### Zeitzone setzen:
```bash
/timezone set timezone:Europe/Zurich
```

#### Zeitzone anzeigen:
```bash
/timezone get
```

### Termin-Änderungszeit

#### Änderungszeit konfigurieren:
```bash
/setchangetime minutes:15
```

**Standard:** 10 Minuten
**Empfehlung:** 15-30 Minuten

### Ban-Dauer

#### Ban-Zeit setzen:
```bash
/setbantime hours:24
```

**Standard:** 24 Stunden
**Empfehlung:** 24-72 Stunden

## 🎨 Einreise-Panel erstellen

### Panel senden:
```bash
/sendentrypanel channel:#einreise
```

**Was passiert:**
- ✅ Embed mit Willkommensnachricht wird erstellt
- ✅ "Start Entry" Button wird hinzugefügt
- ✅ Benutzer können Bewerbungen starten

### Willkommensnachricht anpassen:
```bash
/setweltext message:"Willkommen {username} zu {servername}! Bitte beantworte die Fragen unten."
```

**Platzhalter:**
- `{username}` - Benutzername
- `{servername}` - Server-Name

## 📊 Logging-System

### Logs-Kanal konfigurieren:
```bash
/setlogs channel:#logs
```

**Was wird protokolliert:**
- ✅ Ticket-Erstellung
- ✅ Ticket-Aktionen (Accept/Reject/Close)
- ✅ Staff-Aktionen (Claim/Release)
- ✅ Termin-Änderungen
- ✅ Ban-Aktionen

### Logs-Format:
```
🎫 Ticket erstellt von @Benutzer in #ticket-benutzer
✅ Ticket angenommen von @Moderator für @Benutzer
❌ Ticket abgelehnt von @Moderator für @Benutzer
🔒 Ticket geschlossen von @Moderator
```

## 🔧 Kategorie-Management

### Ticket-Kategorien:
- **🟢 Offene Tickets** - Aktive Bewerbungen
- **🔴 Geschlossene Tickets** - Abgeschlossene Bewerbungen

### Kategorien manuell setzen:
```bash
/setticketcategory category:#Tickets
/setcloseticketcategory category:#ClosedTickets
```

## 🛡️ Berechtigungen

### Automatische Berechtigungen:
- **Staff-Rollen** - Vollzugriff auf Ticket-Kategorien
- **Bot** - Administrator-Berechtigungen
- **@everyone** - Kein Zugriff auf Ticket-Kategorien

### Manuelle Berechtigungen:
Falls automatische Berechtigungen fehlschlagen:

1. **Staff-Rollen manuell hinzufügen:**
   - Kategorie → Einstellungen → Berechtigungen
   - Staff-Rolle hinzufügen
   - Alle Berechtigungen gewähren

2. **Bot-Berechtigungen prüfen:**
   - Bot-Rolle muss über Staff-Rollen stehen
   - Administrator-Berechtigungen empfohlen

## 🔍 Monitoring & Wartung

### Bot-Status prüfen:
```bash
# Logs überwachen
tail -f logs/bot.log

# Bot-Prozess prüfen
pm2 status
```

### Datenbank-Backup:
```bash
# Backup erstellen
cp data/pro.db backup/pro.db.$(date +%Y%m%d_%H%M%S)

# Backup wiederherstellen
cp backup/pro.db.20231201_120000 data/pro.db
```

### Performance-Optimierung:
- **Regelmäßige Backups** - Täglich
- **Log-Rotation** - Wöchentlich
- **Datenbank-Cleanup** - Monatlich

## 🚨 Troubleshooting

### Häufige Probleme:

#### Bot startet nicht:
```bash
# Logs prüfen
npm start

# Node.js Version prüfen
node --version

# Abhängigkeiten neu installieren
rm -rf node_modules
npm install
```

#### Berechtigungsfehler:
```bash
# Bot-Rolle prüfen
# Staff-Rollen prüfen
# Kategorie-Berechtigungen prüfen
```

#### Datenbank-Fehler:
```bash
# Backup wiederherstellen
# Datenbank neu initialisieren
```

## 📞 Support

### Bei Problemen:
1. **Logs prüfen** - Fehlermeldungen analysieren
2. **Dokumentation** - Diese Anleitung durchsuchen
3. **Community** - Discord Server besuchen
4. **Issues** - GitHub Issues erstellen

### Wichtige Links:
- **Discord Developer Portal:** https://discord.com/developers/applications
- **Node.js:** https://nodejs.org/
- **Discord.js:** https://discord.js.org/

---

**Viel Erfolg bei der Einrichtung! 🛡️** 