# 🚨 Troubleshooting

## 📋 Übersicht

Diese Seite enthält Lösungen für häufige Probleme und Fehler beim Swiss RP Einreisebot.

---

## 🔧 Häufige Probleme

### **Bot startet nicht**

#### **Problem:**
```
Error: Cannot find module 'discord.js'
```

#### **Lösung:**
```bash
# Abhängigkeiten installieren
npm install

# Oder neu installieren
rm -rf node_modules package-lock.json
npm install
```

#### **Problem:**
```
Error: Cannot find module 'pro.db'
```

#### **Lösung:**
```bash
# Datenbank-Ordner erstellen
mkdir -p data

# Bot neu starten
npm start
```

#### **Problem:**
```
Error: Invalid token provided
```

#### **Lösung:**
1. **Token prüfen:**
   ```bash
   # .env Datei bearbeiten
   nano .env
   ```

2. **Token neu generieren:**
   - Discord Developer Portal besuchen
   - Bot-Token zurücksetzen
   - Neuen Token in `.env` eintragen

### **Berechtigungsfehler**

#### **Problem: "Du bist kein Staff"**
**Symptom:** Benutzer mit Staff-Rolle bekommt Fehlermeldung

**Lösung:**
1. **Staff-Rolle prüfen:**
   ```bash
   /liststaffroles
   ```

2. **Staff-Rolle hinzufügen:**
   ```bash
   /addstaffrole role:@DeineRolle
   ```

3. **Administrator-Berechtigungen prüfen:**
   - Benutzer hat automatisch Staff-Rechte wenn Administrator

#### **Problem: "Bot hat keine Berechtigungen"**
**Symptom:** Bot kann keine Tickets erstellen oder Rollen verwalten

**Lösung:**
1. **Bot-Rolle prüfen:**
   - Server-Einstellungen → Rollen
   - Bot-Rolle über Staff-Rollen positionieren

2. **Berechtigungen gewähren:**
   - Nachrichten senden
   - Kanäle verwalten
   - Rollen verwalten
   - Nachrichten verwalten
   - Berechtigungen verwalten

3. **Administrator-Berechtigungen (empfohlen):**
   - Bot-Rolle → Administrator aktivieren

### **Ticket-Probleme**

#### **Problem: "Benutzer hat kein aktives Ticket"**
**Symptom:** Moderator kann Termin nicht setzen

**Lösung:**
1. **Ticket-Existenz prüfen:**
   - Benutzer muss zuerst ein Ticket über das Einreise-Panel erstellen
   - Ticket muss in der Ticket-Kategorie existieren

2. **Ticket-Kategorie prüfen:**
   ```bash
   /setticketcategory category:#Tickets
   ```

#### **Problem: "Ticket ist bereits beansprucht"**
**Symptom:** Moderator kann Ticket nicht beanspruchen

**Lösung:**
1. **Anderen Moderator kontaktieren:**
   - Warten bis Ticket freigegeben wird
   - Moderator bitten `/releaseticket` zu verwenden

2. **Ticket-Status prüfen:**
   - Im Ticket nach "Claimed by" Nachricht suchen

#### **Problem: "Ungültiger Zeitslot"**
**Symptom:** Zeitslot kann nicht gesetzt werden

**Lösung:**
1. **Verfügbare Zeitslots prüfen:**
   ```bash
   /gettimeslots
   ```

2. **Zeitslots neu setzen:**
   ```bash
   /settimeslots slots:"18:00-19:00, 19:00-20:00"
   ```

3. **Autocomplete verwenden:**
   - Bei `/setusertimeslot` Autocomplete für Zeitslots nutzen

### **Datenbank-Probleme**

#### **Problem: "Database locked"**
**Symptom:** Bot kann Datenbank nicht lesen/schreiben

**Lösung:**
1. **Bot neu starten:**
   ```bash
   npm restart
   ```

2. **Datenbank-Berechtigungen prüfen:**
   ```bash
   ls -la data/pro.db
   chmod 644 data/pro.db
   ```

3. **Backup wiederherstellen:**
   ```bash
   cp backup/pro.db.latest data/pro.db
   ```

#### **Problem: "Corrupted database"**
**Symptom:** Bot zeigt unerwartete Fehler

**Lösung:**
1. **Datenbank-Integrität prüfen:**
   ```bash
   sqlite3 data/pro.db "PRAGMA integrity_check;"
   ```

2. **Datenbank reparieren:**
   ```bash
   sqlite3 data/pro.db "VACUUM;"
   ```

