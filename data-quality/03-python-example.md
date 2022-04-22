In diesem Praxisbeispiel lesen wir mithilfe der Python-Bibliothek Pandas Fahrzeugdaten ein, die in einer CSV-Datei vorliegen und untersuchen diese anschließend auf einen bestimmten Qualitätsmangel, nämlich fehlende Merkmale in den einzelnen Datenpunkten.

# Pandas installieren

Um die Analyse auf unvollständige Werte durchzuführen, wird die Python-Bibliothek [Pandas](pandas.pydata.org) eingesetzt.
Diese kann wie folgt installiert werden:
`python3 -m pip install pandas`{{execute T1}}

# Trennungs-Skript schreiben

Nun verfassen wir ein kleines Python-Skript, das den Fahrzeugdatensatz als CSV einliest, und ihn anschließend in zwei CSV-Dateien mit vollständigen bzw. fehlenden Datenpunkten unterteilt.

<pre class="file" data-filename="split.py" data-target="append">
import pandas as pd
</pre>

<pre class="file" data-filename="split.py" data-target="append">
data = pd.read_csv('vehicles.csv')
</pre>

<pre class="file" data-filename="split.py" data-target="append">
data_complete = data.dropna()
</pre>

<pre class="file" data-filename="split.py" data-target="append">
data_incomplete = data[data.isna().any(axis=1)]
</pre>

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

Wir in der Konsole zu sehen, wurden die unvollständigen Daten von den vollständigen getrennt, und können separat weiterverarbeitet werden, beispielsweise durch Weitergabe an die Fachabteilung.