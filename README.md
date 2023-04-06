# Locale Zero Karte

## Vorbereitungen

  * QGIS (aktuelle oder LTR Version) herunterladen und installieren
  * Das local0-map Repository clonen bzw. herunterladen und entpacken
  * Das Projekt `qgis_projekt_definition.qgz` mit Doppelklick öffnen oder aus QGIS heraus öffnen.
  * ggf. den Pfad zu den `icons` einstellen unter `Einstellungen > Optionen > System > SVG-Pfade`. Immer dann wenn die Icons nicht in der Karte erscheinen und stattdessen ? dargestellt werden.



## Datenquellen

Die Daten liegen schon im Ordner `geodaten` bereit und müssen nur angefasst werden, wenn sich etwas ändert.

Wenn eine neue Karte mit anderen Standorten erstellt werden soll, müssen die Standorte entweder ergänzt/überarbeitet oder die Datei ausgetauscht werden. Am einfachsten ist es wenn alles (Dateiname, Spaltennamen, Spaltenreihenfolge und Datenformate) gleich bleibt. Wenn sich der Dateiname oder die Spalten ändern (Benennung, Datenformat o.Ä.), muss der Standort-Datensatz neu in QGIS eingelesen werden. 


### Deutschland

Download von [NaturalEarth](https://www.naturalearthdata.com) Version 5.0.0 Datensätzen
  * `ne_10m_admin_0_countries_deu.shp`
  * `ne_10m_admin_1_states_provinces_lines.shp`


Deutschland betreffende Teile der Datensätze in das deutsche Standard-Koordinatenbezugssystem UTM-32 (EPSG: 25832) umprojeziert

```
ogr2ogr -where "iso_a2 = 'DE'" -s_srs EPSG:4326 -t_srs EPSG:25832 deutschland.shp ne_10m_admin_0_countries_deu.shp

ogr2ogr -where "ADM0_A3 = 'DEU'" -s_srs EPSG:4326 -t_srs EPSG:25832 bundeslandgrenzen.shp ne_10m_admin_1_states_provinces_lines.shp
```

Die resultierenden Shapefiles `deutschland.shp` und `bundeslandgrenzen.shp` können in QGIS eingelesen werden.


### Standorte

Als CSV-Datei z.B. `LocalZeroTeamExport.csv` bekommen.
Entscheidend sind die Spalten `North` und `South` mit den Koordinaten der Standort in Dezimalgrad mit Dezimalpunkt im Koodinatenbezugssystem WGS84 (EPSG: 4326) und die Spalte `Phase`.
In QGIS als `Delimited Text File` (deutsch: `getrennte Texte`) eingelesen.
Unter Geometriedefinition als Geometrie-KBS WGS84 einstellen.



## Icons
Die verwendeten (und leicht angewandelte) Icons liegen im Ordner `icons`.

Die Basis der Icons stammt von Jean-Marc Viglino aus der Sammlung [Font-GIS](https://viglino.github.io/font-gis/) Version 1.0.4. Robert Nuske hat Farben und Schatten an den germanZero Style angepasst.

Qgis muss mitgeteilt werden wo die SVG Icons liegen dafür teilt man unter `Einstellungen > Optionen > System > SVG-Pfade` den Pfad zu den SVG Dateien (`local0-map/icons`) mit.



## Styling

  * Die Vektordatensätze `deutschland` und `bundeslandgrenzen` laden. deutschland muss unten liegen.
  * `deutschland` wir mit dem Stil `invertierte Polygone` u der Farbe goldgelb (`#ffc80c`) dargestellt, damit alles außerhalb goldgelb und Deutschland weiß bleibt
  * `bundeslandgrenzen` bekommt ebenfalls die Farbe (`#ffc80c`) und eine passende Linienstärke 

  * die Standorte (hier: `LocalZeroTeamExport`) bekommen Punktsymbole unter `Eigenschaften > Symbolisierung > Kategorisiert`
    * Wert: `Phase`
    * Symbol: `SVG Markierung`
    * in der Tabelle der Werte dann mit Doppelklick auf Symbol das passende Icon (hell o. dunkel) auswählen
    * Größe einstellen
    * Anchor point bottom



## Export
   
  * `Projekt > Layouts > local0-grafik-export` klicken
  * Im neuen Kartenlayoutfenster unter Layout als Bild, SVG oder PDF exportieren. QGIS meckert immer, dass der SVG Layout kaputt sein könnte. Für diesen Datensatz funktioniert es aber problemlos.
