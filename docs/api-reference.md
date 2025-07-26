# 📚 API Referenz

## 📋 Übersicht

Diese Seite enthält die technische API-Referenz für den Swiss RP Einreisebot, einschließlich Datenbankstruktur, Utility-Funktionen und Event-Handler.

---

## 🗄️ Datenbank-API

### **Datenbank-Keys**

#### **Guild-Konfiguration**
```javascript
// Rollen-Konfiguration
keys.guild(guildId, "roles:applicant")     // Bewerber-Rolle ID
keys.guild(guildId, "roles:roleplay")      // Roleplay-Rolle ID
keys.guild(guildId, "roles:staff")         // Haupt-Staff-Rolle ID
keys.guild(guildId, "roles:staff2")        // Zusätzliche Staff-Rolle ID
keys.guild(guildId, "roles:staff3")        // Zusätzliche Staff-Rolle ID

// Kategorie-Konfiguration
keys.guild(guildId, "category")            // Ticket-Kategorie ID
keys.guild(guildId, "closeCategory")       // Geschlossene-Tickets-Kategorie ID

// Logging-Konfiguration
keys.guild(guildId, "logs")                // Logs-Kanal ID

// Nachrichten-Konfiguration
keys.guild(guildId, "welcomeText")         // Willkommensnachricht

// Zeit-Konfiguration
keys.guild(guildId, "banTime")             // Ban-Dauer (Stunden)
keys.guild(guildId, "changeTime")          // Änderungszeit (Minuten)
keys.guild(guildId, "timezone")            // Server-Zeitzone

// Zeitslot-Konfiguration
keys.guild(guildId, "timeslots")           // Verfügbare Zeitslots (Array)
keys.guild(guildId, "staffRoles")          // Staff-Rollen IDs (Array)
```

#### **Ticket-Daten**
```javascript
// Ticket-spezifische Daten
keys.user(channelId, "ticket")             // Benutzer ID für Ticket
keys.user(channelId, "message")            // Ticket-Nachrichten ID
keys.user(channelId, "claimed")            // Beansprucht von (Staff ID)
keys.user(channelId, "appointmentDay")     // Termin-Tag
keys.user(channelId, "appointmentSlot")    // Termin-Zeitslot
keys.user(channelId, "answers")            // Benutzer-Antworten (JSON)
```

### **Datenbank-Operationen**

#### **Grundlegende Operationen**
```javascript
// Daten lesen
const value = await db.get(key);

// Daten schreiben
await db.set(key, value);

// Daten löschen
await db.delete(key);

// Daten prüfen
const exists = await db.has(key);
```

#### **Beispiele**
```javascript
// Bewerber-Rolle abrufen
const applicantRoleId = await db.get(keys.guild(guildId, "roles:applicant"));

// Zeitslots setzen
await db.set(keys.guild(guildId, "timeslots"), ["18:00-19:00", "19:00-20:00"]);

// Ticket-Daten abrufen
const ticketUserId = await db.get(keys.user(channelId, "ticket"));
```

---

## 🛠️ Utility-Funktionen

### **Staff-Utilities**

#### **hasStaffRole(member, guildId)**
Prüft, ob ein Mitglied Staff-Berechtigungen hat.

```javascript
const { hasStaffRole } = require('./utils/staffUtils');

// Verwendung
const isStaff = await hasStaffRole(member, guildId);
```

**Parameter:**
- `member` - Discord.js GuildMember Objekt
- `guildId` - Guild ID (String)

**Rückgabe:**
- `true` - Mitglied ist Staff
- `false` - Mitglied ist kein Staff

**Logik:**
1. Prüft Administrator-Berechtigungen
2. Prüft konfigurierte Staff-Rollen
3. Prüft zusätzliche Staff-Rollen

#### **getStaffRoleIds(guildId)**
Holt alle Staff-Rollen-IDs für einen Server.

```javascript
const { getStaffRoleIds } = require('./utils/staffUtils');

// Verwendung
const staffRoleIds = await getStaffRoleIds(guildId);
```

**Parameter:**
- `guildId` - Guild ID (String)

**Rückgabe:**
- `Array` - Array von Staff-Rollen-IDs

#### **getPrimaryStaffRoleId(guildId)**
Holt die Haupt-Staff-Rollen-ID.