3. **Backup wiederherstellen:**
   ```bash
   cp backup/pro.db.$(date +%Y%m%d_%H%M%S) data/pro.db
   ```

### **Zeitslot-Probleme**

#### **Problem: "No timeslots configured"**
**Symptom:** Autocomplete zeigt keine Zeitslots

**Lösung:**
1. **Zeitslots setzen:**
   ```bash
   /settimeslots slots:"18:00-19:00, 19:00-20:00"
   ```

2. **Zeitslots prüfen:**
   ```bash
   /gettimeslots
   ```

#### **Problem: "Invalid time format"**
**Symptom:** Zeitslots werden nicht akzeptiert

**Lösung:**
1. **Korrektes Format verwenden:**
   ```bash
   # 24-Stunden Format
   /settimeslots slots:"18:00-19:00, 19:00-20:00"
   
   # 12-Stunden Format
   /settimeslots slots:"6:00 PM-7:00 PM, 7:00 PM-8:00 PM"
   ```

2. **Zeitzone prüfen:**
   ```bash
   /timezone get
   /timezone set timezone:Europe/Zurich
   ```

### **Panel-Probleme**

#### **Problem: "Panel wird nicht angezeigt"**
**Symptom:** Einreise-Panel erscheint nicht

**Lösung:**
1. **Panel senden:**
   ```bash
   /sendentrypanel channel:#einreise
   ```

2. **Bot-Berechtigungen prüfen:**
   - Nachrichten senden
   - Embeds senden
   - Buttons erstellen

#### **Problem: "Button funktioniert nicht"**
**Symptom:** "Start Entry" Button reagiert nicht

**Lösung:**
1. **Bot-Berechtigungen prüfen:**
   - Nachrichten verwalten
   - Interaktionen verwalten

2. **Panel neu senden:**
   ```bash
   /sendentrypanel channel:#einreise
   ```

---

## 🔍 Debug-Modus

### **Debug aktivieren**

#### **Umgebungsvariable:**
```env
DEBUG=true
LOG_LEVEL=debug
```

#### **Debug-Logs aktivieren:**
```javascript
// In index.js
process.env.DEBUG = 'true';
```

### **Debug-Informationen**

#### **Bot-Status prüfen:**
```bash
# Logs anzeigen
tail -f logs/bot.log

# Bot-Prozess prüfen
ps aux | grep node

# Memory-Verbrauch
pm2 monit
```

#### **Datenbank-Debug:**
```bash
# Datenbank-Inhalt prüfen
sqlite3 data/pro.db ".tables"
sqlite3 data/pro.db "SELECT * FROM guild;"
```

---

## 🛠️ Erweiterte Lösungen

### **Bot komplett neu installieren**

#### **Schritt-für-Schritt:**
```bash
# 1. Backup erstellen
cp -r . ../swiss-rp-backup

# 2. Repository neu klonen
cd ..
rm -rf swiss-rp-einreisebot
git clone [repository-url]
cd swiss-rp-einreisebot

# 3. Abhängigkeiten installieren
npm install

# 4. Konfiguration wiederherstellen
cp ../swiss-rp-backup/.env .
cp ../swiss-rp-backup/data/pro.db data/

# 5. Bot starten
npm start
```

### **Datenbank zurücksetzen**

#### **Vorsicht: Alle Daten gehen verloren!**
```bash
# 1. Backup erstellen
cp data/pro.db backup/pro.db.$(date +%Y%m%d_%H%M%S)

# 2. Datenbank löschen
rm data/pro.db

# 3. Bot neu starten (erstellt neue DB)
npm start

# 4. Konfiguration neu einrichten
/setup applicant_role:@Bewerber roleplay_role:@Roleplay staff_role:@Moderator logs_channel:#logs
```

### **Logs analysieren**

#### **Fehler-Logs finden:**
```bash
# Alle Fehler anzeigen
grep -i "error" logs/bot.log

# Spezifische Fehler suchen
grep -i "permission" logs/bot.log
grep -i "database" logs/bot.log
grep -i "token" logs/bot.log
```

#### **Performance-Logs:**
```bash
# Response-Zeiten prüfen
grep -i "response" logs/bot.log

# Memory-Verbrauch prüfen
grep -i "memory" logs/bot.log
```

---

## 📞 Support-Kanäle

### **Hilfe bekommen**

#### **1. Dokumentation prüfen:**
- Diese Troubleshooting-Seite
- Administrator Guide
- Moderator Guide
- Befehlsreferenz

