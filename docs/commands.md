# 🔧 Befehlsreferenz

## 📋 Übersicht

Diese Seite enthält alle verfügbaren Befehle des Swiss RP Einreisebots, kategorisiert nach Benutzerrollen und Funktionalität.

---

## 🛡️ Administrator-Befehle

### **Setup & Konfiguration**

| Befehl | Beschreibung | Syntax | Beispiel |
|--------|--------------|--------|----------|
| `/setup` | Automatische Bot-Konfiguration | `/setup applicant_role:@Rolle roleplay_role:@Rolle staff_role:@Rolle logs_channel:#Kanal` | `/setup applicant_role:@Bewerber roleplay_role:@Roleplay staff_role:@Moderator logs_channel:#logs` |
| `/setroles` | Rollen manuell konfigurieren | `/setroles [type] role:@Rolle` | `/setroles applicant role:@Bewerber` |
| `/addstaffrole` | Staff-Rolle hinzufügen | `/addstaffrole role:@Rolle` | `/addstaffrole role:@Helper` |
| `/removestaffrole` | Staff-Rolle entfernen | `/removestaffrole role:@Rolle` | `/removestaffrole role:@Helper` |
| `/liststaffroles` | Alle Staff-Rollen anzeigen | `/liststaffroles` | `/liststaffroles` |

### **Zeitslot-Management**

| Befehl | Beschreibung | Syntax | Beispiel |
|--------|--------------|--------|----------|
| `/settimeslots` | Zeitslots konfigurieren | `/settimeslots slots:"Zeitslot1, Zeitslot2"` | `/settimeslots slots:"18:00-19:00, 19:00-20:00"` |
| `/gettimeslots` | Zeitslots anzeigen | `/gettimeslots` | `/gettimeslots` |
| `/cleartimeslots` | Zeitslots zurücksetzen | `/cleartimeslots` | `/cleartimeslots` |

### **Zeitzone & Zeit-Management**

| Befehl | Beschreibung | Syntax | Beispiel |
|--------|--------------|--------|----------|
| `/timezone set` | Zeitzone setzen | `/timezone set timezone:Region/Stadt` | `/timezone set timezone:Europe/Zurich` |
| `/timezone get` | Zeitzone anzeigen | `/timezone get` | `/timezone get` |
| `/setchangetime` | Termin-Änderungszeit setzen | `/setchangetime minutes:Zahl` | `/setchangetime minutes:15` |
| `/setbantime` | Ban-Dauer setzen | `/setbantime hours:Zahl` | `/setbantime hours:24` |

### **Kategorie-Management**

| Befehl | Beschreibung | Syntax | Beispiel |
|--------|--------------|--------|----------|
| `/setticketcategory` | Ticket-Kategorie setzen | `/setticketcategory category:#Kategorie` | `/setticketcategory category:#Tickets` |
| `/setcloseticketcategory` | Geschlossene-Tickets-Kategorie setzen | `/setcloseticketcategory category:#Kategorie` | `/setcloseticketcategory category:#ClosedTickets` |

### **Panel & Nachrichten**

| Befehl | Beschreibung | Syntax | Beispiel |
|--------|--------------|--------|----------|
| `/sendentrypanel` | Einreise-Panel senden | `/sendentrypanel channel:#Kanal` | `/sendentrypanel channel:#einreise` |
| `/setweltext` | Willkommensnachricht setzen | `/setweltext message:"Nachricht"` | `/setweltext message:"Willkommen {username}!"` |

### **Logging**

| Befehl | Beschreibung | Syntax | Beispiel |
|--------|--------------|--------|----------|
| `/setlogs` | Logs-Kanal setzen | `/setlogs channel:#Kanal` | `/setlogs channel:#logs` |

---

## 🛡️ Moderator-Befehle

### **Ticket-Management**

| Befehl | Beschreibung | Syntax | Beispiel |
|--------|--------------|--------|----------|
| `/claimticket` | Ticket beanspruchen | `/claimticket` | `/claimticket` |
| `/releaseticket` | Ticket freigeben | `/releaseticket` | `/releaseticket` |
| `/setusertimeslot` | Termin für Benutzer setzen | `/setusertimeslot user:@Benutzer day:Tag timeslot:Zeit` | `/setusertimeslot user:@Max day:Freitag timeslot:18:00-19:00` |

