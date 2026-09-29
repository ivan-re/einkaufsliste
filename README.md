# 🛒 Einkaufsliste

Eine schlanke Web-App zum Planen, Teilen und Abhaken von Einkaufslisten – komplett in einer einzigen `index.html`, ohne Build-Schritt und ohne Installation.

**Live:** https://ivan-re.github.io/einkaufsliste/

## Funktionen

- **Listen anlegen:** Neue Listen starten als *offen* und *privat*.
- **Positionen erfassen:** Artikel mit Menge, Einheit (Stk, kg, l, Pack …), Kategorie und optionaler Notiz. Doppelte Artikel werden erkannt und die Menge wird erhöht.
- **Kategorien:** Obst & Gemüse, Milch & Kühlung, Fleisch & Fisch, Brot, Getränke, Vorrat, Tiefkühl, Haushalt, Sonstiges.
- **Abhaken:** Erledigte Positionen rutschen nach unten, ein Fortschrittsbalken zeigt den Stand.
- **Mengen anpassen:** direkt in der Liste mit `+` / `−` oder per Eingabe.
- **Einkauf abschliessen:** mit Datum, Uhrzeit und Laden (Coop, Migros, Aldi, Lidl, Denner, Spar oder frei). Abgeschlossene Listen sind schreibgeschützt.
- **Historie & Vorlagen:** Abgeschlossene Einkäufe lassen sich nach Laden filtern und als Vorlage für eine neue Liste wiederverwenden.
- **Teilen:** Listen öffentlich machen oder gezielt per User-ID freigeben, jeweils mit Recht *Lesen* oder *Bearbeiten*.
- **Suche:** über Listentitel, Laden und Artikel.

## Datenspeicherung

Die App kennt zwei Modi:

| Modus | Wann aktiv | Speicherort | Teilen zwischen Geräten |
|---|---|---|---|
| **Lokal** (Standard) | `FIREBASE_CONFIG` ist `null` | `localStorage` des Browsers | ❌ nein |
| **Firebase** | `FIREBASE_CONFIG` ist gesetzt | Cloud Firestore | ✅ ja |

Im lokalen Modus bleiben die Daten nur im jeweiligen Browser auf dem jeweiligen Gerät. Wenn du die Browserdaten löschst, sind auch die Listen weg.

### Firebase einrichten (optional)

1. Auf [console.firebase.google.com](https://console.firebase.google.com) ein Projekt anlegen und darin eine **Web-App** registrieren.
2. Unter **Authentication → Sign-in method** die Anmeldeart **Anonym** aktivieren.
3. Unter **Authentication → Settings → Autorisierte Domains** `ivan-re.github.io` hinzufügen.
4. Eine **Firestore-Datenbank** anlegen und Sicherheitsregeln setzen.
5. Die Konfiguration der Web-App in `index.html` eintragen:

```js
const FIREBASE_CONFIG = {
    apiKey: "...",
    authDomain: "...",
    projectId: "...",
    storageBucket: "...",
    messagingSenderId: "...",
    appId: "..."
};
```

> ⚠️ Alle Listen liegen in einer gemeinsamen Sammlung. Wer eine Liste sehen darf, entscheidet heute nur die App im Browser. Für echten Datenschutz braucht es passende Firestore-Sicherheitsregeln.

## Lokal starten

Weil die App ES-Module verwendet, solltest du sie über einen lokalen Webserver öffnen statt per Doppelklick:

```bash
npx serve .
# oder
python -m http.server 8000
```

Danach `http://localhost:8000` (bzw. die angezeigte Adresse) im Browser öffnen.

## Technik

- HTML + Vanilla JavaScript (ES-Module)
- [Tailwind CSS](https://tailwindcss.com) (CDN)
- [Font Awesome](https://fontawesome.com) für Icons
- [Firebase](https://firebase.google.com) Auth + Firestore (optional)

## Bekannte Einschränkungen

- Bei gleichzeitiger Bearbeitung derselben Liste durch mehrere Personen gewinnt die zuletzt gespeicherte Änderung.
- Die Funktion „Neues Test-Profil erzeugen“ dient nur zum Testen von Freigaben auf einem Gerät.

## Entstehung

Ursprünglich mit Google Gemini Canvas generiert. Anschliessend so angepasst, dass die App auch ausserhalb von Canvas (z. B. auf GitHub Pages) läuft.
