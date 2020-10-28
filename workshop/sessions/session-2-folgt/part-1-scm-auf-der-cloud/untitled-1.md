# Code ändern und pushen

Jetzt ist alles vorbereitet und ihr könnt den Code lokal entwickeln und die Änderungen sind unter localhost:3000 sichtbar. Im Beispiel machen wir testweise nochmal eine Änderung auf public/index.html.

Um sie ins SCM auf der Cloud zu pushen müssen wir:

```text
git add .
```

* fügt alles geänderte hinzu, dafür ist der PUNKT\)
  * oder git add public/index.html \(fügt nur diese datei hinzu\)

```text
git commit -m "kleiner change"
```

* loggt die änderung in eurer lokalen versionsverwaltung verbindlich ein

```text
git push
```

* check es ins IBM gitlab ein und macht euren lokalen "commit" zu einem commit in der zentralen Codeverwaltung
* schaut auf eure Delivery Pipeline --&gt; sollte "in progress" sein, da ein webhook auf den commit existiert

Sollte man auf "master" pushen? Nein - in der Praxis natürlich nicht!