### **Informationen abrufen**

| Befehl | Beschreibung | Syntax | Beispiel |
|--------|--------------|--------|----------|
| `/getanswers` | Benutzer-Antworten anzeigen | `/getanswers user:@Benutzer` | `/getanswers user:@Max` |
| `/gettimeslots` | Verfügbare Zeitslots anzeigen | `/gettimeslots` | `/gettimeslots` |

---

## 🎯 Befehls-Details

### **Setup-Befehle**

#### `/setup`
**Beschreibung:** Automatische Bot-Konfiguration mit allen notwendigen Einstellungen.

**Parameter:**
- `applicant_role` - Rolle für neue Bewerber
- `roleplay_role` - Rolle für angenommene Bewerber
- `staff_role` - Haupt-Staff-Rolle
- `logs_channel` - Kanal für Logs

**Beispiel:**
```bash
/setup applicant_role:@Bewerber roleplay_role:@Roleplay staff_role:@Moderator logs_channel:#logs
```

**Was passiert:**
- ✅ Kategorien werden erstellt
- ✅ Rollen werden konfiguriert
- ✅ Berechtigungen werden gesetzt
- ✅ Standard-Einstellungen werden angewendet

#### `/setroles`
**Beschreibung:** Rollen manuell konfigurieren.

**Unterbefehle:**
- `applicant` - Bewerber-Rolle
- `roleplay` - Roleplay-Rolle
- `staff` - Haupt-Staff-Rolle
- `staff2` - Zusätzliche Staff-Rolle
- `staff3` - Zusätzliche Staff-Rolle

**Beispiel:**
```bash
/setroles applicant role:@Bewerber
/setroles roleplay role:@Roleplay
/setroles staff role:@Moderator
```

### **Zeitslot-Befehle**

#### `/settimeslots`
**Beschreibung:** Zeitslots für Termine konfigurieren.

**Unterstützte Formate:**
- **24-Stunden:** `18:00-19:00`
- **12-Stunden:** `6:00 PM-7:00 PM`
- **Gemischt:** `18:00-7:00 PM`

**Beispiel:**
```bash
/settimeslots slots:"18:00-19:00, 19:00-20:00, 20:00-21:00"
/settimeslots slots:"6:00 PM-7:00 PM, 7:00 PM-8:00 PM"
```

#### `/setusertimeslot`
**Beschreibung:** Termin für einen Benutzer manuell setzen.

**Parameter:**
- `user` - Zielbenutzer
- `day` - Wochentag (Montag-Sonntag)
- `timeslot` - Zeitslot (mit Autocomplete)

**Beispiel:**
```bash
/setusertimeslot user:@MaxMustermann day:Freitag timeslot:18:00-19:00
```

**Features:**
- ✅ Autocomplete für Zeitslots
- ✅ Automatische Ticket-Aktualisierung
- ✅ Benachrichtigung an Benutzer

### **Ticket-Management-Befehle**

#### `/claimticket`
**Beschreibung:** Ticket für exklusive Bearbeitung beanspruchen.

**Verwendung:**
```bash
/claimticket
```

**Was passiert:**
- ✅ Nur du kannst das Ticket bearbeiten
- ✅ Andere Moderatoren werden benachrichtigt
- ✅ Exklusive Berechtigungen werden gesetzt

#### `/releaseticket`
**Beschreibung:** Beanspruchtes Ticket freigeben.

**Verwendung:**
```bash
/releaseticket
```

**Was passiert:**
- ✅ Ticket wird für andere Moderatoren verfügbar
- ✅ Exklusive Berechtigungen werden entfernt
- ✅ Andere Moderatoren werden benachrichtigt

### **Informations-Befehle**

#### `/getanswers`
**Beschreibung:** Antworten eines Benutzers anzeigen.

**Parameter:**
- `user` - Zielbenutzer

