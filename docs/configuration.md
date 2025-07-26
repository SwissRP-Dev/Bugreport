# ⚙️ Konfiguration

## 📋 Übersicht

Diese Seite beschreibt alle Konfigurationsoptionen des Swiss RP Einreisebots, einschließlich Umgebungsvariablen, Datenbankeinstellungen und erweiterten Optionen.

---

## 🔧 Umgebungsvariablen

### **Grundlegende Konfiguration**

Erstelle eine `.env` Datei im Hauptverzeichnis:

```env
# Bot Token (erforderlich)
BOT_TOKEN=your_discord_bot_token_here

# Sprache (optional, Standard: de)
LOCAL=de

# Debug-Modus (optional, Standard: false)
DEBUG=false

# Log-Level (optional, Standard: info)
LOG_LEVEL=info
```

### **Variablen-Details**

| Variable | Beschreibung | Standard | Erforderlich |
|----------|--------------|----------|--------------|
| `BOT_TOKEN` | Discord Bot Token | - | ✅ Ja |
| `LOCAL` | Sprache (de/en) | `de` | ❌ Nein |
| `DEBUG` | Debug-Modus | `false` | ❌ Nein |
| `LOG_LEVEL` | Log-Level | `info` | ❌ Nein |

### **Sprach-Einstellungen**

```env
# Deutsch (Standard)
LOCAL=de

# Englisch
LOCAL=en
```

### **Debug-Konfiguration**

```env
# Debug-Modus aktivieren
DEBUG=true

# Log-Level setzen
LOG_LEVEL=debug
```

**Verfügbare Log-Level:**
- `error` - Nur Fehler
- `warn` - Warnungen und Fehler
- `info` - Informationen, Warnungen und Fehler
- `debug` - Alle Logs

---

## 🗄️ Datenbank-Konfiguration

### **Datenbank-Datei**

Der Bot verwendet `pro.db` (SQLite) für die Datenspeicherung:

```
data/
└── pro.db
```

### **Datenbank-Struktur**

#### **Guild-Konfiguration**
```sql
-- Server-spezifische Einstellungen
guild:{guildId}:roles:applicant     -- Bewerber-Rolle ID
guild:{guildId}:roles:roleplay      -- Roleplay-Rolle ID
guild:{guildId}:roles:staff         -- Haupt-Staff-Rolle ID
guild:{guildId}:roles:staff2        -- Zusätzliche Staff-Rolle ID
guild:{guildId}:roles:staff3        -- Zusätzliche Staff-Rolle ID
guild:{guildId}:category            -- Ticket-Kategorie ID
guild:{guildId}:closeCategory       -- Geschlossene-Tickets-Kategorie ID
guild:{guildId}:logs                -- Logs-Kanal ID
guild:{guildId}:welcomeText         -- Willkommensnachricht
guild:{guildId}:banTime             -- Ban-Dauer (Stunden)
guild:{guildId}:changeTime          -- Änderungszeit (Minuten)
guild:{guildId}:timezone            -- Server-Zeitzone
guild:{guildId}:timeslots           -- Verfügbare Zeitslots
```

#### **Ticket-Daten**
```sql
-- Ticket-spezifische Daten
user:{channelId}:ticket             -- Benutzer ID für Ticket
user:{channelId}:message            -- Ticket-Nachrichten ID
user:{channelId}:claimed            -- Beansprucht von (Staff ID)
user:{channelId}:appointmentDay     -- Termin-Tag
user:{channelId}:appointmentSlot    -- Termin-Zeitslot
user:{channelId}:answers            -- Benutzer-Antworten (JSON)
```

#### **Staff-Rollen**
```sql
-- Staff-Rollen-Verwaltung
guild:{guildId}:staffRoles          -- Staff-Rollen IDs (Array)
```

### **Datenbank-Backup**

#### **Automatisches Backup**
```bash
# Backup-Skript erstellen
#!/bin/bash
DATE=$(date +%Y%m%d_%H%M%S)
cp data/pro.db backup/pro.db.$DATE
echo "Backup erstellt: pro.db.$DATE"
```

#### **Backup wiederherstellen**
```bash
# Backup wiederherstellen
cp backup/pro.db.20231201_120000 data/pro.db
```

---

## 🎛️ Bot-Konfiguration

### **Rollen-Setup**

#### **Automatisches Setup**
```bash
/setup applicant_role:@Bewerber roleplay_role:@Roleplay staff_role:@Moderator logs_channel:#logs
```

