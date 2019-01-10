---
title: "Statistische Modellbildung"
author: "Walter Gruber"
date: "2019-01-10"
description: "Einführung in die statistische Modellbildung"
cover-image: "Images/Cover.PNG"
github-repo: wgruber/Modellbildung
site: bookdown::bookdown_site
output:
  bookdown::gitbook:
bibliography: "bibliography.bib"
biblio-style: "apalike"
link-citations: true
---

# Vorbemerkung {-}

Dieses Skriptum wurde mit dem Paket *bookdown* erstellt. Der verwendete R-Code wird als Teil des Skriptums angeführt und kann auch direkt von diesem Dokument in ein R-Skript übernommen und ausgeführt werden. Erläuterungen zum Code beschränken sich zum Teil auf wesentliche Code-Fragmente. Für detaillierte Angaben zu diversen Funktionen ist die R-Hilfe zu verwenden.


Der nachfolgende Code ist spezifisch für die Erstellung dieses Dokumentes, sowie der Bearbeitung der Beispiele im Kurs von Bedeutung. Es wird in diesem Code-Teil sichergestellt, dass die verwendeten Pakte vorhanden und geladen sind, die Anzahl der Nachkommastellen bei der Ausgabe definiert, sowie die Verzeichnisse in denen sich die Daten, die R-Skripten und im Skriptum verwendete Abbildungen befinden. Daher sollte dieser Code am Anfang jeder neuen R-Datei übernommen werden. Die Vorgehensweise ist:

1. Starten von R-Studio
2. Öffnen einer neuen R-Script Datei
3. Kopiere die nachfolgenden Zeilen in diese Datei
4. Speichere die Datei mit einem entsprechenden Namen
5. Führe diesen Code aus
6. Füge deinen Code nach diesen Zeilen ein


```r
# Initialisierung
rm(list = ls())
if (!require("pacman")) install.packages("pacman")
pacman::p_load(corrplot, DAAG, dataMaid, devtools, doBy, DT, 
               ggformula, ggplot2, gridExtra, htmlwidgets, 
               imager, knitr, labelled, leaps, magick, MASS, 
               NHANES, mosaic, mosaicCore, mosaicData, pander,
               pastecs, ppcor, reshape2, 
               rockchalk, rpart, rpart.plot)
```


Inhalte, Beispiele und Daten stammen teilweise aus dem Internet, u.a. [@CourseRa], [@DataCamp] und dem Buch [@Field].

# Einleitung {-}

Donald Knuth, einer der Pioniere und bedeutensten Persönlichkeiten in der Entwicklung von Programmiersprachen vertrat in seinem Buch Compter *Programming as an art* [@Knuth] die Auffassung, dass rein wissenschaftliches Arbeiten durch einen Computer erlernt werden kann (*Science is knowledge which we understand so well that we can teach it to a computer*). Alle andere Formen der Datenanalyse bezeichnete er als Kunst.

Neben statistischen Methoden, maschinellem Lernen, diversen Softwarepaketen und verschiedensten Werkzeugen stehen heutzutage auch entsprechend leistungsfähige Computer zur Verfügung, um Unmengen von Daten aufzuzeichnen und zu verarbeiten. Die *Kunst*, Wirklichkeit in bestmöglicher Form durch ein Modell abzubilden, besteht demnach darin, die:

* richtigen Fragen zu stellen.
* Daten zu sammeln, mit welchen diese Fragen beantwortet werden können.
* entsprechenden Methoden und Werkzeuge anzuwenden.
* Ergebnisse richtig zu interpretieren.
* Ergebnisse zu vermitteln.

In den meisten Fällen ist es nicht möglich, die Wirklichkeit absolut getreu durch Daten abzubilden. Seit Urzeiten verwendet daher der Mensch Modelle, um zumindest mit einer Annäherung diese möglichst genau darzustellen und daraus Rückschlüsse für sonst nicht oder schwer zu erklärende Phänome zu ziehen. In einem Artilel beschreibt G. Box [@Box] sehr treffend die Eigenschaften von Modellen:

