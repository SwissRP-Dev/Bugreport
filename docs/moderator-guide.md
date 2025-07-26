# 🛡️ Moderator Guide

## 📋 Übersicht

Diese Anleitung ist speziell für **Moderatoren** gedacht, die den Swiss RP Einreisebot verwenden möchten. Als Moderator hast du Zugriff auf alle Ticket-Management-Funktionen, aber keine Administrator-Berechtigungen für die Bot-Konfiguration.

---

## 🎯 Was du als Moderator tun kannst

### ✅ **Verfügbare Funktionen:**
- Tickets annehmen/ablehnen/schließen
- Termine für Benutzer setzen
- Tickets beanspruchen und freigeben
- Benutzer-Antworten einsehen
- Termine ändern lassen

### ❌ **Nicht verfügbare Funktionen:**
- Bot-Konfiguration ändern
- Rollen einrichten
- Zeitslots setzen
- Kategorien erstellen

---

## 🎫 **Ticket-Management System**

### **1. Ticket-Status verstehen**

Jedes Ticket durchläuft verschiedene Phasen:

```
📝 **Erstellt** → 📅 **Termin ausgewählt** → ⏳ **Warten auf Review** → ✅ **Angenommen** / ❌ **Abgelehnt** / 🔒 **Geschlossen**
```

### **2. Ticket-Buttons verwenden**

In jedem Ticket findest du diese Buttons:

| Button | Funktion | Wann verwenden |
|--------|----------|----------------|
| ✅ **Accept** | Ticket annehmen | Benutzer erfüllt alle Anforderungen |
| ❌ **Reject** | Ticket ablehnen | Benutzer erfüllt Anforderungen nicht |
| 🔒 **Close** | Ticket schließen | Ticket ist erledigt, aber nicht angenommen |
| 🔄 **Change** | Termin ändern lassen | Benutzer soll Termin ändern können |

---

## 🎯 **Ticket Claiming System**

### **Warum Tickets beanspruchen?**

Das Claiming-System verhindert, dass mehrere Moderatoren gleichzeitig an einem Ticket arbeiten.

### **So funktioniert es:**

1. **Ticket beanspruchen:**
   ```
   /claimticket
   ```
   - Nur du kannst das Ticket bearbeiten
   - Andere Moderatoren sehen eine Benachrichtigung
   - Du bekommst exklusive Berechtigungen

2. **Ticket freigeben:**
   ```
   /releaseticket
   ```
   - Andere Moderatoren können das Ticket übernehmen
   - Verwende dies, wenn du fertig bist

### **Wann beanspruchen?**
- ✅ Du beginnst mit der Bearbeitung eines Tickets
- ✅ Du möchtest verhindern, dass andere Moderatoren eingreifen
- ✅ Du arbeitest an einem komplexen Fall

---

## 📅 **Termin-Management**

### **Problem: Benutzer kann Termin nicht auswählen**

Wenn ein Benutzer seinen Termin nicht auswählen kann (z.B. wegen Timeout), kannst du als Moderator den Termin manuell setzen:

```
/setusertimeslot user:@Benutzername day:Montag timeslot:18:00-19:00
```

### **Verfügbare Tage:**
- Montag, Dienstag, Mittwoch, Donnerstag, Freitag, Samstag, Sonntag

### **Zeitslots finden:**
Die verfügbaren Zeitslots werden automatisch vorgeschlagen. Du musst nur den gewünschten Slot aus der Liste auswählen.

### **Beispiel:**
```
/setusertimeslot user:@MaxMustermann day:Freitag timeslot:19:00-20:00
```

**Ergebnis:**
- Termin wird für den Benutzer gesetzt
- Ticket wird automatisch aktualisiert
- Benutzer bekommt eine Benachrichtigung

---

## 🔍 **Benutzer-Informationen einsehen**

### **Antworten eines Benutzers anzeigen:**

```
/getanswers user:@Benutzername
```

**Was du siehst:**
- Vollständiger Name
- Alter
- Geschlecht
- RP-Erfahrung
- Charakter-Introduction & Ziele

### **Verfügbare Zeitslots anzeigen:**

```
/gettimeslots
```

Zeigt alle konfigurierten Zeitslots für den Server an.

---

## 🎯 **Praktische Workflows**

### **Workflow 1: Standard-Ticket-Bearbeitung**

1. **Ticket beanspruchen:**
   ```
   /claimticket
   ```

2. **Antworten prüfen:**
   ```
   /getanswers user:@Benutzername
   ```

3. **Entscheidung treffen:**
   - **Annehmen:** ✅ Accept Button
   - **Ablehnen:** ❌ Reject Button
   - **Weitere Fragen:** Im Ticket chatten

4. **Ticket freigeben:**
   ```
   /releaseticket
   ```

### **Workflow 2: Termin-Problem lösen**

