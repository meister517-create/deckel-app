# Deckel-App – Weihnachtskegeln 🎳

Digitale Kneipen-Deckel für die Kegelrunde. Der Code liegt auf **GitHub** und wird über **GitHub Pages** veröffentlicht. Die Deckel speichert **Firebase Firestore**, sodass alle Handys live dieselben Striche sehen.

## Die Dateien

| Datei | Wofür |
|---|---|
| `index.html` | Die komplette App (Frontend, Backend, Runden, Design) |
| `firebase-config.js` | Deine Firebase-Zugangsdaten (trägst du in Schritt 1.3 ein) |
| `firestore.rules` | Regeln, wer was in die Datenbank schreiben darf (Schritt 1.5) |
| `firebase.json` | Nur nötig, wenn du statt GitHub Pages Firebase Hosting nutzt (siehe Anhang) |

Backend-Passwort: **Dortmunder Kegelbruder** (zu ändern in `index.html`, ziemlich weit oben: `const PASSWORD = …`)

---

## Teil 1 – Firebase einrichten (ca. 10 Minuten)

### 1.1 Projekt anlegen
1. Öffne <https://console.firebase.google.com> und melde dich mit deinem Google-Konto an.
2. Klicke auf **„Projekt hinzufügen“** bzw. **„Firebase-Projekt erstellen“**.
3. Gib als Namen zum Beispiel `deckel-app` ein und klicke auf **Weiter**.
4. **Google Analytics** brauchst du nicht. Schalte es aus und klicke auf **Projekt erstellen**.
5. Wenn das Projekt fertig ist, klicke auf **Weiter**.

### 1.2 Web-App registrieren
1. Klicke auf der Projektübersicht auf das Symbol **`</>`** (Web).
2. App-Spitzname: `Deckel-App`. Den Haken bei *Firebase Hosting* setzt du **nicht**.
3. Klicke auf **App registrieren**.

### 1.3 Zugangsdaten in `firebase-config.js` eintragen
1. Firebase zeigt dir jetzt einen Code-Block mit `const firebaseConfig = { apiKey: "...", ... }`.
2. Öffne `firebase-config.js` in einem Texteditor und ersetze die sechs Werte (`apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId`, `appId`) durch die Werte aus Firebase.
3. Speichern. Die Werte sind nicht geheim und dürfen öffentlich auf GitHub liegen.

> Später findest du die Werte wieder unter **Zahnrad ⚙️ → Projekteinstellungen → Allgemein → Meine Apps → Konfiguration**.

### 1.4 Datenbank (Firestore) anlegen
1. Wähle im linken Menü **Erstellen → Firestore Database** und klicke auf **Datenbank erstellen**.
2. Standort: **`europe-west3 (Frankfurt)`**. Den Standort kannst du später nicht mehr ändern.
3. Modus: **„Im Produktionsmodus starten“**, dann auf **Erstellen** klicken.

### 1.5 Regeln eintragen
1. Öffne in der Firestore-Ansicht den Reiter **Regeln**.
2. Lösche alles, was dort steht, und füge den kompletten Inhalt von `firestore.rules` ein.
3. Klicke auf **Veröffentlichen**.

Mehr musst du in Firebase nicht einrichten. Der kostenlose **Spark-Tarif** reicht für einen Kegelabend locker aus.

---

## Teil 2 – GitHub & Veröffentlichung (ca. 5 Minuten)

### 2.1 Repository anlegen
1. Öffne <https://github.com>, melde dich an und klicke oben rechts auf **+ → New repository**.
2. Repository name: `deckel-app`
3. Sichtbarkeit: **Public**. GitHub Pages ist für private Repos nur in bezahlten Tarifen verfügbar.
4. Klicke auf **Create repository**.

### 2.2 Dateien hochladen
1. Klicke im leeren Repository auf **„uploading an existing file“** (oder auf **Add file → Upload files**).
2. Ziehe diese Dateien hinein: `index.html`, `firebase-config.js` (mit deinen eingetragenen Werten!), `firestore.rules`, `firebase.json`, `README.md`.
3. Klicke unten auf **Commit changes**.

### 2.3 GitHub Pages einschalten
1. Öffne im Repository **Settings → Pages** (im linken Menü).
2. Stelle unter *Build and deployment → Source* **Deploy from a branch** ein.
3. Branch: **`main`**, Ordner: **`/ (root)`**, dann **Save** klicken.
4. Warte 1–2 Minuten und lade die Seite neu. Oben erscheint dann:
   **„Your site is live at `https://DEIN-NAME.github.io/deckel-app/`“**

Diesen Link schickst du in die Kegel-Gruppe. 🍻

---

## Teil 3 – Testen vor dem Abend

1. Öffne den Link. Wenn ein roter Hinweis *„Firebase ist noch nicht eingerichtet“* erscheint, fehlen die Werte in `firebase-config.js`.
2. Trage einen Testnamen ein und buche ein Bier.
3. Öffne den Link auf einem zweiten Handy. Der Strich sollte dort sofort auftauchen.
4. In Firebase unter **Firestore Database → Daten** siehst du jetzt die Sammlungen `players`, `entries` und `config`.
5. Beim ersten Start legt die App die fünf Standard-Getränke automatisch an. Preise und Reihenfolge passt du im **Backend** an (Link unten auf der Seite).
6. Vor dem Abend setzt du im Backend unter **„Alles auf Null“** alles zurück und hakst dabei *„Auch alle Namen löschen“* an.

---

## Später etwas ändern

- **Code ändern:** Öffne die Datei auf GitHub, klicke auf den Stift ✏️, ändere den Text und klicke auf *Commit changes*. Nach ca. 1 Minute ist die Änderung online.
- **Getränke/Preise:** Die änderst du im Backend der App, dafür brauchst du keinen Code.
- **Eigene Domain** (wie beim Börde-Cup): Trage sie unter **Settings → Pages → Custom domain** ein. Bei deinem Domain-Anbieter legst du dann einen `CNAME`-Eintrag auf `DEIN-NAME.github.io` an.

## Gut zu wissen

- Jeder, der den Link hat, kann Striche setzen. Gib den Link also nur in die Runde.
- Das Backend-Passwort schützt vor versehentlichen Änderungen. Es steht aber im Code der Seite und ist damit kein echter Sicherheitsschutz. Für einen Kegelabend reicht das.
- Eine Runde, die gerade zusammengestellt wird, existiert nur auf dem Handy, auf dem sie zusammengestellt wird. Erst **„Runde beenden & buchen“** schreibt sie in die Datenbank.

---

## Anhang – Firebase Hosting statt GitHub Pages (optional)

Wenn der Börde-Cup über Firebase Hosting lief, kannst du hier genauso vorgehen:

```bash
npm install -g firebase-tools
firebase login
cd deckel-app            # Ordner mit den Dateien
firebase use --add       # dein Projekt auswählen
firebase deploy          # lädt App + Firestore-Regeln hoch
```

Die App ist danach unter `https://DEIN-PROJEKT.web.app` erreichbar. Automatisch bei jedem GitHub-Commit deployen geht über `firebase init hosting:github`.
