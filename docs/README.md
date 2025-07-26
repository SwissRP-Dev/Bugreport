# 🛡️ Swiss RP Einreisebot

> **Professioneller Discord Bot für Roleplay-Einreiseanfragen**

Der Swiss RP Einreisebot ist ein fortschrittlicher Discord Bot, der speziell für Roleplay-Server entwickelt wurde. Er automatisiert den gesamten Einreise-Prozess von der Bewerbung bis zur Genehmigung.

## ✨ Features

- 🎫 **Automatisches Ticket-System** - Private Kanäle für jede Bewerbung
- 📅 **Termin-Management** - Flexible Zeitslot-Verwaltung
- 🛡️ **Staff-Management** - Erweiterte Moderator-Funktionen
- 🔒 **Ticket-Claiming** - Verhindert Konflikte zwischen Moderatoren
- 📊 **Logging-System** - Vollständige Protokollierung aller Aktionen
- 🌍 **Mehrsprachig** - Deutsch und Englisch unterstützt
- ⚡ **Autocomplete** - Intelligente Zeitslot-Vorschläge

## 🚀 Schnellstart

### Voraussetzungen
- Discord Bot Token
- Node.js 16+ 
- Administrator-Berechtigungen auf dem Discord Server

### Installation
```bash
# Repository klonen
git clone [repository-url]
cd swiss-rp-einreisebot

# Abhängigkeiten installieren
npm install

# Konfiguration
cp env.example .env
# .env Datei bearbeiten

# Bot starten
npm start
```

### Erste Einrichtung
```bash
# Automatische Setup
/setup applicant_role:@Bewerber roleplay_role:@Roleplay staff_role:@Moderator logs_channel:#logs

# Einreise-Panel erstellen
/sendentrypanel channel:#einreise
```

## 📚 Dokumentation

- **[Administrator Guide](admin-guide.md)** - Vollständige Bot-Konfiguration
- **[Moderator Guide](moderator-guide.md)** - Anleitung für Moderatoren
- **[Befehlsreferenz](commands.md)** - Alle verfügbaren Befehle
- **[Troubleshooting](troubleshooting.md)** - Häufige Probleme und Lösungen

## 🎯 Hauptfunktionen

### Für Administratoren
- **Automatische Setup** - Ein-Klick-Konfiguration
- **Flexible Rollenverwaltung** - Unbegrenzte Staff-Rollen
- **Zeitslot-Management** - 24h/12h Format unterstützt
- **Kategorie-Management** - Automatische Kanal-Erstellung

### Für Moderatoren
- **Ticket-Claiming** - Exklusive Ticket-Bearbeitung
- **Termin-Setzung** - Manuelle Terminvergabe
- **Antworten-Review** - Vollständige Bewerber-Informationen
- **Schnelle Entscheidungen** - Accept/Reject/Close Buttons

### Für Bewerber
- **Einfache Bewerbung** - Modal-basierte Eingabe
- **Termin-Auswahl** - Dropdown-basierte Zeitslots
- **Status-Updates** - Automatische Benachrichtigungen
- **DM-Benachrichtigungen** - Direkte Kommunikation

## 🔧 Technische Details

- **Framework:** Discord.js v14
- **Datenbank:** pro.db (SQLite-basiert)
- **Sprachen:** JavaScript/Node.js
- **Architektur:** Modulare Struktur mit Utils

## 📞 Support

Bei Fragen oder Problemen:
1. **Dokumentation prüfen** - Diese Seiten durchsuchen
2. **Issues erstellen** - GitHub Issues verwenden
3. **Community kontaktieren** - Discord Server besuchen

## 📄 Lizenz

Dieses Projekt ist unter der MIT-Lizenz lizenziert.

---

**Entwickelt mit ❤️ für die Swiss RP Community** 