1. **Problem identifizieren:**
   - Benutzer kann Termin nicht auswählen
   - Termin-Interaktion ist abgelaufen

2. **Termin manuell setzen:**
   ```
   /setusertimeslot user:@Benutzername day:Freitag timeslot:18:00-19:00
   ```

3. **Ticket normal bearbeiten**

### **Workflow 3: Komplexer Fall**

1. **Ticket beanspruchen**
2. **Antworten prüfen**
3. **Fragen stellen** (im Ticket chatten)
4. **Termin setzen** (falls nötig)
5. **Entscheidung treffen**
6. **Ticket freigeben**

---

## 🚨 **Häufige Probleme & Lösungen**

### **Problem: "Du bist kein Staff"**
**Lösung:** Du brauchst eine Staff-Rolle. Kontaktiere einen Administrator.

### **Problem: "Benutzer hat kein aktives Ticket"**
**Lösung:** Der Benutzer muss zuerst ein Ticket über das Einreise-Panel erstellen.

### **Problem: "Ticket ist bereits beansprucht"**
**Lösung:** Warte, bis der andere Moderator das Ticket freigibt, oder kontaktiere ihn.

### **Problem: "Ungültiger Zeitslot"**
**Lösung:** Verwende `/gettimeslots` um verfügbare Slots zu sehen.

### **Problem: Benutzer kann Termin nicht ändern**
**Lösung:** Verwende `/setusertimeslot` um den Termin manuell zu setzen.

---

## 📝 **Best Practices**

### **✅ Do's:**
- **Tickets beanspruchen** bevor du beginnst
- **Antworten gründlich prüfen** vor Entscheidungen
- **Freundlich kommunizieren** mit Bewerbern
- **Tickets freigeben** wenn du fertig bist
- **Logs prüfen** für wichtige Informationen

### **❌ Don'ts:**
- **Nicht mehrere Tickets gleichzeitig** beanspruchen
- **Nicht vorschnell entscheiden** ohne Antworten zu prüfen
- **Nicht Tickets offen lassen** ohne sie freizugeben
- **Nicht persönliche Daten** außerhalb des Tickets teilen

---

## 🔧 **Verfügbare Befehle für Moderatoren**

| Befehl | Beschreibung | Beispiel |
|--------|--------------|----------|
| `/claimticket` | Ticket beanspruchen | `/claimticket` |
| `/releaseticket` | Ticket freigeben | `/releaseticket` |
| `/setusertimeslot` | Termin für Benutzer setzen | `/setusertimeslot user:@Max day:Freitag timeslot:18:00-19:00` |
| `/getanswers` | Benutzer-Antworten anzeigen | `/getanswers user:@Max` |
| `/gettimeslots` | Verfügbare Zeitslots anzeigen | `/gettimeslots` |

---

## 🎯 **Ticket-Buttons Erklärung**

### **✅ Accept Button**
- **Wann:** Benutzer erfüllt alle Anforderungen
- **Was passiert:** 
  - Benutzer bekommt Roleplay-Rolle
  - Applicant-Rolle wird entfernt
  - Ticket wird automatisch geschlossen
  - Benutzer bekommt DM mit Bestätigung

### **❌ Reject Button**
- **Wann:** Benutzer erfüllt Anforderungen nicht
- **Was passiert:**
  - Benutzer wird für konfigurierte Zeit gebannt
  - Ticket wird automatisch geschlossen
  - Benutzer bekommt DM mit Ablehnung

### **🔒 Close Button**
- **Wann:** Ticket ist erledigt, aber nicht angenommen
- **Was passiert:**
  - Ticket wird in "Geschlossen"-Kategorie verschoben
  - Benutzer kann Ticket nicht mehr sehen
  - Ticket kann später gelöscht werden

### **🔄 Change Button**
- **Wann:** Benutzer soll Termin ändern können
- **Was passiert:**
  - Benutzer kann Termin erneut auswählen
  - Nur verfügbar innerhalb der konfigurierten Zeit

---

## 📞 **Support**

### **Bei Problemen:**
1. **Prüfe diese Anleitung** zuerst
2. **Kontaktiere einen Administrator** für Bot-Konfiguration
3. **Frage andere Moderatoren** für Workflow-Fragen

### **Wichtige Kontakte:**
- **Bot-Administrator:** Für Konfigurationsprobleme
- **Server-Administrator:** Für Berechtigungsprobleme
- **Andere Moderatoren:** Für Workflow-Fragen

---

## 🎉 **Fazit**

Als Moderator hast du alle notwendigen Werkzeuge, um Tickets effizient zu bearbeiten. Das Claiming-System sorgt für eine geordnete Arbeitsweise, und die verfügbaren Befehle ermöglichen es dir, alle Situationen professionell zu handhaben.

**Viel Erfolg bei der Moderation! 🛡️** 