#### **2. Logs analysieren:**
```bash
# Letzte 100 Zeilen
tail -n 100 logs/bot.log

# Fehler der letzten Stunde
grep "$(date '+%Y-%m-%d %H:')" logs/bot.log | grep -i error
```

#### **3. Community kontaktieren:**
- Discord Server besuchen
- GitHub Issues erstellen
- Entwickler kontaktieren

### **Issue erstellen**

#### **Benötigte Informationen:**
1. **Fehlermeldung** - Vollständiger Error-Text
2. **Schritte zum Reproduzieren** - Was wurde gemacht?
3. **Erwartetes Verhalten** - Was sollte passieren?
4. **Tatsächliches Verhalten** - Was passiert stattdessen?
5. **Bot-Version** - `npm list` Ausgabe
6. **Node.js Version** - `node --version`
7. **Betriebssystem** - `uname -a`

#### **Issue-Template:**
```markdown
## Problem
Kurze Beschreibung des Problems

## Schritte zum Reproduzieren
1. Schritt 1
2. Schritt 2
3. Schritt 3

## Erwartetes Verhalten
Was sollte passieren?

## Tatsächliches Verhalten
Was passiert stattdessen?

## Fehlermeldung
```
Error: Vollständiger Error-Text
```

## System-Informationen
- Bot-Version: [Version]
- Node.js: [Version]
- OS: [Betriebssystem]
```

---

## 🚀 Prävention

### **Regelmäßige Wartung**

#### **Tägliche Checks:**
```bash
# Bot-Status prüfen
pm2 status

# Logs überwachen
tail -n 50 logs/bot.log

# Memory-Verbrauch prüfen
pm2 monit
```

#### **Wöchentliche Wartung:**
```bash
# Backup erstellen
cp data/pro.db backup/pro.db.$(date +%Y%m%d_%H%M%S)

# Logs rotieren
mv logs/bot.log logs/bot.log.$(date +%Y%m%d)
gzip logs/bot.log.$(date +%Y%m%d)

# Datenbank optimieren
sqlite3 data/pro.db "VACUUM;"
```

#### **Monatliche Wartung:**
```bash
# Alte Backups löschen (älter als 30 Tage)
find backup/ -name "pro.db.*" -mtime +30 -delete

# Alte Logs löschen (älter als 90 Tage)
find logs/ -name "bot.log.*" -mtime +90 -delete

# Abhängigkeiten aktualisieren
npm update
```

### **Monitoring einrichten**

#### **Discord-Webhook für Alerts:**
```javascript
// Kritische Fehler an Discord senden
const webhook = new WebhookClient({ url: 'WEBHOOK_URL' });

webhook.send({
    content: '🚨 Bot-Fehler aufgetreten!',
    embeds: [{
        title: 'Error Alert',
        description: error.message,
        color: 0xFF0000,
        timestamp: new Date()
    }]
});
```

#### **Health-Check-Skript:**
```bash
#!/bin/bash
# Bot-Status prüfen
if ! pgrep -f "node.*index.js" > /dev/null; then
    echo "Bot ist nicht aktiv!"
    # Benachrichtigung senden
    curl -X POST -H "Content-Type: application/json" \
         -d '{"content":"🚨 Bot ist offline!"}' \
         $DISCORD_WEBHOOK_URL
fi
```

---

## 🎯 Häufige Fragen (FAQ)

### **Q: Warum funktioniert der Bot nicht?**
**A:** Prüfe die häufigsten Probleme:
1. Bot-Token korrekt?
2. Abhängigkeiten installiert?
3. Bot-Berechtigungen gesetzt?
4. Datenbank vorhanden?

### **Q: Wie kann ich den Bot zurücksetzen?**
**A:** 
1. Backup erstellen
2. Datenbank löschen
3. Bot neu starten
4. Konfiguration neu einrichten

### **Q: Warum kann ich keine Tickets erstellen?**
**A:** Prüfe:
1. Einreise-Panel vorhanden?
2. Bot-Berechtigungen?
3. Ticket-Kategorie konfiguriert?

### **Q: Wie kann ich Staff-Rollen hinzufügen?**
**A:** 
```bash
/addstaffrole role:@DeineRolle
```

### **Q: Warum funktioniert Autocomplete nicht?**
**A:** Prüfe:
1. Zeitslots konfiguriert?
2. Bot-Berechtigungen?
3. Discord.js Version aktuell?

---

**Viel Erfolg beim Troubleshooting! 🛡️** 