>Now it would be very remarkable if any system existing in the real world could be exactly represented by any simple model. However, cunningly chosen parsimonious models often do provide remarkably useful approximations. For example, the law P⋅V=R⋅T relating pressure P, volume V and temperature T of an “ideal” gas via a constant R is not exactly true for any real gas, but it frequently provides a useful approximation and furthermore its structure is informative since it springs from a physical view of the behavior of gas molecules. For such a model there is no need to ask the question “Is the model true?”. If “truth” is to be the “whole truth” the answer must be “No”. The only question of interest is “Is the model illuminating and useful?”.
> --- G. Box

# Allgemeine Definition des Begriffs *Modell* {-}

Allgemein versteht man unter [Modellbau](https://de.wikipedia.org/wiki/Modellbau) die Herstellung eines konkreten, dreidimensionalen, physischen Objektes. Der Prozess der [Modellbildung](https://de.wikipedia.org/wiki/Modell#Modellbildung) abstrahiert dabei mit dem Erstellen eines Modells von der Realität, weil diese meist zu komplex ist, um sie vollständig abzubilden. 

Diese Vollständigkeit wird aber auch gar nicht beabsichtigt, vielmehr sollen lediglich die wesentlichen Einflussfaktoren identifiziert und dargestellt werden, die für den realen Prozess und im Modellkontext bedeutsam sind.

Der Begriff Modell entstand im Italien der Renaissance (italienisch *modello*), hervorgegangen aus lateinischesn *modulus*, einem Maßstab in der Architektur. Es wurde bis ins 18. Jahrhundert vorwiegend in der bildenden Kunst als Fachbegriff verwendet.

In der Umgangssprache wird das Wort *Modell* für unterschiedliche Sachverhalte verwendet. Im naturwissenschaftlichen Erkenntnisprozess haben Modelle verschiedene Bedeutungen und Funktionen. Merkmale und Charakteristika, an denen ein Modell eindeutig als Modell definiert werden kann, existieren nicht [@Upmeier-Krueger-2010]. Die Bedeutung ist zudem vom Kontext abhängig. Beim *Modellsein* werden folgende Aspekte unterschieden [@Mahr-Bernd-2008]:

* *Modell für etwas sein*
* *Modell von etwas sein*

Dies muss auch bei der Beurteilung eines Modells, also der Frage, ob ein Modell ein gutes Modell ist, berücksichtigen werden. Hier ist die Frage des Zwecks des Modells entscheidend. Mahr benennt drei allgemeine Kriterien zur Beurteilung von Modellen: 

1. Das Modell muss die Funktion erfüllen, 
2. durch seine Anwendung etwas von dem, wovon es ein Modell ist, zudem wofür es ein Modell ist, transportieren.
3. Das Modell muss ein Garant von Konsistenz sein. 

D.h., dass das Modell garantieren muss, dass es keine Widersprüche enthält, so dass seine Anwendung nicht notwendig zu Widersprüchen führen muss. Das Modell muss über eine ausreichende pragmatische Eignung verfügen und demnach das, wofür oder wovon es ein Modell ist, ausreichend und angemessen repräsentieren.

Die Hauptfunktion in den Naturwissenschaften ist die Untersuchung und Interpretation von Phänomenen. Ziel ist die Reduzierung von Komplexität und somit die Erzeugung eines fokussierten Bildes des zu untersuchenden Objekts. Man kann sagen, dass Modelle den Blick auf das Wesentliche eines Phänomens oder Gegenstandes lenken sollen. Das Modell ist somit ein Repräsentant des Originals. Modell und Original können sich aber im Material, der Dimensionierung und der Abstraktion unterscheiden. Sie können gegenständlich, bildhaft, schematisch oder formelhaft sein.

