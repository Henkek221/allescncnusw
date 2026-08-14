# shapes-projekt

Jupyter-Notebooks rund um Bildverarbeitung: ein interaktiver Composer fuer industrielle
CT-/Roentgenbilder und zwei kleine neuronale Netze auf einem Formen-Datensatz.

## Inhalt

| Datei | Was drin ist |
|---|---|
| [`ct_composer.ipynb`](ct_composer.ipynb) | Interaktives GUI: Objekte aus einem CT ausschneiden, in ein anderes Bild einsetzen, Groessen in um steuern. Siehe unten. |
| [`cnn.ipynb`](cnn.ipynb) | Mini-CNN, das Quadrate von Dreiecken unterscheidet, mit Lernkurve, Wichtigkeits-Heatmap und Filter-Ansicht. |
| [`autoencoder.ipynb`](autoencoder.ipynb) | Autoencoder auf demselben Datensatz. |
| `shapes_dataset/` | 100 PNGs, je 50 Quadrate und Dreiecke, Trainingsdaten fuer die beiden Netze. |

## CT-Objekt-Composer

Zweck: Objekte bekannter Groesse (z.B. 50 um) aus einem CT ausschneiden, in ein anderes Bild
einsetzen und pruefen, ab welcher Groesse eine Bildauswertung sie noch findet.

1. **Ausschneiden** &ndash; CT laden (Pfad, Upload oder eingebautes Demo-CT), mit der Maus einen
   Rahmen um das Objekt ziehen, Groesse wird in px, um und mm angezeigt. Export als 16-bit PNG.
2. **Platzieren** &ndash; Klick ins Bild legt das Objekt ab, Ziehen verschiebt es, beliebig viele
   Objekte. Groesse in px oder direkt in um. Der Hintergrund ist ein leeres Detektorbild
   (Pixelzahl, Grauwert, Rauschen einstellbar) oder ein eigenes Bild. Export als 16-bit PNG.

Der Uebergang laesst sich weich einstellen: Feather-Kante, Ellipsen-Maske, Kontrast und wahlweise
Angleichen des Patchrands an das lokale Hintergrundniveau. Die Statuszeile zeigt Kontrast und SNR
des aktiven Objekts gegen den Hintergrund.

Das eingebaute Demo-CT ist ein Roentgenbild einer M4-Schraube aus Stahl: der Grauwert kodiert die
durchstrahlte Materialdicke (Beer-Lambert), dazu Detektorunschaerfe und Photonenrauschen. Es
enthaelt Gewinde, Kopf mit Innensechskant, drei Poren und vier Kalibrierkugeln mit
50 / 100 / 200 / 400 um Durchmesser. Gemessen bei 10 um/px gegen den Luftbereich:
SNR 3.2 / 7.1 / 13.2 / 23.0.

## Loslegen

```bash
pip install numpy scipy pillow matplotlib ipywidgets ipympl jupyterlab
jupyter lab
```

Fuer `cnn.ipynb` und `autoencoder.ipynb` zusaetzlich `torch` (CPU reicht).

`ipympl` wird fuer die Maussteuerung im Composer gebraucht &ndash; ohne das Paket sind die
Bildflaechen statisch. Die Notebooks von oben nach unten ausfuehren; der Composer laeuft ohne
eigene Daten mit dem Demo-CT.

## Ordner, die nicht im Repo liegen

`demo_ct/`, `patches/` und `scenes/` sind erzeugte Bilddaten und stehen in `.gitignore` &ndash;
die Notebooks legen sie beim Ausfuehren selbst an.
