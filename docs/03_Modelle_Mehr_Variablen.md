

# (PART\*) Teil III: Modelle mit mehr Variablen {-}



# Korrelationen {-}

Korrelation ist ein Maß für den statistischen Zusammenhang zwischen zwei Datensätzen. Unabhängige Variablen sind daher stets unkorreliert. Korrelation impliziert daher auch stochastische Abhängigkeit. Bei der Berechnung einer Korrelation wird die lineare Abhängigkeit zwischen zwei Variablen quantifiziert.

Korrelationen werden i.A. der *deskriptiven Statistik* zugeordnet. Durch eine Reihe von Verfahren, wie z.B. partielle Korrelation, multiple Korrelation oder Faktorenanalyse, kann die einfache Korrelation zweier Variablen auf Beziehungen zwischen zwei Variablen unter Berücksichtigung des Einflusses weiterer Variablen werden. Korrelationen sind ein unverzichtbares Werkzeug für viele Forschungsgebiete.

## Kausalität {-}

Eine relevante (statistisch signifikante) Korrelation liefert keinen Beleg für die Kausalität. Vor allem in der Medizin und Psychologie suchen Forscher nach Kriterien für Kausalität. Es existieren mehrere Ansätze zur Erklärung der Ursächlichkeit einer Korrelation (siehe z.B. die 9  [Bradford-Hill-Kriterien](https://de.wikipedia.org/wiki/%C3%84tiologie_(Medizin)){target="_blank"}).

<!-- 1. *Stärke der Assoziation (Effektstärke)*: Eine geringe Effektsstärke bedeutet nicht, dass keine Beziehung zwischen den Variablen existiert, aber bei einer größeren Effektstärke ist eine kausale Beziehung wahrscheinlicher. -->
<!-- 2. *Konsistenz (Reproduzierbarkeit)*: Übereinstimmende Befunde, festgestellt durch verschiedene Personen an verschiedenen Orten mit verschiedenen Stichproben, verstärkt die Wahrscheinlichkeit eines Effekts. -->
<!-- 3. *Spezifität*: Kausalität ist wahrscheinlich, wenn es keine andere, bessere Erklärung für das Auftreten des Ereignisses gibt. Je spezifischer die Beziehung zwischen einem Faktor und einem Effekt ist, desto höher die Wahrscheinlichkeit eines kausalen Zusammenhangs. -->
<!-- 4. *Zeitbedingtheit*: Die Ursache muss der Wirkung vorausgehen (wenn erwartet wird, dass es eine Verzögerung nach der Ursache und dem erwarteten Effekt gibt, dann muss der Effekt nach der Verzögerung eintreten). -->
<!-- 5. *Dosis-Wirkungs-Beziehung*: Größere Exposition sollte gewöhnlich auch zu einer größeren Auftretenshäufigkeit des Effekts führen. In einigen Fällen jedoch kann bereits die bloße Anwesenheit eines Faktors einen Effekt auslösen. In anderen Fällen wird der umgekehrte Fall beobachtet: die Anwesenheit eines Faktors reduziert die Auftretenshäufigkeit. -->
<!-- 6. *(Biologische) Plausibilität*: Ein plausibler Mechanismus zwischen Ursache und Wirkung ist hilfreich (allerdings fügte Hill auch hinzu, dass das Verständnis von Ursache und Wirkung durch unseren aktuellen Wissensstand begrenzt sein kann). -->
<!-- 7. *Koheränz*: Die Stimmigkeit zwischen epidemiologischen- und Laborbefunden erhöht die Wahrscheinlichkeit eines Effekts. Hill fügte allerdings hinzu, dass das Fehlen eines Laborbefundes nicht einen epidemiologischen Effekt auf die Beziehung ungültig machen kann. -->
<!-- 8. *Experiment*: Es ist wahrscheinlicher, dass eine Beziehung kausal ist, wenn sie experimentell verifiziert werden kann. -->
<!-- 9. *Analogie*: Der Effekt ähnlicher Faktoren darf berücksichtigt werden. -->

## Linearität {-}

Ein Korrelationskoeffizient zeigt die Stärke eines *linearen Zusammenhangs* zwischen zwei Variablen. Aber der Wert von $r$ charakterisiert nicht die genaue Art des Zusammenhangs oder das Aussehen des Punktdiagramms beider Variablen[^6].

[^6]: [Abbildungen aus Matheguru](https://matheguru.com/stochastik/korrelation-korrelationskoeffizient.html){target="_blank"}

<center>

![**Abbildung 1**: Korrelation und Linearität](Images/03_LinearitaetKorrelation.JPG){ width=80% }

</center>

## Korrelationskoeffizienten {-}

Neben dem Pearson-Produkt-Moment-Korrelationskoeffizienten $r$ existieren noch etliche weitere Korrelationskoeffizienten und Zusammenhangsmaße. Die meisten hiervon sind Sonderfälle der Pearson-Produkt-Moment-Korrelation. Nachfolgende Tabelle zeigt, wann welcher Koeffizient berechnet werden soll. Die Verwendung unterschiedlicher Korrelationsberechnungen ist i.A. abhängig vom Skalenniveau der beteiligten Variablen.

<center>

![**Abbildung 2**: verschiedene Korrelationskoeffizienten](Images/Korrelationskoeffizienten.JPG){ width=100% }

</center>

Weiter Infos zu den einzelnen Korrelationskoeffizienten sind der Literatur zu entnehmen. Eine übersichtliche Darstellung findet man auch auf der Website von [MatheGuru](https://matheguru.com/stochastik/korrelation-korrelationskoeffizient.html){target="_blank"}.

## Herleitung {-}

Bereits bei der deskriptiven Statistik haben wir mit dem Maß der Varianz ($s^2$) einen Kennwert definiert, der die Schwankungen bezüglich des entsprechenden Mittelwertes beschreibt. Per Definition ist die Varianz die durchschnittliche Summe der quadrierten Abweichungen zum Mittelwert, also:

\begin{equation} 
  s^2 = \frac{\sum_{i=1}^{N} (x_i - \bar{x})^2}{N-1}
  (\#eq:Var)
\end{equation} 

Betrachtet man zwei (normalverteilte) intervallskalierte Variablen $x$ und $y$, dann lässt sich diese Idee auch als ein Kennwert der gemeinsamen Variablität der beiden Variablen definieren:

\begin{equation} 
  cov(x,y) = \frac{\sum_{i=1}^{N} (x_i - \bar{x}) \cdot (y_i - \bar{y})}{N-1}
  (\#eq:Cov)
\end{equation} 

Dieser Kennwert nennt sich *Kovarianz* ($cov$). Da dieser Kennwert an die entsprechenden Einheiten der Variablen gebunden ist, normiert man i.A. dieses Maß durch das Produkt der jeweiligen Standardabweichung $s_x$ und $s_y$. Dieses normierte Maß bezeichnet man als *Korrelationskoeffizient* ($r$):

\begin{equation} 
  r(x,y) = \frac{cov(x,y)}{s_x \cdot s_y}
  (\#eq:Korr)
\end{equation}

### Beispiel {-}

Anhand des bereits verwendeten Datensatzes (*CPS85*) wollen wir die Beziehung der Variablen Gehalt (*wage*), Ausbildung (*educ*) und Berufserfahrung (*exper*) berechnen und graphisch darstellen. Kopiere den folgenden Code ins RStudio und führe diesen dann aus. Diskutiere die Ergebnisse.


```r
  M      <- data.frame(wage = CPS85$wage, educ = CPS85$educ, exper = CPS85$exper)
  Korr_1 <- cor(M)
  pander(Korr_1, style = "rmarkdown")
  # DT::datatable(round(Korr_1,2))
  corrplot(cor(M), method = "ellipse")
```

# Einfache Regression {-}

Will man bei der Korrelationsanalyse den Zusammenhang von Variablen beschreiben, versucht man in der Regressionsanalyse eine Variable mittels einer linearen Funktion durch eine (oder mehrere) andere Variablen zur *erklären*. Nichts desto trotz sind Korrelation und Regression sehr eng miteinander verknüpft.

Der Begriff Regression tauchte erstmalig 1877 in einer von Sir Francis Galton abgefassten wissenschaftlichen Studie auf. In einer späteren Studie über die Körpergröße von Vätern und deren Söhnen wendete er den Gedanken der Regressionsanalyse erneut an. 

Er fand heraus, dass Söhne sehr großer (kleiner) Väter zwar groß (klein), aber etwas kleiner (größer) sind als diese. Die Körpergröße entwickelt sich somit immer wieder in Richtung des Durchschnitts zurück. Als Engländer bezeichnete Galton diesen Prozess als *Regression*[^7].

[^7]: was mit *Rückschritt*, *Rückkehr* oder *rückläufige Entwicklung* übersetzt werden kann (siehe [Deskriptive Statistik und moderne Datenanalyse](https://link.springer.com/chapter/10.1007/978-3-8349-7071-8_5)).

Zwischen der Körpergröße der Söhne und der Väter besteht somit ein Zusammenhang, dessen Stärke mit Hilfe der Korrelation ausgedrückt werden könnte. Im Unterschied zur Korrelationsanalyse unterstellt man bei der Regressionsanalyse jedoch sehr oft auch die kausale Richtung des Zusammenhangs: 

>Die Körpergröße der Söhne ist abhängig von der Körpergröße des Vaters und nicht umgekehrt.

Entsprechend bezeichnete Galton:

* die Größe der Söhne als *abhängige Variable* (*dependent variable*, **DV**) und 
* die Größe der Väter als *unabhängige Variable* (*independent variable*, **IV**).

Häufig werden die Variable die vorhergesagt werden soll bei der Regression *Kriterium* ($y_i$)und die Variable(n) die für die Vorhersage eingesetzt wird/werden *Prädiktor(n)* ($x_{1i}$)[^8] genannt. Anhand des Prädiktors wird demzufolge das Kriterium vorhergesagt.

[^8]: wobei die 1 für den ersten (einzigen) Prädiktor und $i$ als Index für die $i$-te Beobachtung steht.

Der Schluss, dass die Regression die Kausalität von Zusammenhängen *beweist*, ist damit allerdings nicht (immer) erlaubt. Die Kausalität (Wirkungsrichtung) muss zuvor theoretisch abgeleitet werden, bevor sie empirisch (mit Hilfe der Regression) bewiesen werden kann. So ist die Richtung der Kausalität bei Fragen wie:

* ist es das Alter des Bräutigams, welches das Alter der Braut bestimmt, oder umgekehrt?
* beeinflusst sich das Alter der verheirateten Paare gar gegenseitig? 

nicht zu bestimmen. Manchmal ist die Kausalität jedoch sehr offensichtlich: 

* der Blutdruck hat keinen Einfluss auf das Alter, sondern das Alter hat einen Einfluss auf den Blutdruck. 
* die Körpergröße hat einen Einfluss auf das Körpergewicht, aber umgekehrt lässt sich dieser Zusammenhang wohl theoretisch kaum herleiten.
* mit Zunahme des $CO_2$ Gehaltes in der Atmosphäre steigt die durchschnittliche Temperatur, eine umgekehrte Wirkungsrichtung ist aber auszuschließen (da hätten wir in südlichen Ländern ein kleines Problem!).

Die Regression ermöglicht jedenfalls unter bestimmten Umständen[^9] gute, bzw. bestmögliche Vorhersage für eine Variable. Folgernd aus dem eben gesagten, sollte nochmals klargestellt werden, dass im Gegensatz zur Korrelation festgelegt werden muss, welche Variable durch eine andere Variable vorhergesagt werden soll. 

[^9]: intervallskaliertes Kriterium, linearer Zusammenhang zw. Kriterium und Prädiktor(en), Zufallsstichprobe, Normalverteilung der Fehler, Homoskedastizität, Unabhängigkeit der Fehler. Details dazu später.

## Definitionen {-}

Die formale Definition eines einfachen linearen Modells ist:

\begin{equation} 
  y_i = b_0 + b_1 \cdot x_{1i} + \varepsilon_i
  (\#eq:LinModFehler)
\end{equation}

Die wesentlichen Parameter dieses einfachen Modells sind:

1. Konstanter Term (intercept) $b_0$: jener Wert den $y_i$ einnimmt, wenn $x_{1i} = 0$ ist.
2. Steigung (slope) $b_1$: die Zunahme von $y_i$, wenn $x_{1i}$ sich um eine Einheit erhöht.

Des Weiteren berücksichtigt dieses Modell auch einen Fehler ($\varepsilon_i$). Damit kommt auch ein ganz zentraler Teil bei der Modellbildung zum Ausdruck. Die meisten Modelle definieren sich also aus:

\begin{equation} 
  \textrm{wahrer Wert} = \textrm{Modell} + \textrm{Fehler}
  (\#eq:AllgModellvorstellung)
\end{equation}

Daraus lässt sich auch folgende Erkenntnis bezüglich des Modells direkt ableiten:

1. Je kleiner die Summe der Fehler sind, desto besser ist das Modell.
2. Je genauer das Modell, desto kleiner wird auch der Fehler sein.

Mit dieser Erkenntnis wird auch klar, dass i.A. ein ganz einfaches Modell (mit einem einzigen Prädiktor) nur zu einer bedingten Reduktion des Fehlers geeignet ist. Wir werden uns im weiteren Verlauf mit erweiterten Modellen beschäftigen, wollen aber zunächst die Eigenschaften des einfachen linearen Modells näher betrachten. Im folgenden Link findet man eine gute [Veranschaulichung des einfachen linearen Modells](https://phet.colorado.edu/sims/html/least-squares-regression/latest/least-squares-regression_en.html){target="_blank"}.

Betrachtet man das Modell isoliert (also ohne Fehlerterm), ist folgende Schreibweise üblich:

\begin{equation} 
  \hat{y}_i = b_0 + b_1 \cdot x_{1i}
  (\#eq:LinMod)
\end{equation}

### Berechnung der Koeffizienten {-}

Für die Berechnung der Koeffizienten wird das Kriterium der kleinste Quadrate (MLS) angewandet. Einfach ausgedrückt wird eine Gerade durch die beobachteten Daten gesucht, die folgenden Eigenschaften aufweist:

1. die Summe der quadratischen Abstände jeder Beobachtung zum entsprechenden Punkt auf der Geraden ist ein Minimum, also $\sum_{i=1}^{N} \varepsilon_i^2 = min$.
2. es gibt keine andere Gerade die eine kleinere Summe dieser Fehler liefert.

Die Berechnung der Parameter entspricht daher einer Extremwertaufgabe, d.h. die partiellen Ableitungen werden auf Null gesetzt. Daraus lassen sich dann die Parameter $b_0, b_1$ berechnent. Details dazu siehe [Wikipedia](https://de.wikipedia.org/wiki/Einfache_lineare_Regression){target="_blank"}.

## Modellanwendung {-}

Zur Anwendung eines einfachen linearen Modell betrachten wir wiederum die bereits bekannten Daten aus dem Datensatz *CPS85*. Diese Mal wollen wir das Gehalt (*wage*) durch die Ausbildungsdauer (*educ* in Jahren) vorhersagen. Formal lautet das Modell demnach:

\begin{equation} 
   \hat{\textrm{wage}} = b_0 + b_1 \cdot \textrm{educ}
  (\#eq:LinModBsp1)
\end{equation}

Die Werte der Parameter $b_0, b_1$ können für dieses Beispiel entsprechend der obigen Erläuterung folgendermaßen interpretiert werden:

1. Für eine Person mit keiner Ausbildung ($\textrm{wage} = x_{1i} = 0$) wird durch das Modell ein Einkommen $y_i = b_0$ vorhergesagt.
2. Erhöht man die Ausbildungsdauer $x_{1i}$ um ein Jahr, steigt der Gehalt $y_i$ um das $b_1$-fache an.

Kopiere zur Veranschaulichung folgenden Code in dein R-Script und führe diesen aus.


```r
  DF <- CPS85
  ggplot(CPS85, aes(x = educ, y = wage)) +
    geom_point() +
    geom_smooth(method=lm, se=FALSE) +
    theme_bw()
```

![](03_Modelle_Mehr_Variablen_files/figure-latex/Modell1-1.pdf)<!-- --> 

```r
  model_1     <- lm(wage ~ educ, data = CPS85)
  pander(summary(model_1))
```


---------------------------------------------------------------
     &nbsp;        Estimate   Std. Error   t value   Pr(>|t|)  
----------------- ---------- ------------ --------- -----------
 **(Intercept)**    -0.746      1.045      -0.7135    0.4758   

    **educ**        0.7505     0.07873      9.532    5.474e-20 
---------------------------------------------------------------


--------------------------------------------------------------
 Observations   Residual Std. Error   $R^2$    Adjusted $R^2$ 
-------------- --------------------- -------- ----------------
     534               4.754          0.1459       0.1443     
--------------------------------------------------------------

Table: Fitting linear model: wage ~ educ

Die in der Tabelle angegebenen Werte der Spalte **Estimate** entsprechen dabei den Parametern $b_0, b_1$ des Modells. Eine weitere wesentliche Kennzahl für die Interpretation des Modells ist der Spalte $R^2$ zu entnehmen. Dieser Wert wird als *Determinationskoeffizient*[^10] bezeichnet. Umgerechnet in \% (im vorliegenden Beispiel also 14.43\%) besagt der Wert, wie viel der Variablität des Gehaltes durch den Prädiktor Ausbilung erklärt wird. Wir werden im weiteren Verlauf noch öfter auf diesen Kennwert zurückkommen.

[^10]: häufig auch als Varianzaufklärung

Welche Gehälter würden für Ausbildungszeiten zwischen 10 und 14 Jahren vorhergesagt werden? Kopiere folgenden Code in dein R-Script und führe diesen aus. Änder auch den Wertebereich der Prädiktoren und beobachte was dabei passiert!



Im Vergleich zum Mittelwert-Modell zeigt sich mit steigender Ausbildung ein höheres Einkommen. Der Fehler bei der Vorhersage des Einkommens wird sich daher durch diese Modellvorstellung verringern (mehr zur Abschätzung der Fehlerreduktion später).

### Aufgabe SLR 1 {-}

Öffne ein neues R-Script und kopiere die bereits bekannte Kopfzeile in diese Datei. Speichere anschließend das Skript unter dem Namen *SLR_Aufgabe1.R*. Bearbeite nun folgende Aufgabenstellungen:

* Lade die Datei "*Album Sales 1.dat*"
* erstelle ein einfaches Streudiagramm mit Sales auf der x- und adverts auf der y-Achse.
* erstelle ein einfaches lineares Modell zur Vorhersage der Verkaufszahlen (*sales*) durch die Variable *adverts*.
* Wie stark korrelliert der Prädiktor mit dem Kriterium?
* Wie viel Varianz wird vom Kriterium durch den Prädiktor aufgeklärt?
* Ist das erstellte Modell signifikant besser, als dan Null-Modell?
* Welchen Wert würde das Modell für Werbeausgaben = 100 vorhersagen?

[Lösung Aufgabe SLR 1](#aufgabe-slr-1-lsg)

## Residualanalyse {-}

Ein zentrales Thema der Modellbildung ist die Beurteilung und (statistische) Auswertung der Abweichungen des Modells von den Beobachtungen (Fehler, Residum). Folgende Kennwerte bilden die Möglichkeit, die Güte des Modells abzuschätzen:

1. *Vorhergesagte Werte*: vorhergesagte Werte der Regressionsgleichung (= Werte die auf der Geraden liegen).
      * Nicht standardisiert: der Wert, den das Modell für die abhängige Variable vorhersagt.
      * Standardisiert: $z$-Transformierte vorhergesagte Werte.
      * Korrigiert: der vorhergesagte Wert für einen Fall, wenn dieser Fall von der Berechnung der Regressionskoeffizienten ausgeschlossen ist.
      * Standardfehler des Mittelwerts: Standardfehler der vorhergesagten Werte. Ein Schätzwert der Standardabweichung des Durchschnittswertes der abhängigen Variablen für die Fälle, die dieselben Werte für die unabhängigen Variablen haben.
2. *Residuen*: tatsächliche Wert der abhängigen Variablen minus des vorhergesagten Werts aus der Regressionsgleichung.
      * Nicht standardisiert: Die Differenz zwischen einem beobachteten Wert und dem durch das Modell vorhergesagten Wert.
      * Standardisiert: Der Quotient aus dem Residuum und einer Schätzung seiner Standardabweichung. Standardisierte Residuen, auch bekannt als Pearson-Residuen, haben einen Mittelwert von 0 und eine Standardabweichung von 1.
      * Studentisiert: Ein Residuum, das durch seine geschätzte Standardabweichung geteilt wird, die je nach der Distanz zwischen den Werten der unabhängigen Variablen des Falles und dem Mittelwert der unabhängigen Variablen von Fall zu Fall variiert.
      * Ausgeschlossen: Das Residuum für einen Fall, wenn dieser Fall nicht in die Berechnung der Regressionskoeffizienten eingegangen ist. Dies ist die Differenz zwischen dem Wert der abhängigen Variablen und dem korrigierten Schätzwert.
      * Studentisiert und ausgeschlossen: Der Quotient aus dem ausgeschlossenen Residuum eines Falles und seinem Standardfehler. Die Differenz zwischen einem studentisierten ausgeschlossenen Residuum und dem zugehörigen studentisierten Residuum gibt an, welchen Unterschied die Entfernung eines Falles für dessen eigene Vorhersage bewirkt.
3. *Distanzen*: Maße zum Auffinden von Fällen mit ungewöhnlichen Wertekombinationen bei den unabhängigen Variablen und von Fällen, die einen großen Einfluss auf das Modell haben könnten.
      * Mahalanobis: Dieses Maß gibt an, wie weit die Werte der unabhängigen Variablen eines Falls vom Mittelwert aller Fälle abweichen. Eine große Mahalanobis-Distanz charakterisiert einen Fall, der bei einer oder mehreren unabhängigen Variablen Extremwerte besitzt.
      * Cook: Ein Maß dafür, wie stark sich die Residuen aller Fälle ändern würden, wenn ein spezieller Fall von der Berechnung der Regressionskoeffizienten ausgeschlossen würde. Ein großer Wert der Cook-Distanz zeigt an, dass der Ausschluss eines Falles von der Berechnung der Regressionskoeffizienten die Koeffizienten substanziell verändert.
      * Hebelwerte: Werte, die den Einfluss eines Punktes auf die Anpassung der Regression messen. Der zentrierte Wert für die Hebelwirkung bewegt sich zwischen 0 (kein Einfluss auf die Anpassung) und $(N-1)/N$.
4. *Vorhersageintervalle*: obere und untere Grenzen sowohl für Mittelwert als auch für einzelne Vorhersageintervalle.
      * Mittelwert: Unter- und Obergrenze (zwei Variablen) für das Vorhersageintervall für den mittleren vorhergesagten Wert.
      * Individuell: Unter- und Obergrenzen (zwei Variablen) für das Vorhersageintervall der abhängigen Variablen für einen Einzelfall.
      * Konfidenzintervall: Geben Sie einen Wert zwischen 1 und 99,99 ein, um das Konfidenzniveau für die beiden Vorhersageintervalle festzulegen. Wählen Sie *Mittelwert* oder *Individuell* aus, bevor Sie diesen Wert eingeben. Typische Werte für Konfidenzniveaus sind 90, 95 und 99.
5. *Einflussstatistiken*: Änderung in den Regressionskoeffizienten (DfBeta(s)) und vorhergesagten Werten (DfFit), die sich aus dem Ausschluss eines bestimmten Falls ergeben. 
      * Differenz in Beta: entspricht der Änderung im Regressionskoeffizienten, die sich aus dem Ausschluss eines bestimmten Falls ergibt. Für jeden Term im Modell, einschließlich der Konstanten, wird ein Wert berechnet.
      * Standardisiertes DfBeta: die Änderung des Regressionskoeffizienten, die sich durch den Ausschluss eines bestimmten Falls ergibt. Es empfiehlt sich, Fälle mit absoluten Werten größer als $2/\sqrt{N}$ zu überprüfen, wenn $N$ die Anzahl der Fälle darstellt. Für jeden Term im Modell, einschließlich der Konstanten, wird ein Wert berechnet.
      * DfFit: Differenz im Anpassungswert ist die Änderung im vorhergesagten Wert, die sich aus dem Ausschluss eines bestimmten Falls ergibt.
      * Standardisiertes DfFit: Änderung des vorhergesagten Werts, die sich durch den Ausschluss eines bestimmten Falls ergibt. Es empfiehlt sich, Fälle mit absoluten Werten $> 2/\sqrt{p/N}$ zu überprüfen, wobei $p$ die Anzahl der unabhängigen Variablen im Modell und $N$ die Anzahl der Fälle darstellt.
      * Kovarianzverhältnis: Verhältnis der Determinante der Kovarianzmatrix bei Ausschluss eines bestimmten Falls von der Berechnung der Regressionskoeffizienten zur Determinante der Kovarianzmatrix bei Einschluss aller Fälle. Wenn der Quotient dicht bei 1 liegt, beeinflusst der ausgeschlossene Fall die Kovarianzmatrix nur unwesentlich.

Nachfolgender Code und Tabelle zeigen die Auswertung der Residualanalyse für das oben erstellte *model_1*:


```r
  CPS85_Res <- data.frame(Res     = round(resid(model_1), 2),
                          StdRes  = round(rstandard(model_1), 2),
                          StudRes = round(rstudent(model_1), 2),
                          # Cook    = round(cooks.distance(model_1), 2),
                          # DFBeta  = round(dfbeta(model_1), 2),
                          DF5Fit  = round(dffits(model_1), 2),
                          # Lev     = round(hatvalues(model_1), 2),
                          CovRat  = round(covratio(model_1), 2))
  pander(head(CPS85_Res))
```


--------------------------------------------
  Res    StdRes   StudRes   DF5Fit   CovRat 
------- -------- --------- -------- --------
 2.24     0.47     0.47      0.03     1.01  

 -2.76   -0.58     -0.58    -0.03      1    

 -4.46   -0.94     -0.94    -0.04      1    

 2.24     0.47     0.47      0.02     1.01  

 6.74     1.42     1.42      0.07      1    

 -2.26   -0.48     -0.48    -0.03     1.01  
--------------------------------------------

Mit der Residualanalyse kann man auf relativ einfache Weise jene Werte ermitteln (und auch graphisch darstellen), die z.B. um mehr als eine Standardabweichung abweichen. Diese Werte könnte man nochmals genauer untersuchen und gegebenenfalls vor einer weiterführenden Analyse ausschließen[^11]. Keinesfalls sollte sie jedoch dazu verwendet werden, um einen erwünschten Effekt durch schrittweises löschen störender Daten zu erreichen! Kopiere folgenden Code in dein R-Script und führe diesen aus.

[^11]: der Ausschluss von Werten ist nur dann erlaubt, wenn eine entsprechende Begründung (nachvollziehbarer Messfehler, falsche Datenübertragung, etc.) vorliegt!


```r
  # Liste standardisierte Residuen > |1|
  Ind_Res <- which((CPS85_Res$StdRes > 1 | CPS85_Res$StdRes < -1) == TRUE)
  # Anzeige der Werte von wage und educ sowie der Standardisierten Residuen
  # fÃ¼r jene FÃ¤lle, deren Residuen Ã¼ber 1 SD abweichen.
  
  # pander(data.frame(Indizes = Ind_Res,
  #                   wage = CPS85$wage[Ind_Res],
  #                   educ = CPS85$educ[Ind_Res] ,
  #                   CPS85_Res$StdRes[Ind_Res]))
  
  p_Res1 <- ggplot(CPS85, aes(x = educ, y = wage)) + 
            geom_point() +
            geom_point(data=CPS85[Ind_Res,],colour="red",size=3) +
            theme_bw()
  print(p_Res1, comment = FALSE)
```

![](03_Modelle_Mehr_Variablen_files/figure-latex/Modell1_ResidStat_Graph1-1.pdf)<!-- --> 

# Multiple Regression {-}

Man könnte nun die bereits erwähnte Variable Erfahrung (*exper*) ins Modell aufnehmen. Der bereits aus der Korrelation ersichtliche (negative) Zusammenhang mit der Ausbildung *educ* lässt den Schluss auf eine Kovariabilität der beiden Variablen zu. Man nennt derartige Variablen auch **Kovariate**. Im linearen Modell wird diese jedoch wie eine weitere Variable (ein weiterer Prädiktor) zur Vorhersage des Kriteriums verwendet.

## Definition {-}

Die formale Definition eines multiplen linearen Modells ist:

\begin{equation} 
  y_i = b_0 + b_1 \cdot x_{1i} + \cdots + b_k \cdot x_{ki} + \varepsilon_i
  (\#eq:LinModMultFehler)
\end{equation}

Die wesentlichen Parameter dieses Modells sind:

1. Intercept $b_0$: jener Wert den $y_i$ einnimmt, wenn $x_{ji} = 0$ ist (mit $j \epsilon [1,k]$).
2. Steigung $b_i$: die Zunahme von $y_i$, wenn $x_{ji}$ sich um eine Einheit erhöht, bei gleichzeitigem Konstanthalten der restlichen Prädiktorwerte $x_{mi}$ (mit $m [1,k]$ und $m \ne j$)!

Des Weiteren berücksichtigt auch dieses Modell wieder einen Fehler ($\varepsilon_i$). Betrachtet man das multiple Modell isoliert (also ohne Fehlerterm), ist folgende Schreibweise üblich:

\begin{equation} 
  \hat{y}_i = b_0 + b_1 \cdot x_{1i} + \cdots + b_k \cdot x_{ki}
  (\#eq:LinModMult)
\end{equation}

Betrachten wir an unseren Beispieldaten folgendes Modell mit zwei Prädiktoren:

\begin{eqnarray*} 
  \hat{wage}_i = b_0 + b_1 \cdot educ_{i} + b_2 \cdot exper_{i}
  (\#eq:LinModMultBsp)
\end{eqnarray*}


```r
  model_2     <- lm(wage ~ educ + exper, data = CPS85)
  Det_model_2 <- pander(summary(model_2))
  plotPlane(model = model_2, plotx1 = "educ", plotx2 = "exper")
```

![](03_Modelle_Mehr_Variablen_files/figure-latex/Modell2-1.pdf)<!-- --> 

Dabei entspricht der Koeffizient $b_2$ der Zunahme des Gehaltes $\hat{y}_i$ wenn sich die Erfahrung $x_{2i}$ um eine Einheit erhöht und die Ausbildung $x_{1i}$ konstant gehalten wird. In nachfolgernder Tabelle sind die Werte der Vorhersagen des Modells für den vorliegenden Datensatz auszugsweise dargestellt:


```r
  MinExp    <- min(CPS85$exper)
  MaxExp    <- max(CPS85$exper)
  RowSeq    <- seq(from = 1, to = MaxExp, by = 1)
  educVon   <- 10
  educBis   <- 18
  AnzCols   <- educBis - educVon + 1
  Predicted <- matrix(NA, nrow = MaxExp, ncol = AnzCols)
  for (i in seq(from = 1, to = MaxExp, by = 1)) {
    new_input     <- data.frame(educ = educVon:educBis, exper = i)
    Predicted[i,] <- predict(model_2, newdata = new_input)
  }
  Predicted           <- data.frame(seq(from = 1, to = MaxExp, by = 1), Predicted)
  colnames(Predicted) <- c("Exp", "Edu10", "Edu11","Edu12", "Edu13",
                           "Edu14","Edu15", "Edu16","Edu17", "Edu18")
  TabRows2Disp        <- c(1:3, 53:55)
  Predicted2Disp      <- Predicted[TabRows2Disp,]
  row.names(Predicted2Disp) <- NULL
  pander(Predicted2Disp, style = "rmarkdown")
```



| Exp | Edu10 | Edu11 | Edu12 | Edu13 | Edu14 | Edu15 | Edu16 | Edu17 | Edu18 |
|:---:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
|  1  | 4.46  | 5.386 | 6.312 | 7.238 | 8.164 | 9.09  | 10.02 | 10.94 | 11.87 |
|  2  | 4.565 | 5.491 | 6.417 | 7.343 | 8.269 | 9.195 | 10.12 | 11.05 | 11.97 |
|  3  | 4.671 | 5.597 | 6.522 | 7.448 | 8.374 |  9.3  | 10.23 | 11.15 | 12.08 |
| 53  | 9.927 | 10.85 | 11.78 | 12.71 | 13.63 | 14.56 | 15.48 | 16.41 | 17.33 |
| 54  | 10.03 | 10.96 | 11.88 | 12.81 | 13.74 | 14.66 | 15.59 | 16.51 | 17.44 |
| 55  | 10.14 | 11.06 | 11.99 | 12.92 | 13.84 | 14.77 | 15.69 | 16.62 | 17.55 |

```r
  
  CPS852Disp           <- melt(Predicted,
                               id.vars = "Exp",
                               measure.vars = c("Edu10", "Edu11", "Edu12",
                                                "Edu13", "Edu14","Edu15",
                                                "Edu16", "Edu17", "Edu18"))
  CPS852Disp$Exp       <- rep(1:55, 9)
  colnames(CPS852Disp) <- c("Exp", "Edu", "WagePred")
  p                    <- ggplot(CPS852Disp, aes(x = Exp, y = WagePred, color = Edu)) +
                          geom_line() +
                          theme_bw()
  print(p, comment = FALSE)
```

![](03_Modelle_Mehr_Variablen_files/figure-latex/Modell2_1-1.pdf)<!-- --> 

## Modellvergleich {-}

Ein Modell sollte die Wirklichkeit mit möglichst großer Genauigkeit abbilden. Bei der Erstellung des Modells wurden aufgrund einer Stichprobe aus der Grundgesamtheit die Modellparameter (z.B. die $b$’s) bestimmt. Um nun festzustellen, inwieweit das Modell brauchbare Vorhersagen liefert, sollte man das Modell evaluieren. In den vorangegangen Beispielen wurden zwei Modelle (*model_1* und *model_2*) erstellt.

Der Vergleich der Modelle ist über den Fehler des jeweiligen Modells möglich. Je kleiner der Fehler, desto besser bildet das Modell die beobachteten Werte ab. Im Idealfall (Fehler = 0), würden alle beobachteten Werte gleich den vorhergesagten Werten sein und damit auf der Linie liegen.


```r
  M          <- data.frame(wage = CPS85$wage, educ = CPS85$educ, exper = CPS85$exper)
  MV_Data    <- data.frame(educ = M$educ, exper = M$exper)
  MSE_Model1 <- round(mean(resid(model_1)^2),2)
  #MSE_Model1 <- mean((M$wage - predict(model_1, newdata = MV_Data))^2)
  StdResid <- rstandard(model_1)
  #StdResid <- (resid(model_1)-mean(resid(model_1)))/sd(resid(model_1))
  MSE_Model2 <- round(mean((M$wage - predict(model_2, newdata = MV_Data))^2),2)
```

Der Modellvergleich der obigen Beispiele ergibt für das Modell 1 einen $MSE_1 =$ 22.52 und für Modell 2 einen $MSE_2 =$ 21.04.

Bei diesen Ergebnis lässt sich zunächst nur feststellen, dass der $MSE_2$ kleiner als der $MSE_1$ ist. Ob diese Verringerung des $MSE$ von statistischer und/oder praktischer Signifikanz ist, wird im folgenden noch genauer betrachtet.

Mit einer einfachen ANOVA lässt sich nun auch die statistische Signifikanz der Änderungen im Fehler bei den verwendeten Modellen berechnen. Betrachten wir zunächst die statistische Änderung die Modell 1 im Vergleich zum Mittelwertsmodell erzielt:


```r
  # ANOVA Tests auf signifikante Ã„nderungen model_1 vs Mittelwertsmodell
  # Berechnung der Quadratsummen fÃ¼r die Regression (educ)
  preds_1            <- predict(model_1, newdata = CPS85)
  AnzPred            <- 2 # b_0 und b_1
  SS_Regression_1    <- sum((preds_1 - mean(preds_1))^2)
  Zdf_Regression_1   <- AnzPred - 1
  MSS_Regression_1   <- round(SS_Regression_1 / Zdf_Regression_1, 2)
  # Berechnung der Quadratsummen des Fehlers (Residuals)
  Residuals_1        <- CPS85$wage - preds_1
  SS_Residuals_1     <- sum(Residuals_1^2)
  Ndf_Residuals_1    <- nrow(CPS85) - AnzPred
  MSS_Residuals_1    <- round(SS_Residuals_1 / Ndf_Residuals_1, 2)
  # Berechnung der Teststatistik
  F_Wert             <- round(MSS_Regression_1 / MSS_Residuals_1, 2)
  # Berechnung der totalen Quadratsumme
  SS_Total_1         <- sum((CPS85$wage - mean(CPS85$wage))^2)
  CPS85_Total        <- nrow(CPS85) - 1
  # Vergleich mit den Ergebnissen der ANOVA
  pander(anova(model_1))
```


--------------------------------------------------------------
    &nbsp;       Df    Sum Sq   Mean Sq   F value    Pr(>F)   
--------------- ----- -------- --------- --------- -----------
   **educ**       1     2053     2053      90.85    5.474e-20 

 **Residuals**   532   12023     22.6       NA         NA     
--------------------------------------------------------------

Table: Analysis of Variance Table

Das Ergebnis zeigt uns, dass Modell 1 im Vergleich zum Mittelwertsmodell zu einer statistisch signifikanten Fehlerreduktion führt. Bei der händischen Berechnung der Prüfgrößen erhalten wir für die mittlere Quadratsumme der Regression (also der Varianz der Werte die durch das Modell vorhergesagt werden) einen Wert von $MSS_{Regression} = $ 2053.29, welcher ident mit dem Wert der ANOVA-Tabelle ist.

Die restlichen Kennwerte stimmen auch mit dem Ergebnis der ANOVA überein ($MSS_{Residual}$ =  22.6, F(1,532) = 90.85).

Wird das Modell 1 erweitert (auf Modell 2), stellt sich die Frage, ob diese Erweiterung im statistischen Sinn zu einer signifikanten Verbesserung führt. Bei diesem Vergleich wird nun die Änderung (Change Statistic) zwischen Modell 1 und Modell 2 auf Signifikanz geprüft.


```r
  # ANOVA Tests auf signifikante Ã„nderungen model_1 vs model_2 (Ã„nderung signifikant?)
  pander(anova(model_1, model_2))
```


-----------------------------------------------------
 Res.Df    RSS    Df   Sum of Sq     F      Pr(>F)   
-------- ------- ---- ----------- ------- -----------
  532     12023   NA      NA        NA        NA     

  531     11233   1      790.6     37.37   1.893e-09 
-----------------------------------------------------

Table: Analysis of Variance Table

Zum Verständnis dieser Statistik greifen wir kurz zurück auf die verschiedenen Möglichkeiten der Berechnung von Korrelationskoeffizienten zurück. Diese sind:

1. Pearson Korrelationskoeffizient ($r_{xy}$): entspricht der Kovarianz der $z$-transformierten Variablen.
2. Partielle Korrealtionskoeffizient ($r_{xy \cdot z}$): ist die bivariate Korrelation zweier Variablen, welche mittels linearer Regression vom Einfluss einer Drittvariablen bereinigt wurden.
3.Semipartialkorrelation ($sr_{k \cdot x_j}$): zwischen Kriterium und dem $j$-ten Prädiktor ergibt sich als Korrelation von $y$ mit dem Residuum $x_j^*$ der linearen Regression des $j$-ten Prädiktors auf den anderen Prädiktor. Mit anderen Worten, die Semipartialkorrelation gibt den alleinigen Beitrag eines Prädiktors $x_j$ (bereinigt um die gemeinsamen Anteile mit den restlichen Prädiktoren) am Kriterium an. Das Quadrat dieses Koeffizienten wird unter anderm auch als Nützlichkeit des Prädiktors $U_k$ bezeichnet und findet sich z.B. in SPSS als $R^2_{change}$ wieder. Formal: $sr_{k \cdot 12 \cdots (k-1)}^2 = R_{y, 12 \cdots k}^2 - R_{y, 12 \cdots k-1}^2$


```r
  # Korrelationen, Paritial- und Semipartialkorrelationen
  Korr_Data      <- data.frame(wage = M$wage, educ = M$educ, exper = M$exper)
  PearsonKorr    <- cor(Korr_Data)
  ModVgl_Korr    <- pander(PearsonKorr)
  R2Change_mod_1 <- PearsonKorr[2]^2
  # Partial Korrelation zwischen "wage" und "educ" gegeben "exper"
  PartKorr_1       <- pcor.test(Korr_Data$wage, Korr_Data$educ, Korr_Data$exper)
  ModVgl_ParKorr_1 <- pander(PartKorr_1)
  # Partial Korrelation zwischen "wage" und "exper" gegeben "educ"
  PartKorr_2       <- pcor.test(Korr_Data$wage, Korr_Data$exper, Korr_Data$educ)
  ModVgl_ParKorr_2 <- pander(PartKorr_2)
  # Semi-Partial (part) Korrelation zwischen "wage" und "educ" gegeben "exper"
  SemiPartKorr_1      <- spcor.test(Korr_Data$wage, Korr_Data$educ, Korr_Data$exper)
  ModVgl_SemParKorr_1 <- pander(SemiPartKorr_1)
  # Semi-Partial (part) Korrelation zwischen "wage" und "exper" gegeben "edu"
  SemiPartKorr_2      <- spcor.test(Korr_Data$wage, Korr_Data$exper, Korr_Data$educ)
  ModVgl_SemParKorr_1 <- pander(SemiPartKorr_2)
  R2Change_mod_2      <- round(SemiPartKorr_2$estimate^2,3)
  pander(summary(model_2))
```


---------------------------------------------------------------
     &nbsp;        Estimate   Std. Error   t value   Pr(>|t|)  
----------------- ---------- ------------ --------- -----------
 **(Intercept)**    -4.904      1.219      -4.024    6.564e-05 

    **educ**        0.926       0.0814      11.37    5.563e-27 

    **exper**       0.1051      0.0172      6.113    1.893e-09 
---------------------------------------------------------------


-------------------------------------------------------------
 Observations   Residual Std. Error   $R^2$   Adjusted $R^2$ 
-------------- --------------------- ------- ----------------
     534               4.599          0.202       0.199      
-------------------------------------------------------------

Table: Fitting linear model: wage ~ educ + exper

Im vorliegenden Beispiel sind daher die beiden Nützlichkeitsmaße $U_{educ}$ = 0.146 und $U_{exper}$ = 0.056 von Interesse. Ersteres bedeutet, dass die Varianzaufklärung aufgrund der Verwendung der Variablen *educ* 14.6% ist. 
Wird im Modell dann noch der Prädiktor *exper* aufgenommen, werden zusätzliche 5.6% an Varianz des Kriteriums wage erklärt. Insgesamt werden somit $R^2 = 0.202$ oder 20.2% der Varianz des Kriteriums erklärt.
Der Test ($t(531) = 11.37, p< .001$) bestätigt für den Prädiktor *educ*, sowie ($t(531) = 6.11, p<.001$) für den Prädiktor *exper* die statistische Signifikanz.

## Aufgabe MLR 1 {-}

Öffne ein neues R-Script und kopiere die bereits bekannte Kopfzeile in diese Datei. Speichere anschließend das Skript unter dem Namen *SLR_Aufgabe2.R*. Bearbeite nun folgende Aufgabenstellungen:

* Lade die Datei "*Album Sales 2.dat*"
* erstelle ein lineares Modell zur Vorhersage der Verkaufszahlen (*sales*) durch die Variable *adverts*.
* erstelle ein weiteres lineares Modell zur Vorhersage der Verkaufszahlen (*sales*) durch die Variable *adverts*, *airplay* und *attract*.
* Zeige die Ergebnisse des ersten Modells an.
* Zeige die Ergebnisse des zweiten Modells an.
* Vergleiche die beiden Modelle mit einer ANOVA und interpretiere die Ergebnisse.
* Berechne zur Überprüfung der Multikolinearität den Kennwert *Tol* und *VIF* (verwende die Funktion *vif()*. Hinweis: die Toleranz ist der Kehrwert von *VIF*)

[Lösung Aufgabe MLR 1](#aufgabe-mlr-1-lsg)

## Wahl relevanter Prädiktoren {-}

Eine wichtige Frage bei der Modellerstellung betrifft die Wahl der besten Prädiktoren. Prinzipiell muss bereits im Vorfeld der statistischen Analyse bestimmt werden, welche Merkmale für die Modellierung der abhängigen Variablen am geeignetsten sind. Ausreichende theoretische und praktischen Kenntnisse sind daher unbedingt erforderlich. Die Erfassung von potentiellen Prädiktoren ist stets mit zeitlichen und/oder finanziellen Aufwand verbunden. Prädiktoren sind dann gut geeignet, wenn Sie folgende Eigenschaften erfüllen:

1. jeder Prädiktor erklärt möglichst viel der Variabilität des Kriteriums.
2. die Prädiktoren (z.B. $x_1$ und $x_2$) sind im günstigsten Fall voneinander unabhängig ($r(x_1,x_2) \approx 0$)

Diese Eigenschaft kann man durch eine einfache paarweise Korrelation prüfen. Vor allem wenn die zweite Eigenschaft nicht gegeben ist, also wenn einen hohe Korrelationen zwischen zwei Prädiktoren vorliegt, wird es bei der Modellierung zu maßgeblichen Problemen (Multikollinearität) kommen (siehe: [Voraussetzungen der multiplen Regression](#voraussetzungen-der-multiplen-regression).

Neben der Frage nach der Güte einzelner Prädiktoren ist es auch wichtig sich Gedanken über die Anzahl der zu verwendenden Prädiktoren zu machen. Einerseits führt trivialerweise eine höhere Anzahl von Prädiktoren auch zu einer besseren Aufklärung der Varianz im Kriterium. Ausgenommen von Prädiktoren die in keiner Beziehung zum Kriterium stehen, wird jeder zusätzliche Prädiktor mehr oder weniger der verbleibenden Varianz erklären. In den meisten Fällen ist es aber aus zeitlichen/finanziellen oder sonstigen Gründen nicht sinnvoll, eine möglichst große Menge an Prädiktorvariablen zu erheben.

Werden zu viele erklärende Variablen zur Spezifizierung eines Modells verwendet, wird die tatsächliche (geringere) Anpassungsgüte verschleiert. Das Modell wird zwar besser auf die Daten der Stichprobe angepasst, allerdings besteht aufgrund fehlender Generalität keine Übertragbarkeit auf die Grundgesamtheit.
Grundsätzlich sollte wie bereits erwähnt die Wahl der Prädiktoren auf theoretisch und praktisch fundierten Grundlagen erfolgen. Welche der zur Verfügung stehenden Prädiktoren im Endeffekt für das Modell verwendet werden, kann anhand der Modellvergleiche auch im statistischen Sinn evaluiert werden.

Bei der bisher besprochenen Vorgehensweise der Modellerstellung obliegt es dem Analysten, die zu verwendenden Prädiktoren zu bestimmen. Eine weitere Möglichkeit bietet die sogenannte sequentielle Vorgehensweise, bei der die Ein- und Ausschlusskriterien für Prädiktoren durch statistische Kriterien getroffen werden.

## Sequentielle Modellbildung {-}

In manchen Fällen sind nicht ausreichende theoretische Grundlagen und Erfahrungswerte bezüglich der Wirksamkeit und Wichtigkeit von Prädiktoren vorhanden. In solchen Fällen kann ein exploratives Vorgehen bei der Modellerstellung sehr hilfreich sein. Die nachfolgend beschriebene sequentielle Modellierung entspricht einem solchen Ansatz.

Bei der sequentiellen Modellbildung wird ein Modell schrittweise mit unabhängigen Variablen erweitert. In der Regel wird jene Variable, die das $R^2$ am meisten vergrößert und damit die Vorhersage am meisten verbessert hinzugefügt.

Abhängig von der Anzahl der verfügbaren Prädiktoren wird die Bildung neuer Modelle entweder abgebrochen, wenn weitere Variablen keinen weiteren statistischen signifikanten Beitrag zur Varianzaufklärung mehr leisten, oder wenn keine weiteren Variablen zur Verfügung stehen.

Aufgrund der statistischen (maschinellen) Entscheidung über die Verwendung von Prädiktoren, wird diese Vorgehensweise vielfach kritisiert. Nehmen wir in einem sehr einfachen Beispiel einmal an, es stehen 2 Prädiktoren ($x_1, x_2$) zur Vorhersage der abhängigen Variablen zur Verfügung. Der Prädiktor $x_1$ klärt geringfügig weniger Varianz des Kriteriums auf als Prädiktor $x_2$, ersterer ist aber inhaltlich sinnvoller, leichter zu interpretiern und vor allem weit kostengünstiger zu erfassen. Bei der sequentiellen Methode könnte aber aufgrund des Abbruchkriteriums (Signifikanz des Beitrags) genau dieser Prädiktor vom Modell ausgeschlossen werden.

Bei der sequentiellen Methode unterscheidet man noch unterschiedliche Vorgehensweisen hinsichtlich des Hinzufügens/Entfernens von Variablen:

1. Schrittweise (STEPWISE): Diese Methode ist ähnlich wie “Vorwärts”-Selektion, es wird aber zusätzlich bei jedem Schritt getestet, ob die am wenigsten “nützliche” Variable entfernt werden soll.
2. Vorwärts-Selektion (FORWARD): Die Variablen werden sequenziell in das Modell aufgenommen. Diejenige unabhängige Variable, welche am stärksten mit der abhängigen Variable korreliert wird zuerst zum Modell hinzugefügt. Dann wird jene der verbleibenden Variablen hinzugefügt, die die höchste partielle Korrelation mit der abhängigen Variablen aufweist. Dieser Schritt wird wiederholt, bis sich die Modellgüte (R-Quadrat) nicht weiter signifikant erhöht oder alle Variablen ins Modellaufgenommen worden sind.
3. Rückwärts-Elimination (BACKWARD): Zunächst sind alle Variablen im Regressionsmodell enthalten und werden anschließend sequenziell entfernt. Schrittweise wird immer diejenige unabhängige Variable entfernt, welche die kleinste partielle Korrelation mit der abhängigen Variable aufweist, bis entweder keine Variablen mehr im Modell sind oder keine die verwendeten Ausschlusskriterien erfüllen. Im Unterschied zur STEPWISE-Methode wird nicht mehr geprüft, ob die am wenigsten nützliche Variable entfernt werden soll - diese bleibt somit im Modell!

Diese Methoden unterscheiden sich von der sogenannten Einschlussmethode (ENTER), bei der alle Variablen gleichzeitig in das Modell eingefügt werden. Diese Methode wird angewendet, wenn das Modell auf theoretischen Überlegungen basiert. Das heißt, sie eignet sich um Theorien zu testen, während die übrigen Methoden eher im Rahmen explorativer Studien eingesetzt werden.

## Modellvergleich durch AIC {-}

Nach einer (explorativen) Analyse der Daten und der Wahl einer passenden Modellklasse, geht es darum das bestmögliche Modell zu den vorliegenden Daten zu finden (siehe FUB). Daher stellt sich die Frage, was “bestmögliches” Modell bedeutet und wie ein solches bestimmt werden kann. In diesem Zusammenhang wird der Gedanke aufgegriffen, dass mit keinem Regressionsmodell die Realität eins zu eins abgebildet werden kann. Nimmt man zu viele erklärende Variablen auf, läuft man in Gefahr das Modell zu “overfitten” (überanpassen). Ein überangepasstes Modell erklärt die zum Schätzen verwendete abhängige Variable meist sehr gut, schneidet jedoch in der Vorhersage von Daten außerhalb der verwendeten Stichprobe häufig schlecht ab. Auf der anderen Seite kann ein Modell auch “underfitted” sein, d.h. die aufgenommenen unabhängigen Variablen können die abhängige Variable nur sehr unzureichend erklären.

Das Thema der Modellselektion ist ein allgegenwärtiges in der Statistik/ Regressionsanalyse. Dennoch gibt es keine absoluten, objektiven Kriterien anhand derer entschieden werden kann, ob das eine oder das andere Modell gewählt werden sollte. Vielmehr existieren viele verschiedene Verfahren, die versuchen zwischen möglichst viel Erklärungsgehalt des Modells und möglichst wenig Komplexität (siehe dazu [Ockhams Rasiermesser](https://de.wikipedia.org/wiki/Ockhams_Rasiermesser)) abzuwägen.

In einem Artikel von [@Yamashita] wurden folgende Methoden:

a. Partial F
b. Partial Correlation
c. Semi-Partial Correlation
d. Akaike Information Criteria (AIC)

für den Vergleich von Regressionsmodellen untersucht. Die Autoren schließen aus den Ergebnissen ihrer Untersuchung, dass alle Methoden zu den gleichen Ergebnissen, d.h. zur gleichen Modellentscheidung gelangen. Da aber der AIC einerseits leicht zu interpretieren und andererseits auch auf nichtlineare Modelle und Modelle die auf nicht normalverteilten Daten beruhen zu erweitern ist, wird die Anwendung dieses Kriteriums empfohlen.

Das AIC dient also dazu, verschiedene Modellkandidaten zu vergleichen. Dies geschieht anhand des Wertes der log-Likelihood, der umso größer ist, je besser das Modell die abhängige Variable erklärt. Um nicht komplexere Modelle als durchweg besser einzustufen wird neben der log-Likelihood noch die Anzahl der geschätzten Parameter als Strafterm mitaufgenommen.

\begin{equation} 
  AIC_k = 2 \cdot |k| - 2\cdot \hat{L}_k
  (\#eq:AIC)
\end{equation} 

In der Formel steht $k$ für die Anzahl der im Modell enthaltenen Parameter und $\hat{L}_k$ für den Wert der log-Likelihoodfunktion. 

**Das Modell mit dem kleinsten AIC wird bevorzugt.**

Das AIC darf nicht als absolutes Gütemaß verstanden werden. Auch das Modell, welches vom Akaike Kriterium als bestes ausgewiesen wird, kann eine sehr schlechte Anpassung an die Daten aufweisen. Die Anpassung ist lediglich besser als in den Alternativmodellen.

Die praktische Bedeutung soll anhand eines einfachen Beispiels und der Verwendung des Kriteriums bei unseren Beispieldaten erläutert werden.

Nehmen wir an, dass drei Modellvergleiche (mod_1,mod_2,mod_3) folgende AIC-Werte ergeben haben:

$AIC_1 = 100, AIC_2 = 102, AIC_3 = 110$. Berechnet man $e^{(AIC_{min} - AIC_i)/2}$, kann das Ergebnis folgendermaßen interpretiert werden:

* Beim *mod_2* ist es um das $e^{(100-102)/2} = 0.368$-fache wahrscheinlicher den Informationsverlust zu verringern als bei Modell 1 (*mod_1*).
* Beim *mod_3* ist es um das $e^{(100-110)/2} = 0.007$-fache wahrscheinlicher den Informationsverlust zu verringern als bei Modell 1 (*mod_1*).

Bei diesem Beispiel würde man also *mod_3* für weitere Betrachtungen ausschließen. Nachdem aber die Modelle *mod_1* und *mod_2* sehr nahe beisammen liegen, ist es mit den vorliegenden Daten nicht möglich, eine klare Entscheidung für eines der beiden Modelle zu treffen.

Man könnte durchaus noch zusätzliche Daten erheben um dadurch eventuell eine klarere Trennung der beiden Modelle (*mod_1*, *mod_2*) zu erkennen. Ist das nicht möglich, könnte man beide Modelle mit der relativen likelihood gewichten und auf eine statistische Signifikanz testen, oder davon ausgehen, dass mit den vorliegenden Daten eine Modellwahl eben nicht eindeutig zu treffen ist.


## Kreuzvalidierung {-}

Betrachten wir im Folgenden ein Modell (*mod_1*) mit den Prädiktoren *sector* (Berufsgruppe), *exper* (Erfahrung), sowie das um den Prädiktor *age* (Alter) erweiterte Model (*mod_2*).

Die Vorhergehensweise bei der Kreuzvalidierung ist relativ simpel:

1. Erstelle ein/mehrere Modell(e) und berechne die jeweiligen Modellparameter $b_i^j$ (mit $j = j$-tes Modell und $i = i$’ter Parameter) mit einer Teilmenge der zur Verfügung stehenden Daten (z.B. *Training_Data* $\subset$ *DF*).
2. Verwende die restlichen Daten um mit den entsprechenden Modellen Vorhersagen zu berechnen.
3. Berechne die Differenz der beobachteten Daten und der vorhergesagten Daten. Diese Differenz entspricht dem Fehler des Modells ($\rightarrow \epsilon_i$).
4. Berechne den mittleren quadratischen Fehler der Differenzen.

## Voraussetzungen MLR {-}

Folgende Voraussetzungen müssen/sollten bei der linearen Modellierung mit mehreren Prädiktoren erfüllt sein, damit die Ergebnisse auch sinnvoll interpretiert werden können (Bemerkung: im folgenden sei die abhängige Variable $y$ und die Prädiktoren mit den Zahlen ${1, 2, \cdots, k}$ bezeichnet):

1. **Lineare Beziehung** zwischen den Variablen (keine Ausreißer): eine einfache Prüfung erfolgt visuell mit Streudiagrammen, wobei alle Beziehungen, also $r_{y\cdot1}, r_{y\cdot2}, \cdots, r_{y\cdot k}, \cdots, r_{1\cdot2}, r_{1\cdot k}, \cdots, r_{(k-1)\cdot k}$ zu betrachten sind!
2. **Varianzgleichheit der Residuen** (Homoskädasdizität): auch diese Vorausstung kann visuell geprüft werden. Dabei wird ein Streudiagramm der Residuen erstellt, in welchem auf der x-Achse die standardisierten vorhergesagten Werte und auf der y-Achse doe standardisierten Residuen aufgetragen werden. Heteroskedastizität liegt vor, wenn die Punktewolke nicht gleichverteilt um die Gerade liegen!

<center>

![**Abbildung 3**: Homoskedastizität vs. Heteroskedastizität](Images/Homoskedastizitaet.JPG){ width=80% }

</center>

Bekannte Verfahren, um die Nullhypothese „Homoskedastizität“ zu überprüfen sind der:

        * Levene-Test
        * Goldfeld-Quandt-Test
        * White-Test
        * Glejser-Test
        * RESET-Test
        * Breusch-Pagan-Test

3. **Normalverteilung der Residuen**: mittels Histogramm der Fehler zu prüfen - sollte halbwegs normalverteilt sein mit einem Erwartungswert des Fehlers $E(\varepsilon) = 0$. 
4. **Unabhängigkeit der Residuen** (keine Autokorrelation): verletzt wird diese Voraussetzung, wenn aufeinanderfolgende Werte abhängig sind (z.B. auf einen hohen Wert folgt ein hoher Wert, etc.). Vor allem bei Längsschnittdaten ein Thema, bei welchen die Prüfung durch die Durbin-Watson-Methode empfohlen wird. Es gilt: $d = \frac{\sum_{i} (e_i - e_{i-1})^2}{\sum_{i} (e_i)^2}$ mit $d \approx 2$, Werte zwischen $1.5 < d < 2.5$ sind noch akzeptabel.

5. **Vollständig spezifizierte Modelle**: werden maßgebliche Prädiktoren nicht im Modell berücksichtigt, wird es auch kaum gelingen, die Varianz des Kriteriums zufriedenstellend zu erklären. Andererseits bewirken Modelle mit vielen Prädiktoren, dass die $\beta$-Gewichte entsprechend klein werden. Bei derartigen Gegebenheiten ist die Stichprobe entsprechend groß zu wählen. 
6. **Keine Multikollinearität**: Multikollinearität bedeutet, dass Prädiktoren existieren, die hoch miteinander korrelieren (z.B. $r_{1\cdot2} > 0.8$). Damit wird es für das Modell schwer, den jeweiligen Beitrag den Prädiktoren zuzuordnen. Besteht rein das Interesse an maximaler Varianzaufklärung des Kriteriums, ist eine hohe Multikollinearität zu vernachlässigen - die $\beta$-Gewichte der einzelnen Prädiktoren darf man dann allerdings nicht interpretieren. Spielen jedoch gerade diese eine wichtige Rolle, kann man entweder hoch korrelierte Prädiktoren zusammenfassen (eventuell Faktorenanalyse/Clusteranalyse vorher durchführen), oder entsprechende Prädiktoren ausschließen. Allerdings sollte man vor dem Ausschluss von Prädiktoren diese auf eventuelle Suppressionseffekte prüfen.

      * *Negative und reziproke Suppression*: man spricht von Suppressionseffekten, wenn ein Prädiktor aus einem anderen Prädiktor irrelevante Varianz unterdrückt (suppression) und dadurch die Beziehung zwischen diesem Prädiktor und dem Kriterium erhöht. Solche Effekte können durchaus beträchtlich sein und u.U. auch einen Prädiktor, der nichts mit dem Kriterium an sich zu tun hat ($r_{y\cdot k} \approx 0$), als wichtigen Bestandteil des Modells werden lassen. Die Aufnahme des Suppressors in das Regressionsmodell hat somit den Effekt, den anderen Prädiktor von diesen Fehlereinflüssen zu bereinigen. Erkennbar sind Suppressionseffekte einerseits durch Vorzeichenwechsel bei Korrelationen (Nullter Ordnung, also der Produkt-Moment-Korrelation) vs. $\beta$-Gewichten (negative Suppression, bzw. NET-Suppression). D.h., dass für nicht-negative Validitäten[^12] ist der Prädiktor $2$ ein negativer Suppressor, falls seine partielle Steigung negativ ist, d. h., falls $B_2 < 0$. Eine *reziproke Suppression* liegt vor, wenn für nicht-negative Validitäten die Korrelation der Prädiktoren negativ ist, d. h., falls $r_{1\cdot2} < 0$. Weitere Details zu Suppressionseffekten siehe Literatur und Diskriminanzanalyse.
      
[^12]: Die Korrelationen des Kriteriums mit den Prädiktorvariablen bezeichnen wir als Validitäten, d. h. die Validität der $j$-ten Prädiktorvariablen ist gleich ihrer Korrelation mit dem Kriterium.
      
7. **Hohe Reliabilität der Prädiktoren und des Kriteriums**: Variablen sind hochreliabel, wenn sie weitgehend frei von Zufallsfehlern sind, also bei Messwiederholung ähnliche Ergebnisse liefern.
8. **Keine Varianzeinschränkung**: eine Einschränkung führt i.A. zu eingeschränkten (niedrigeren) Korrelationen. Z.B.: aus 500 Personen werden 100 augrund eines Aufnahmeverfahrens zu einem Studium zugelassen. Will man die Validität des Aufnahmeverfahrens anhand der Beziehung Studienerfolg und Leistung beim Aufnahmetest prüfen, wird es aufgrund der eingeschränkten Variabilität durch die Aufnahmekriterium zu einer Unterschätzung kommen.
9. **Unabgängigkeit der Beobachtungseinheiten**: eine Verletzung dieser Voraussetzung, kann zu einer maßgeblichen Reduktion der Teststärke des Modells führen. Z.B. soll die Teamorientierung in einem Unternehmen untersucht werden. Diese wird sicher zwischen den einzelnen Personen variieren, aber darüber hinaus kann diese auch abhängig von der Abteilung sein, in welcher Personen arbeiten. Die Variabilität kann dadurch bei bestimmten Abteilungen stark eingeschränkt sein, was einer Reduktion des Stichprobenumfangs und damit einer Teststärkenreduktion gleichzusetzen ist. In solchen Fällen könnte man eine Multilevel-Analyse (gemischtes hierarchisches Modell) einsetzen!

Zusammenfassend lässt sich festhalten, dass eine Verletzung einer/mehrerer dieser Voraussetzungen meistens dazu führt, dass die Genauigkeit der Vorhersage gemindert wird. Relativ einfach zu prüfen sind die ersten drei Voraussetzungen (graphisch, Kennwerte wie Korrelation, etc.). Bei der Überprüfung der restlichen Voraussetzung muss man i.A. auf entsprechende statische Verfahren zurückgreifen, die hier aber nicht näher besprochen werden. Einen Überblick über die Möglichkeiten zur Überprüfung der Voraussetzungen finden Sie z.B. unter [@UZH], oder MR2 - [@Hemmerich].


# Lösungen {-}

## Aufgabe SLR 1 Lsg {-}


```r
  album1       <- read.delim("Daten/Album Sales 1.dat", header = TRUE)
  ggplot(album1, aes(x = adverts, y = sales)) +
    geom_point() +
    geom_smooth(method=lm, se=FALSE) +
    theme_bw()
  albumSales.1 <- lm(sales ~ adverts, data = album1)
  pander(summary(albumSales.1))
  
# #---- Modell1_Pred_1
#   
#   new_input <- data.frame(educ = 10:14)
#   pander(predict(model_1, newdata = new_input), style = "rmarkdown")
```

[zurück zur Aufgabenstellung](#aufgabe-slr-1)

## Aufgabe MLR 1 Lsg {-}


```r
  album2       <- read.delim("Daten/Album Sales 2.dat", header = TRUE)
  # Erstes Modell
  albumSales.2 <- lm(sales ~ adverts, data = album2)
  # zweites Modell
  albumSales.3 <- lm(sales ~ adverts + airplay + attract, data = album2)
  # Ausgabe Ergebnisse
  pander(summary(albumSales.2))
  pander(summary(albumSales.3))
  # Modellvergleich
  anova(albumSales.2, albumSales.3)
  Tol <- 1/vif(albumSales.3)
  VIF <- vif(albumSales.3)
```

[zurück zur Aufgabenstellung](#aufgabe-mlr-1)
