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

Die Daten liegen in **Cloud Firestore** (Firebase-Projekt `einkaufsliste-20ef0`). Jeder Browser meldet sich automatisch **anonym** an und bekommt eine eigene User-ID.

- Die App lädt nur Listen, die man sehen darf: eigene, öffentliche und für die eigene User-ID freigegebene.
- Das erzwingen die Sicherheitsregeln in [`firestore.rules`](firestore.rules). Bei Änderungen dort muss man sie in der Firebase-Konsole unter **Firestore → Regeln** neu veröffentlichen.
- Ein Offline-Cache hält die Listen auch bei schlechtem Empfang im Laden nutzbar. Änderungen werden nachgereicht, sobald wieder Verbindung besteht.
- Die anonyme User-ID gilt pro Browser. Handy und PC sind darum zwei verschiedene Nutzer. Listen teilt man über die User-ID im Profil.

**Lokaler Modus:** Setzt man in `index.html` `FIREBASE_CONFIG = null`, speichert die App nur im `localStorage` des Browsers. Dann ist kein Teilen zwischen Geräten möglich.

### Firebase-Einstellungen

1. **Authentication → Sign-in method:** Anmeldeart **Anonym** aktivieren.
2. **Authentication → Settings → Autorisierte Domains:** `ivan-re.github.io` hinzufügen.
3. **Firestore → Regeln:** den Inhalt von `firestore.rules` einfügen und veröffentlichen.

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
- [Firebase](https://firebase.google.com) Auth (anonym) + Cloud Firestore

## Bekannte Einschränkungen

- Bei gleichzeitiger Bearbeitung derselben Liste durch mehrere Personen gewinnt die zuletzt gespeicherte Änderung.
- Wer die Browserdaten löscht, verliert seine anonyme User-ID und damit den Zugriff auf seine Listen.

## Entstehung

Ursprünglich mit Google Gemini Canvas generiert. Anschliessend so angepasst, dass die App auch ausserhalb von Canvas (z. B. auf GitHub Pages) läuft.
