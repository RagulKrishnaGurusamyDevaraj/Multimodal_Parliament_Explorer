## Nutzung
Es gibt eine Voraussetzung, es muss Xelatex installiert sein, bzw. Tex Live Installation, um die Exports durchführen zu können.
Im Prinzip sehr einfach, die Driver Klasse ist unser Einstieg ins Programm, zunächst muss allerdings der Scheduler
ausgeführt werden, dieser sucht alle 7 Tage nach neuen Daten, liest diese ein, analysiert sie mit NLP Methoden und speichert alles in der 
DB.
Einfach zur Driver-Klasse navigieren und die main Methode ausführen, dann läuft alles.
Die POM beinhaltet alle Abhängigkeiten, daher sollte das Programm reibungslos laufen.
Es ist vorgekommen, dass das Programm teilweise sehr lange dauert und es nach dem download der DTD
Dateien etwas ins Stocken gerät, dann ist es sinnvoller das Programm kurz zu schließen und neu zu starten,
als abzuwarten.
Bei den Websites kann durchaus ein wenig Geduld angebracht sein, da manche Komponenten etwas mehr Zeit in Anspruch nehmen, bis 
sie vollständig geladen sind.
Die Exports finden sich ganz am Ende einer Abgeordnetenseite und werden unter resources/TeXandPdf gespeichert.


## Zeitlicher Aufwand
Zeitlich braucht das Programm ca. 50 min. Da der Videodownload aufgrund der Größe der
Dateien und der Menge, ebenso wie der Debattendownload und Parsing aufgrund der Menge einiges 
an Zeit verbraucht.


## Ablauf
Das Programm lädt zuerst alle Debatten runter und speichert sie im Ordner resources/speeches.
Dabei wird auch der scheduler gestartet der noch nicht runtergeladene Reden einliest.
Im Anschluss werden diese Reden mit der NLP Klasse verarbeitet und ebenfalls in die Datenbank
eingelesen sowie Serialisiert.
Später werden alle Videos heruntergeladen sowie mit NLP Methoden verarbeitet und gespeichert.
Ist all das abgeschlossen wird der REST Service gestartet und die Website lokal verfügbar gemacht.


## Anmerkungen

### NLP-Verarbeitung
Da die NLP-Verarbeitung der Reden viel Zeit in Anspruch nimmt, haben wir sie auskommentiert, die Ergebnisse
sind aber alle in der Datenbank gespeichert, ohne diese Maßnahme würde es mehrere Stunden dauern.
Gleiches gilt für die Serialisierung der NLP-Resultate, da es über 20.000 Reden sind, würde es das Projekt 
sprengen und für alle Beteiligten schwieriger machen. Daher ist der Ordner PPR_Processed_Speeches, über den 
die schon fertig analysierten Reden eingelesen werden, leer. Genauso wie der Ordner serialized_CAS_files leer ist,
in dem die serialisierten Reden gespeichert werden. Der Grund weshalb die videos nicht verarbeitet werden, 
ist das die PPR Server nicht erreichbar waren in dem Augenblick als die Analyse für sie gemacht werden sollte, aber 
die Methoden funktionieren, während dem Testen hat es genau wie intendiert funktioniert.

### Tex Live Installation
Auf Debian/Ubuntu: sudo apt install texlive-full 
Stellen Sie sicher, dass xelatex im PATH Betriebssystems verfügbar ist. 

Bei Linux oder macOS muss ggf. Ausführungsrechte für den PDF-Compiler setzen: 
chmod +x /usr/bin/xelatex