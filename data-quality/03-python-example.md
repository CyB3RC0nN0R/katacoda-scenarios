In diesem Praxisbeispiel lesen wir mithilfe der Python-Bibliothek [Pandas](https://pandas.pydata.org) Fahrzeugdaten ein, die in einer CSV-Datei vorliegen und untersuchen diese anschließend auf einen bestimmten Qualitätsmangel, nämlich fehlende Merkmale in den einzelnen Datenpunkten.

# Rohdaten betrachten

Da es sich um einen sehr kleinen Datensatz handelt, lässt sich dieser direkt in der Konsole mit `cat vehicles.csv`{{execute T1}} betrachten.
In einem echten Projekt sind mächtigere Werkzeuge, beispielsweise ein Jupyter Notebook, hilfreich.

# Trennungs-Skript schreiben

Nun verfassen wir ein kleines Python-Skript, das den Fahrzeugdatensatz als CSV einliest, und ihn anschließend in zwei CSV-Dateien mit vollständigen bzw. fehlenden Datenpunkten unterteilt.

Zunächst wird die Pandas-Bibliothek importiert.
Wie dabei üblich, definieren wir für Pandas das Kürzel `pd`, um später darauf zuzugreifen.

<pre class="file" data-filename="split.py" data-target="append">
import pandas as pd
</pre>

Als nächstes wird die CSV-Datei mir den Rohdaten aus `vehicles.csv` in ein Pandas Dataframe eingelesen.
Dabei handelt es sich um eine tabellarische Datenstruktur, die den Inhalt der CSV-Datei abbilden kann.
Sie definiert eine Vielzahl hilfreicher Funktionen, um die Daten zu untersuchen und zu manipulieren.

<pre class="file" data-filename="split.py" data-target="append">
data = pd.read_csv('vehicles.csv')
</pre>

Aus dem nun eingelesenen Datensatz können wir die vollständigen Reihen abspalten.
Dies wird mit der Funktion `dropna` des Dataframes erzielt, welches unvollständige Reihen entfernet.
Das ursprüngliche Dataframe bleibt dabei erhalten, denn es wird eine Kopie mit dem Ergebnis angelegt.

<pre class="file" data-filename="split.py" data-target="append">
data_complete = data.dropna()
</pre>

Ähnlich verfahren wir mit den unvollständigen Daten.
Dazu muss erst mit der Funktion `isna` selektiert werden, welche Reihen unvollständig sind, um dann ein neues Dataframe mit eben diesen Reihen zu erstellen.

<pre class="file" data-filename="split.py" data-target="append">
data_incomplete = data[data.isna().any(axis=1)]
</pre>

Die zwei so gewonnenen Dataframes werden nun in jeweils eine CSV-Datei exportiert.

<pre class="file" data-filename="split.py" data-target="append">
data_complete.to_csv('vehicles_complete.csv')
data_incomplete.to_csv('vehicles_incomplete.csv')
</pre>

# Ausführung und Überprüfung

Mit `python3 split.py`{{execute T1}} kann das Skript gestartet werden.
Wenn alles funktioniert hat, wurden die zwei Dateien `vehicles_complete.csv` und `vehicles_incomplete.csv` angelegt.
Diese betrachten wir nun einzeln:

`cat vehicles_complete.csv`{{execute T1}}

`cat vehicles_incomplete.csv`{{execute T1}}

Wie in der Konsole zu sehen, wurden die unvollständigen Daten von den vollständigen getrennt, und können separat weiterverarbeitet werden, beispielsweise durch Weitergabe an die Fachabteilung.