**Beispiel:**
```bash
/getanswers user:@MaxMustermann
```

**Angezeigte Informationen:**
- Vollständiger Name
- Alter
- Geschlecht
- RP-Erfahrung
- Charakter-Introduction & Ziele

#### `/gettimeslots`
**Beschreibung:** Alle verfügbaren Zeitslots anzeigen.

**Verwendung:**
```bash
/gettimeslots
```

**Ausgabe:**
```
Zeitslots: 18:00-19:00, 19:00-20:00, 20:00-21:00
```

---

## 🔧 Erweiterte Konfiguration

### **Zeitzone-Einstellungen**

#### `/timezone set`
**Beschreibung:** Server-Zeitzone für Zeitslot-Anzeige setzen.

**Unterstützte Zeitzonen:**
- `Europe/Zurich`
- `Europe/Berlin`
- `America/New_York`
- `UTC`

**Beispiel:**
```bash
/timezone set timezone:Europe/Zurich
```

#### `/timezone get`
**Beschreibung:** Aktuelle Server-Zeitzone anzeigen.

**Verwendung:**
```bash
/timezone get
```

### **Zeit-Management**

#### `/setchangetime`
**Beschreibung:** Zeit für Benutzer zum Ändern von Terminen setzen.

**Parameter:**
- `minutes` - Minuten (1-1440)

**Beispiel:**
```bash
/setchangetime minutes:15
```

#### `/setbantime`
**Beschreibung:** Ban-Dauer für abgelehnte Bewerber setzen.

**Parameter:**
- `hours` - Stunden (1-8760)

**Beispiel:**
```bash
/setbantime hours:24
```

---

## 🚨 Berechtigungen

### **Administrator-Befehle**
- Erfordern Administrator-Berechtigungen
- Können nur von Server-Administratoren verwendet werden
- Ändern Bot-Konfiguration und Server-Einstellungen

### **Moderator-Befehle**
- Erfordern Staff-Rolle oder Administrator-Berechtigungen
- Können von allen Staff-Mitgliedern verwendet werden
- Bearbeiten Tickets und Benutzer-Daten

### **Berechtigungs-Hierarchie**
1. **Administrator** - Alle Befehle verfügbar
2. **Staff-Rolle** - Moderator-Befehle verfügbar
3. **Regulärer Benutzer** - Keine Befehle verfügbar

---

## 📝 Best Practices

### **Für Administratoren**
- ✅ Verwende `/setup` für die erste Konfiguration
- ✅ Setze Staff-Rollen mit `/addstaffrole`
- ✅ Konfiguriere Zeitslots vor dem Start
- ✅ Teste alle Einstellungen vor dem Live-Betrieb

### **Für Moderatoren**
- ✅ Beanspruche Tickets mit `/claimticket`
- ✅ Prüfe Antworten mit `/getanswers`
- ✅ Setze Termine mit `/setusertimeslot`
- ✅ Gib Tickets mit `/releaseticket` frei

### **Allgemein**
- ✅ Verwende Autocomplete für Zeitslots
- ✅ Prüfe Berechtigungen vor Befehlsausführung
- ✅ Konsultiere Logs bei Problemen
- ✅ Halte Dokumentation aktuell

---

## 🔍 Troubleshooting

### **Häufige Fehler**

#### "Du bist kein Staff"
**Lösung:** Staff-Rolle benötigt oder Administrator-Berechtigungen prüfen.

#### "Benutzer hat kein aktives Ticket"
**Lösung:** Benutzer muss zuerst ein Ticket über das Einreise-Panel erstellen.

#### "Ungültiger Zeitslot"
**Lösung:** Verwende `/gettimeslots` um verfügbare Slots zu sehen.

#### "Ticket ist bereits beansprucht"
**Lösung:** Warte bis der andere Moderator das Ticket freigibt.

### **Befehls-Syntax**
- Verwende korrekte Parameter-Namen
- Setze Werte in Anführungszeichen bei Leerzeichen
- Prüfe Rollen- und Kanal-Mentions

---

**Viel Erfolg bei der Verwendung der Befehle! 🛡️** 