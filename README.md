# EA 10: Seeds Daten in 3D

Einsendeaufgabe 10, Modul Graphical Visualisation Technologies, TH Lübeck, Wintersemester 2026/27.

Eine einseitige Web-App, die den Seeds-Datensatz (210 Weizenkörner, 7 Merkmale,
3 Sorten Kama, Rosa und Canadian) mit t-SNE (Bibliothek tSNEJS) auf drei
Dimensionen reduziert und als interaktive 3D-Punktwolke mit WebGL 1 darstellt.
Beim Start wird das gespeicherte beste Ergebnis geladen. Mit `r` beginnt t-SNE
neu bei Step 0, `t` rechnet einen Schritt, `T` zehn Schritte. Die Navigation
durch die Daten folgt dem Kapitel NAV.

## Live-Demo

Öffentlich erreichbar unter:
<https://merganh.github.io/gvt-ea10-seeds-daten-in-3d/>

## Lokal ausführen

Kein Build-Schritt. Die Seite lädt Dateien per `XMLHttpRequest` und braucht
deshalb einen lokalen Server:

```bash
python3 -m http.server 8000
# dann im Browser: http://localhost:8000
```

## Deployment via GitHub Pages

Im Repo liegt ein Workflow unter `.github/workflows/pages.yml`, der die Seite bei
jedem Push auf `main` automatisch nach GitHub Pages deployt. Einmalig im Repo
unter **Settings → Pages → Build and deployment → Source** `GitHub Actions`
wählen.

## Aufbau

- `index.html`: gesamte Anwendung in einer Datei (HTML, CSS, JS inline)
- `data/seeds.csv`: Seeds-Datensatz von UCI als CSV (ohne Kopfzeile, Komma als Trennzeichen, Klasse 1 bis 3 im letzten Feld)
- `data/seeds-tsne.json`: bestes t-SNE-Ergebnis (3D-Koordinaten, Labels, Parameter, Gütemaße)
- `lib/tsne.js`: tSNEJS von Andrej Karpathy, unveränderte Kopie, MIT-Lizenz

Gespeichertes Ergebnis: Min-Max-Normalisierung, Perplexity 20, Epsilon 10,
1000 Iterationen, kNN-Genauigkeit (k = 5) 94,3 %, Silhouette 0,515.

## Bedienung

- **r**: Restart, t-SNE beginnt bei Step 0 mit neuen Zufallszahlen
- **t**: Step, ein Iterationsschritt
- **T** (Shift+t): Step10, zehn Iterationsschritte
- **x / y / z**: Kamera drehen (Nick, Gier, Roll), mit Shift zurück
- **w / a / s / d**: Kamera verschieben
- **Leertaste**: Kameraflug vorwärts, mit Shift rückwärts
- **b / B**: Zoom hinein bzw. heraus
- **o / p**: orthogonale bzw. perspektivische Projektion
- **0**: Ansicht zurücksetzen
- **k**: aktuelle Karte als `seeds-tsne.json` herunterladen
- **Maus**: ziehen dreht die Kamera, Mausrad zoomt

Restart, Step und Step10 gibt es auch als Buttons.

## Quellen

- Seeds-Datensatz: UCI Machine Learning Repository, DOI 10.24432/C5H30K, CC BY 4.0
- Veröffentlichung: Charytanowicz et al., Complete Gradient Clustering Algorithm for Features Analysis of X-ray Images, 2010, DOI 10.1007/978-3-642-13105-9_2
- tSNEJS: <https://github.com/karpathy/tsnejs>, MIT-Lizenz

## Quelltext-Markierung

Die für die Aufgabe geschriebenen JavaScript-Stellen sind mit
`// START EA10_SEEDS_TSNE` und `// END EA10_SEEDS_TSNE` markiert.
