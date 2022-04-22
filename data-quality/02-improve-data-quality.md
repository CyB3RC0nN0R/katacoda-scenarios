Grundsätzlich gibt es zwei verschiedene Ansätze, die Datenqualität zu gewährleisten.
Einerseits ist eine direkte Korrektur von Qualitätsmängeln an der Quelle möglich.
Dabei müssen die Korrekturmaßnahmen in allen Quellsystemen implementiert werden, was oftmals sehr aufwändig und nicht umsetzbar ist.
Dadurch wird die zweite Möglichkeit, die Korrektur erst im Data Warehouse vorzunehmen, häufig bevorzugt.
Diese kann während eines Extract-Transform-Load (ETL)-Prozesses geschehen, oder manuell nach Ablauf eines ETL-Prozesses [3].

Die folgende Tabelle demonstriert einige gängige Transformationen, die zur Qualitätssicherung vorgenommen werden.

|Problem|Lösung|
|-|-|
|Falsche Werte wie 32.12.2020|Korrekter Datentyp|
|Fehlende Werte|NOT NULL Constraint|
|Verletzte Referenzen|FOREIGN KEY Constraint|
|Duplikate|PRIMARY oder UNIQUE KEY Constraint|
|Inkonsistente Daten|ACID-Transaktionen, Geschäftslogik, zusätzliche Prüfungen|