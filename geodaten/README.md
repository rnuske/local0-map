
## Deutschland

Download von [NaturalEarth](https://www.naturalearthdata.com) Version 5.0.0 Datensätzen
  * `ne_10m_admin_0_countries_deu.shp`
  * `ne_10m_admin_1_states_provinces_lines.shp`


Deutschland betreffende Teile der Datensätze in das deutsche Standard-Koordinatenbezugssystem UTM-32 (EPSG: 25832) umprojeziert

```
ogr2ogr -where "iso_a2 = 'DE'" -s_srs EPSG:4326 -t_srs EPSG:25832 deutschland.shp ne_10m_admin_0_countries_deu.shp

ogr2ogr -where "ADM0_A3 = 'DEU'" -s_srs EPSG:4326 -t_srs EPSG:25832 bundeslandgrenzen.shp ne_10m_admin_1_states_provinces_lines.shp
```

Die resultierenden Shapefiles `deutschland.shp` und `bundeslandgrenzen.shp` können in QGIS eingelesen werden.


## Standorte

Als CSV-Datei z.B. `LocalZeroTeamExport.csv` bekommen.
Entscheidend sind die Spalten `North` und `South` mit den Koordinaten der Standort in Dezimalgrad mit Dezimalpunkt im Koodinatenbezugssystem WGS84 (EPSG: 4326) und die Spalte `Phase`.
In QGIS als `Delimited Text File` (deutsch: `getrennte Texte`) eingelesen.
Unter Geometriedefinition als Geometrie-KBS WGS84 einstellen.
