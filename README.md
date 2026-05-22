# KanMind Frontend

![KanMind Logo](assets/icons/logo_icon.svg)

Ein Kanban-Board-Frontend, entwickelt mit **Vanilla JavaScript**, HTML und CSS – ohne externe Frameworks. Das Projekt wurde durch die **Developer Akademie** erstellt und bindet sich an ein Django-REST-Backend an.

---

## Voraussetzungen

- **Django-Backend** `KanMind` muss lokal laufen (`http://127.0.0.1:8000/api/`)
- **Visual Studio Code** mit der Erweiterung **Live Server**

---

## Schnellstart

1. Django-Backend starten.
2. Dieses Projekt in VS Code öffnen.
3. Rechtsklick auf `index.html` (oberste Ebene) → **Open with Live Server**.
4. Der Browser öffnet sich und leitet automatisch zur Login-Seite weiter.

> **Gastlogin** ist vorkonfiguriert – einfach auf „Guest Login" klicken.

---

## Projektstruktur

```
04_KanMind-FE/
├── index.html              # Einstiegspunkt – leitet je nach Auth-Status weiter
├── assets/
│   ├── fonts/
│   └── icons/
├── pages/
│   ├── auth/               # Login & Registrierung
│   │   ├── login.html
│   │   └── register.html
│   ├── dashboard/          # Übersicht mit Diagrammen & Aufgabenliste
│   │   ├── dashboard.js
│   │   ├── dashboard_charts.js
│   │   └── index.html
│   ├── boards/             # Board-Übersicht & Board erstellen
│   │   ├── boards.js
│   │   └── index.html
│   ├── board/              # Einzelnes Kanban-Board mit Aufgaben
│   │   ├── board.js
│   │   ├── board_templates.js
│   │   └── index.html
│   ├── imprint/
│   └── privacy/
└── shared/
    ├── css/                # Globale Stylesheets
    │   ├── variables.css   # CSS-Variablen (Farben, Abstände)
    │   ├── standard.css
    │   ├── fonts.css
    │   ├── assets.css
    │   ├── form.css
    │   └── header_footer.css
    └── js/                 # Globale JavaScript-Module
        ├── config.js       # API-Basis-URL & Endpunkte
        ├── api.js          # HTTP-Hilfsfunktionen (GET, POST, PATCH, DELETE)
        ├── auth.js         # Login, Registrierung, Formularvalidierung
        ├── header.js       # Header-Template & Logout
        ├── board_settings.js # Board-Einstellungen & Mitgliederverwaltung
        └── ui_helper.js    # UI-Hilfsfunktionen (Dialoge, Toggles, Fehler)
```

---

## Features

| Bereich | Funktion |
|---|---|
| **Auth** | Login, Registrierung, Gastlogin, Token-basierte Authentifizierung |
| **Dashboard** | Willkommensnachricht, Fortschrittsanzeige (Wave-Chart), Aufgabenverteilung (Pie-Chart/Doughnut via Chart.js), Board-Liste |
| **Boards** | Board-Liste anzeigen, neues Board erstellen, Mitglieder per E-Mail einladen |
| **Board (Kanban)** | Aufgaben in Spalten (`to-do`, `in-progress`, `review`, `done`), Aufgabe erstellen/bearbeiten, Kommentare, Assignee & Reviewer setzen, Priorität & Fälligkeitsdatum |
| **Board-Einstellungen** | Board umbenennen, Mitglieder hinzufügen/entfernen |

---

## API-Anbindung

Die Basis-URL und alle Endpunkte sind in `shared/js/config.js` konfiguriert:

```js
const API_BASE_URL = 'http://127.0.0.1:8000/api/';

const LOGIN_URL            = 'login/';
const REGISTER_URL         = 'registration/';
const BOARDS_URL           = 'boards/';
const MAIL_CHECK_URL       = 'email-check/';
const TASKS_URL            = 'tasks/';
const TASKS_ASSIGNED_URL   = 'tasks/assigned-to-me/';
const TASKS_REVIEWER_URL   = 'tasks/reviewing/';
```

Die Authentifizierung erfolgt per **Token** im `Authorization`-Header. Token und Nutzerinfos werden im `localStorage` gespeichert.

---

## Architektur & Konventionen

- **Kein Build-Step** – alle Dateien werden direkt vom Browser geladen.
- **Shared JS/CSS** – globale Module in `shared/` werden per `<script>`- bzw. `<link>`-Tag in jede Seite eingebunden.
- **Template-Funktionen** – HTML-Strings werden per JavaScript erzeugt und per `innerHTML` eingefügt (z. B. `board_templates.js`).
- **localStorage** – `auth-token`, `auth-user-id`, `auth-email`, `auth-fullname` werden nach dem Login gesetzt und beim Logout gelöscht.

---

## Hinweis

Dieses Projekt ist **ausschließlich für Schüler der Developer Akademie** gedacht und nicht zur freien Nutzung oder Weitergabe freigegeben.

---