```javascript
const { getPrimaryStaffRoleId } = require('./utils/staffUtils');

// Verwendung
const primaryStaffRoleId = await getPrimaryStaffRoleId(guildId);
```

**Parameter:**
- `guildId` - Guild ID (String)

**Rückgabe:**
- `String` - Haupt-Staff-Rollen-ID oder `null`

#### **getAdditionalStaffRoleIds(guildId)**
Holt zusätzliche Staff-Rollen-IDs.

```javascript
const { getAdditionalStaffRoleIds } = require('./utils/staffUtils');

// Verwendung
const additionalStaffRoleIds = await getAdditionalStaffRoleIds(guildId);
```

**Parameter:**
- `guildId` - Guild ID (String)

**Rückgabe:**
- `Array` - Array von zusätzlichen Staff-Rollen-IDs

#### **getUserTicketChannel(userId, guildId, guild)**
Findet den Ticket-Kanal für einen Benutzer.

```javascript
const { getUserTicketChannel } = require('./utils/staffUtils');

// Verwendung
const channelId = await getUserTicketChannel(userId, guildId, guild);
```

**Parameter:**
- `userId` - Benutzer-ID (String)
- `guildId` - Guild ID (String)
- `guild` - Discord.js Guild Objekt (optional)

**Rückgabe:**
- `String` - Kanal-ID oder `null`

### **Timeslot-Utilities**

#### **getGuildTimeslots(guildId, db, keys)**
Holt verfügbare Zeitslots für einen Server.

```javascript
const { getGuildTimeslots } = require('./utils/timeslotUtils');

// Verwendung
const timeslots = await getGuildTimeslots(guildId, db, keys);
```

**Parameter:**
- `guildId` - Guild ID (String)
- `db` - Datenbank-Instanz
- `keys` - Keys-Objekt

**Rückgabe:**
- `Array` - Array von Zeitslots oder `null`

#### **parseTimeslots(timeslotsString)**
Parst eine Zeitslot-String in ein Array.

```javascript
const { parseTimeslots } = require('./utils/timeslotUtils');

// Verwendung
const timeslots = parseTimeslots("18:00-19:00, 19:00-20:00");
```

**Parameter:**
- `timeslotsString` - Zeitslot-String (String)

**Rückgabe:**
- `Array` - Array von Zeitslots

**Unterstützte Formate:**
- `"18:00-19:00, 19:00-20:00"`
- `"6:00 PM-7:00 PM, 7:00 PM-8:00 PM"`
- `"18:00-7:00 PM, 19:00-8:00 PM"`

#### **validateTimeslot(timeslot, availableTimeslots)**
Validiert einen Zeitslot gegen verfügbare Zeitslots.

```javascript
const { validateTimeslot } = require('./utils/timeslotUtils');

// Verwendung
const isValid = validateTimeslot("18:00-19:00", ["18:00-19:00", "19:00-20:00"]);
```

**Parameter:**
- `timeslot` - Zu validierender Zeitslot (String)
- `availableTimeslots` - Verfügbare Zeitslots (Array)

**Rückgabe:**
- `true` - Zeitslot ist gültig
- `false` - Zeitslot ist ungültig

### **Localization-Utilities**

#### **loadLocalization(local)**
Lädt Lokalisierungsdaten.

```javascript
const { loadLocalization } = require('./utils/localization');

// Verwendung
const local = loadLocalization('de'); // oder 'en'
```

**Parameter:**
- `local` - Sprachcode (String)

**Rückgabe:**
- `Object` - Lokalisierungs-Objekt

#### **replacePlaceholders(text, replacements)**
Ersetzt Platzhalter in Text.

```javascript
const { replacePlaceholders } = require('./utils/localization');

// Verwendung
const text = replacePlaceholders(
    "Willkommen {username} zu {servername}!",
    { username: "Max", servername: "Swiss RP" }
);
```

**Parameter:**
- `text` - Text mit Platzhaltern (String)
- `replacements` - Ersetzungen (Object)

**Rückgabe:**
- `String` - Text mit ersetzten Platzhaltern

### **Interaction-Utilities**

#### **handleInteraction(interaction, handler)**
Zentrale Interaktion-Behandlung mit Error-Handling.

```javascript
const { handleInteraction } = require('./utils/interactionHandler');

// Verwendung
await handleInteraction(interaction, async () => {
    // Interaktion-Logik hier
    await interaction.reply("Antwort");
});
```

