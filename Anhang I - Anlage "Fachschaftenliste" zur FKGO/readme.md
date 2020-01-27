# Anmerkungen zur Fachschaftenliste
Die Liste der Fachschaften mit zugeordneten Studiengängen muss zu Beginn jedes Semesters durch das Fachschaftenreferat aktualisiert werden. Sie wird danach auf der Fachschaftenkonferenz beschlossen und dem Studierendenparlament zur Bestätigung vorgelegt. [§ 22 SdS](https://www.sp.uni-bonn.de/dokumente/idx/Satzungen/SdS.html#%C2%A722)

## Fachschaftenliste aktualisieren - How to
Um das Aktualisieren der Fachschaftenliste einfacher zu machen, wurde von @hszemi ein Werkzeug erstellt, welches die Studierendenstatistik der Universität mit der Fachschaftenliste abgleicht und die Änderungen ausspuckt.

### Benötigte Daten
Um das Werkzeug zu verwenden, müssen zunächst die Rohdaten vorbeireitet werden. Das sind:

- Studierendenstatistik - Personen - aktuelles Semester
- Studierendenstatistik - Fälle - aktuelles Semester
- Liste der Fachschaften der RFWU Bonn mit zugeordneten FAKs (Markdown)

Die Studierendenstatistik ist im Universitäts-Intranet erhältlich: 
[Link](https://www.intranet.uni-bonn.de/organisation/verwaltung/dez-9/abt-9.3/studierendenstatistik)

Dort auf "Gastzugang" klicken und bei "Studierende" unter "Dateien zum Download" die aktuellen Excel-Tabellen für Personen und Fälle herunterladen. 

Die Liste der Fachschaften der RFWU Bonn mit zugeordneten FAKs im Markdown-Format kann im fstool 
heruntergeladen werden: [Link](https://gaia.asta.uni-bonn.de/fstool/fachschaften-md.php?fullnames)

### Daten vorbereiten

Die Excel-Dateien der Studierendenstatistik müssen in csv-Dateien umgewandelt werden. Dafür die Datei öffnen, 
das zweite Tabellenblatt (Quelldaten) öffnen und als csv-Datei speichern (Komma als Feldtrenner, Anführungszeichen 
als Texttrenner)

### Skriptmagie

Das Skript `analyze.py` im Ordner `fakupdate` wird mit den beiden csv-Dateien sowie der aktuellen 
Fachschaftenliste im Markdown-Format als Parameter aufgerufen. Am Rechner des Fachschaftenreferats wird dazu zunächst die Konsole geöffnet und mit dem folgenden Befehl der relevante Ordner angesteuert:

```
cd Dokumente/fakupdate/fktools/fakupdate
```
Anschließend wird mit dem folgenden Befehl das Skript gestartet. Vorraussetzung ist, dass sich die nötigen Dateien im selben Ordner wie das Skript befinden.

```
./analyze.py faelle.csv personen.csv fachschaftenliste.md
```

Es erzeugt daraufhin 5 neue Dateien im selben Ordner:

- `FAKDIFF.txt`, enthält alle zu entfernenden und hinzuzufügenden FAKs mit den Kommentaren "NEW" und "REMOVED"
- `FAKLISTE.txt`, enthält alle existierenden FAKs aus den csv-Dateien
- `FAKNEW.txt`, enthält alle neuen FAKs aus den csv-Dateien
- `FAKREMOVED.txt` enthält alle zu entfernenden FAKs aus den csv-Dateien
- `FS-Removed.md` enthält für jede betroffene Fachschaft die zu entfernenden FAKs

Neu hinzugekommene FAKs müssen manuell zugeordnet werden. Anhaltspunkt hierfür kann die zugehörige Fakultät 
sein, diese kann in den Excel-Dateien nachgeschlagen werden. Zu entfernende FAKs sollten nur entfernt werden, 
wenn wirklich sicher ist, dass sie nicht mehr benötigt werden.