#### **Manuelles Setup**
```bash
# Bewerber-Rolle
/setroles applicant role:@Bewerber

# Roleplay-Rolle
/setroles roleplay role:@Roleplay

# Staff-Rolle
/setroles staff role:@Moderator

# Zusätzliche Staff-Rollen
/addstaffrole role:@Helper
/addstaffrole role:@Support
```

### **Kategorie-Konfiguration**

#### **Ticket-Kategorien**
```bash
# Offene Tickets
/setticketcategory category:#Tickets

# Geschlossene Tickets
/setcloseticketcategory category:#ClosedTickets
```

**Empfohlene Struktur:**
```
📁 Tickets
├── #ticket-benutzer1
├── #ticket-benutzer2
└── #ticket-benutzer3

📁 ClosedTickets
├── #ticket-benutzer4
├── #ticket-benutzer5
└── #ticket-benutzer6
```

### **Zeitslot-Konfiguration**

#### **Zeitslots setzen**
```bash
# 24-Stunden Format
/settimeslots slots:"18:00-19:00, 19:00-20:00, 20:00-21:00"

# 12-Stunden Format
/settimeslots slots:"6:00 PM-7:00 PM, 7:00 PM-8:00 PM"

# Gemischtes Format
/settimeslots slots:"18:00-7:00 PM, 19:00-8:00 PM"
```

#### **Zeitzone konfigurieren**
```bash
# Schweizer Zeit
/timezone set timezone:Europe/Zurich

# Deutsche Zeit
/timezone set timezone:Europe/Berlin

# UTC
/timezone set timezone:UTC
```

### **Zeit-Management**

#### **Ban-Dauer**
```bash
# 24 Stunden (Standard)
/setbantime hours:24

# 48 Stunden
/setbantime hours:48

# 1 Woche
/setbantime hours:168
```

#### **Änderungszeit**
```bash
# 10 Minuten (Standard)
/setchangetime minutes:10

# 15 Minuten
/setchangetime minutes:15

# 30 Minuten
/setchangetime minutes:30
```

---

## 🎨 Benutzeroberfläche

### **Willkommensnachricht**

#### **Standard-Nachricht**
```
Willkommen {username} zu {servername}!
Bitte beantworte die Fragen unten, um deine Bewerbung zu starten.
```

#### **Anpassbare Nachricht**
```bash
/setweltext message:"🎉 Willkommen {username} zu {servername}! 🎉\n\nBitte beantworte die Fragen unten, um deine Bewerbung zu starten.\n\nViel Glück! 🍀"
```

**Verfügbare Platzhalter:**
- `{username}` - Benutzername
- `{servername}` - Server-Name

### **Einreise-Panel**

#### **Panel erstellen**
```bash
/sendentrypanel channel:#einreise
```

**Panel-Features:**
- ✅ Anpassbare Willkommensnachricht
- ✅ "Start Entry" Button
- ✅ Responsive Design
- ✅ Mehrsprachige Unterstützung

---

## 📊 Logging-Konfiguration

### **Logs-Kanal**

#### **Logs-Kanal setzen**
```bash
/setlogs channel:#logs
```

#### **Logs-Format**
```
🎫 Ticket erstellt von @Benutzer in #ticket-benutzer
✅ Ticket angenommen von @Moderator für @Benutzer
❌ Ticket abgelehnt von @Moderator für @Benutzer
🔒 Ticket geschlossen von @Moderator
🔄 Termin geändert von @Benutzer
📅 Termin gesetzt von @Moderator für @Benutzer
```

### **Log-Level**

#### **Konfiguration**
```env
# Nur Fehler
LOG_LEVEL=error

# Warnungen und Fehler
LOG_LEVEL=warn

# Alle Informationen
LOG_LEVEL=info

# Debug-Informationen
LOG_LEVEL=debug
```

---

## 🔒 Berechtigungen

### **Bot-Berechtigungen**

#### **Erforderliche Berechtigungen**
- ✅ **Nachrichten senden** - Für Ticket-Erstellung
- ✅ **Kanäle verwalten** - Für Ticket-Kanäle
- ✅ **Rollen verwalten** - Für Rollen-Zuweisung
- ✅ **Nachrichten verwalten** - Für Ticket-Updates
- ✅ **Berechtigungen verwalten** - Für Kategorie-Setup

#### **Empfohlene Berechtigungen**
- ✅ **Administrator** - Für vollständige Funktionalität
- ✅ **Server verwalten** - Für erweiterte Features