**Parameter:**
- `interaction` - Discord.js Interaction Objekt
- `handler` - Async-Funktion für Interaktion-Logik

**Features:**
- Automatisches Error-Handling
- Logging von Fehlern
- Graceful Degradation

#### **safeReply(interaction, options)**
Sichere Antwort auf Interaktionen.

```javascript
const { safeReply } = require('./utils/interactionHandler');

// Verwendung
await safeReply(interaction, {
    content: "Antwort",
    ephemeral: true
});
```

**Parameter:**
- `interaction` - Discord.js Interaction Objekt
- `options` - Antwort-Optionen (Object)

**Features:**
- Automatisches Deferring
- Error-Handling
- Ephemeral-Unterstützung

---

## 🎯 Event-Handler

### **Button-Handler**

#### **handleEntryButton(interaction)**
Behandelt "Start Entry" Button-Klicks.

```javascript
const { handleEntryButton } = require('./handlers/buttonHandler');

// Verwendung
await handleEntryButton(interaction);
```

**Parameter:**
- `interaction` - Discord.js ButtonInteraction Objekt

**Funktionalität:**
- Prüft ob Benutzer bereits ein Ticket hat
- Erstellt Modal für Bewerbung
- Validiert Benutzer-Berechtigungen

#### **handleTicketButtons(interaction)**
Behandelt Ticket-Aktions-Buttons (Accept/Reject/Close/Change).

```javascript
const { handleTicketButtons } = require('./handlers/buttonHandler');

// Verwendung
await handleTicketButtons(interaction);
```

**Parameter:**
- `interaction` - Discord.js ButtonInteraction Objekt

**Unterstützte Buttons:**
- `accept` - Ticket annehmen
- `reject` - Ticket ablehnen
- `close` - Ticket schließen
- `change` - Termin ändern lassen

### **Select-Menu-Handler**

#### **handleTimeslotSelect(interaction)**
Behandelt Zeitslot-Auswahl.

```javascript
const { handleTimeslotSelect } = require('./handlers/selectMenuHandler');

// Verwendung
await handleTimeslotSelect(interaction);
```

**Parameter:**
- `interaction` - Discord.js StringSelectMenuInteraction Objekt

**Funktionalität:**
- Validiert ausgewählten Zeitslot
- Speichert Termin in Datenbank
- Aktualisiert Ticket-Nachricht
- Sendet Bestätigung an Benutzer

### **Setup-Handler**

#### **handleSetupModal(interaction)**
Behandelt Setup-Modal-Submission.

```javascript
const { handleSetupModal } = require('./handlers/setupHandler');

// Verwendung
await handleSetupModal(interaction);
```

**Parameter:**
- `interaction` - Discord.js ModalSubmitInteraction Objekt

**Funktionalität:**
- Validiert Setup-Daten
- Erstellt Kategorien
- Konfiguriert Rollen
- Setzt Berechtigungen
- Speichert Konfiguration

---

## 🔧 Service-Funktionen

### **Ticket-Service**

#### **createTicket(member, inputs, local, interaction)**
Erstellt ein neues Ticket.

```javascript
const { createTicket } = require('./services/ticketService');

// Verwendung
await createTicket(member, inputs, local, interaction);
```

**Parameter:**
- `member` - Discord.js GuildMember Objekt
- `inputs` - Benutzer-Eingaben (Object)
- `local` - Lokalisierungs-Objekt
- `interaction` - Discord.js Interaction Objekt (optional)

**Funktionalität:**
- Erstellt Ticket-Kanal
- Speichert Benutzer-Daten
- Sendet Willkommensnachricht
- Erstellt Ticket-Buttons
- Sendet Ephemeral-Bestätigung

#### **closeTicket(channel, reason, local)**
Schließt ein Ticket.

```javascript
const { closeTicket } = require('./services/ticketService');

// Verwendung
await closeTicket(channel, "Ticket geschlossen", local);
```

**Parameter:**
- `channel` - Discord.js TextChannel Objekt
- `reason` - Schließungsgrund (String)
- `local` - Lokalisierungs-Objekt

**Funktionalität:**
- Verschiebt Ticket in geschlossene Kategorie
- Entfernt Benutzer-Berechtigungen
- Sendet Schließungsnachricht
- Protokolliert Aktion

#### **acceptTicket(channel, moderator, local)**
Nimmt ein Ticket an.