### **Rollen-Hierarchie**

#### **Empfohlene Struktur**
```
👑 Server Owner
├── 🤖 Bot (Administrator)
├── 🛡️ Moderator (Staff-Rolle)
├── 🎭 Roleplay (Angenommene Bewerber)
└── 📝 Bewerber (Neue Benutzer)
```

#### **Berechtigungen pro Rolle**

**Bot-Rolle:**
- ✅ Administrator-Berechtigungen
- ✅ Über Staff-Rollen positioniert

**Staff-Rollen:**
- ✅ Vollzugriff auf Ticket-Kategorien
- ✅ Nachrichten verwalten
- ✅ Benutzer verwalten

**Roleplay-Rolle:**
- ✅ Zugriff auf Roleplay-Kanäle
- ✅ Kein Zugriff auf Ticket-Kategorien

**Bewerber-Rolle:**
- ✅ Zugriff auf Bewerber-Kanäle
- ✅ Kein Zugriff auf Ticket-Kategorien

---

## 🚀 Performance-Optimierung

### **Datenbank-Optimierung**

#### **Regelmäßige Wartung**
```bash
# Backup erstellen
cp data/pro.db backup/pro.db.$(date +%Y%m%d_%H%M%S)

# Datenbank optimieren
sqlite3 data/pro.db "VACUUM;"

# Indizes prüfen
sqlite3 data/pro.db "ANALYZE;"
```

#### **Cleanup-Skript**
```bash
#!/bin/bash
# Alte Backups löschen (älter als 30 Tage)
find backup/ -name "pro.db.*" -mtime +30 -delete

# Logs rotieren
if [ -f logs/bot.log ]; then
    mv logs/bot.log logs/bot.log.$(date +%Y%m%d)
    gzip logs/bot.log.$(date +%Y%m%d)
fi
```

### **Bot-Optimierung**

#### **Memory-Management**
```javascript
// Garbage Collection aktivieren
setInterval(() => {
    if (global.gc) {
        global.gc();
    }
}, 30000); // Alle 30 Sekunden
```

#### **Error-Handling**
```javascript
// Unhandled Promise Rejections abfangen
process.on('unhandledRejection', (error) => {
    console.error('Unhandled Promise Rejection:', error);
});
```

---

## 🔍 Monitoring

### **Bot-Status**

#### **Health-Check**
```bash
# Bot-Prozess prüfen
ps aux | grep node

# Memory-Verbrauch
pm2 monit

# Logs überwachen
tail -f logs/bot.log
```

#### **Performance-Metriken**
- **Memory-Verbrauch** - Sollte unter 100MB bleiben
- **CPU-Verbrauch** - Sollte unter 5% bleiben
- **Response-Time** - Sollte unter 1 Sekunde sein
- **Uptime** - Sollte über 99% sein

### **Alerting**

#### **Discord-Webhook für Alerts**
```javascript
// Webhook für kritische Fehler
const webhook = new WebhookClient({ url: 'WEBHOOK_URL' });

webhook.send({
    content: '🚨 Bot-Fehler aufgetreten!',
    embeds: [{
        title: 'Error Alert',
        description: error.message,
        color: 0xFF0000
    }]
});
```

---

## 🚨 Troubleshooting

### **Häufige Konfigurationsprobleme**

#### **Bot startet nicht**
```bash
# Token prüfen
echo $BOT_TOKEN

# Abhängigkeiten prüfen
npm list

# Logs prüfen
cat logs/bot.log
```

#### **Berechtigungsfehler**
```bash
# Bot-Rolle prüfen
# Staff-Rollen prüfen
# Kategorie-Berechtigungen prüfen
```

#### **Datenbank-Fehler**
```bash
# Datenbank-Integrität prüfen
sqlite3 data/pro.db "PRAGMA integrity_check;"

# Backup wiederherstellen
cp backup/pro.db.latest data/pro.db
```

---

## 📞 Support

### **Konfigurations-Hilfe**
1. **Dokumentation prüfen** - Diese Seite durchsuchen
2. **Logs analysieren** - Fehlermeldungen prüfen
3. **Community kontaktieren** - Discord Server besuchen
4. **Issues erstellen** - GitHub Issues verwenden

### **Wichtige Links**
- **Discord Developer Portal:** https://discord.com/developers/applications
- **Discord.js Dokumentation:** https://discord.js.org/
- **SQLite Dokumentation:** https://www.sqlite.org/docs.html

---

**Viel Erfolg bei der Konfiguration! 🛡️** 