```javascript
const { acceptTicket } = require('./services/ticketService');

// Verwendung
await acceptTicket(channel, moderator, local);
```

**Parameter:**
- `channel` - Discord.js TextChannel Objekt
- `moderator` - Discord.js GuildMember Objekt
- `local` - Lokalisierungs-Objekt

**Funktionalität:**
- Weist Roleplay-Rolle zu
- Entfernt Bewerber-Rolle
- Schließt Ticket
- Sendet Bestätigung an Benutzer
- Protokolliert Aktion

#### **rejectTicket(channel, moderator, local)**
Lehnt ein Ticket ab.

```javascript
const { rejectTicket } = require('./services/ticketService');

// Verwendung
await rejectTicket(channel, moderator, local);
```

**Parameter:**
- `channel` - Discord.js TextChannel Objekt
- `moderator` - Discord.js GuildMember Objekt
- `local` - Lokalisierungs-Objekt

**Funktionalität:**
- Bannt Benutzer für konfigurierte Zeit
- Schließt Ticket
- Sendet Ablehnungsnachricht
- Protokolliert Aktion

---

## 📊 Debug-Utilities

### **Debug-Trace**

#### **DebugTrace.error(message, error)**
Loggt Fehler.

```javascript
const { DebugTrace } = require('./utils/debug');

// Verwendung
DebugTrace.error("Fehler beim Erstellen des Tickets", error);
```

**Parameter:**
- `message` - Fehlermeldung (String)
- `error` - Error-Objekt (Error)

#### **DebugTrace.warn(message)**
Loggt Warnungen.

```javascript
const { DebugTrace } = require('./utils/debug');

// Verwendung
DebugTrace.warn("Benutzer hat bereits ein Ticket");
```

**Parameter:**
- `message` - Warnmeldung (String)

#### **DebugTrace.info(message)**
Loggt Informationen.

```javascript
const { DebugTrace } = require('./utils/debug');

// Verwendung
DebugTrace.info("Ticket erfolgreich erstellt");
```

**Parameter:**
- `message` - Informationsmeldung (String)

---

## 🔄 Command-Deployer

### **deployCommands(client, commands)**
Deployt Slash-Commands.

```javascript
const { deployCommands } = require('./utils/commandDeployer');

// Verwendung
await deployCommands(client, commands);
```

**Parameter:**
- `client` - Discord.js Client Objekt
- `commands` - Array von Command-Objekten

**Funktionalität:**
- Registriert Slash-Commands
- Aktualisiert bestehende Commands
- Loggt Deployment-Status

---

## 📝 Datenstrukturen

### **Command-Struktur**
```javascript
module.exports = {
    data: new SlashCommandBuilder()
        .setName("commandname")
        .setDescription("Beschreibung"),
    
    async execute(interaction) {
        // Command-Logik
    },
    
    async autocomplete(interaction) {
        // Autocomplete-Logik (optional)
    }
};
```

### **Input-Struktur**
```javascript
const inputs = {
    fullName: "Max Mustermann",
    age: "25",
    gender: "Männlich",
    rpExperience: "2 Jahre",
    characterIntro: "Mein Charakter ist...",
    characterGoals: "Meine Ziele sind..."
};
```

### **Localization-Struktur**
```javascript
const local = {
    entryPanel: {
        title: "Einreise-Panel",
        description: "Willkommen!",
        ticket_created: "Ticket erstellt!"
    },
    error: {
        already_ticket: "Du hast bereits ein Ticket!",
        no_staff: "Du bist kein Staff!"
    }
};
```

---

## 🚀 Performance-Tipps

### **Datenbank-Optimierung**
```javascript
// Batch-Operationen verwenden
await db.set(key1, value1);
await db.set(key2, value2);

// Caching für häufige Abfragen
const staffRoles = await getStaffRoleIds(guildId);
// Cache für 5 Minuten
```

### **Memory-Management**
```javascript
// Große Objekte nach Verwendung löschen
delete largeObject;

// Garbage Collection manuell auslösen
if (global.gc) {
    global.gc();
}
```

### **Error-Handling**
```javascript
// Try-Catch für kritische Operationen
try {
    await criticalOperation();
} catch (error) {
    DebugTrace.error("Kritischer Fehler", error);
    await fallbackOperation();
}
```

---

**Viel Erfolg bei der Entwicklung! 🛡️** 