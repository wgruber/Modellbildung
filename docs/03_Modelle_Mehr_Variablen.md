

# (PART\*) Teil III: Modelle mit mehr Variablen {-}



# Korrelationen {-}

Korrelation ist ein Maß für den statistischen Zusammenhang zwischen zwei Datensätzen. Unabhängige Variablen sind daher stets unkorreliert. Korrelation impliziert daher auch stochastische Abhängigkeit. Durch Korrelation wird die lineare Abhängigkeit zwischen zwei Variablen quantifiziert.

Auch wenn Korrelation eine *deskriptive Statistik* ist, wird sie durch eine Reihe von Verfahren, wie z.B. partielle Korrelation, multiple Korrelation oder Faktorenanalyse, verfeinert. Es ist ein absolut unverzichtbares Werkzeug für viele Forschungsgebiete.

## Kausalität {-}

Eine relevante (statistisch signifikante) Korrelation liefert keinen Beleg für Kausalität. Vor allem in der Medizin und Psychologie suchen Forscher nach Kriterien für Kausalität. Es existieren mehrere Ansätze, nachfolgend seien hier die neun Kriterien von Hill (1965) angeführt:

1. *Stärke der Assoziation (Effektstärke)*: Eine geringe Effektsstärke bedeutet nicht, dass keine Beziehung zwischen den Variablen existiert, aber bei einer größeren Effektstärke ist eine kausale Beziehung wahrscheinlicher.
2. *Konsistenz (Reproduzierbarkeit)*: Übereinstimmende Befunde, festgestellt durch verschiedene Personen an verschiedenen Orten mit verschiedenen Stichproben, verstärkt die Wahrscheinlichkeit eines Effekts.
3. *Spezifität*: Kausalität ist wahrscheinlich, wenn es keine andere bessere Erklärung für das Auftreten des Ereignisses gibt. Je spezifischer die Beziehung zwischen einem Faktor und einem Effekt ist, desto höher die Wahrscheinlichkeit eines kausalen Zusammenhangs.
4. *Zeitbedingtheit*: Die Ursache muss der Wirkung vorausgehen (wenn erwartet wird, dass es eine Verzögerung nach der Ursache und dem erwarteten Effekt gibt, dann muss der Effekt nach der Verzögerung eintreten).
5. *Dosis-Wirkungs-Beziehung*: Größere Exposition sollte gewöhnlich auch zu einer größeren Auftretenshäufigkeit des Effekts führen. In einigen Fällen jedoch kann bereits die bloße Anwesenheit eines Faktors einen Effekt auslösen. In anderen Fällen wird der umgekehrte Fall beobachtet: die Anwesenheit eines Faktors reduziert die Auftretenshäufigkeit.
6. *(Biologische) Plausibilität*: Ein plausibler Mechanismus zwischen Ursache und Wirkung ist hilfreich (allerdings fügte Hill auch hinzu, dass das Verständnis von Ursache und Wirkung durch unseren aktuellen Wissensstand begrenzt sein kann).
7. *Koheränz*: Die Stimmigkeit zwischen epidemiologischen- und Laborbefunden erhöht die Wahrscheinlichkeit eines Effekts. Hill fügte allerdings hinzu, dass das Fehlen eines Laborbefundes nicht einen epidemiologischen Effekt auf die Beziehung ungültig machen kann.
8. *Experiment*: Es ist wahrscheinlicher, dass eine Beziehung kausal ist, wenn sie experimentell verifiziert werden kann.
9. *Analogie*: Der Effekt ähnlicher Faktoren darf berücksichtigt werden.

## Linearität {-}

Ein Korrelationskoeffizient zeigt die Stärke eines *linearen Zusammenhangs* zwischen zwei Variablen. Aber der Wert von $r$ charakterisiert nicht die genaue Art des Zusammenhangs oder das Aussehen des Punktdiagramms beider Variablen[^6].

[^6]: [Abbildungen aus Matheguru](https://matheguru.com/stochastik/korrelation-korrelationskoeffizient.html)

<center>

![**Abbildung 2**: Korrelation und Linearität](Images/03_LinearitaetKorrelation.JPG){ width=80% }

</center>

## Korrelationskoeffizienten {-}

Neben dem Pearson-Produkt-Moment-Korrelationskoeffizienten $r$ existieren noch etliche weitere Korrelationskoeffizienten und Zusammenhangsmaße. Die meisten hiervon sind Sonderfälle der Pearson-Produkt-Moment-Korrelation. Die Tabelle (unten) zeigt, wann welcher Koeffizient berechnet werden soll, abhängig von dem Skalenniveau der beteiligten Variablen.

<center>

![**Abbildung 3**: verschiedene Korrelationskoeffizienten](Images/Korrelationskoeffizienten.JPG){ width=100% }

</center>

Weiter Infos zu den einzelnen Korrelationskoeffizienten sind der Literatur zu entnehmen. Eine übersichtliche Darstellung findet man auch unter folgendem [Link](https://matheguru.com/stochastik/korrelation-korrelationskoeffizient.html).

## Modell {-}

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

Die Regression basiert auf der Korrelation und ermöglicht die bestmögliche Vorhersage für eine Variable. Im Gegensatz zur Korrelation muss hierbei festgelegt werden, welche Variable durch eine andere Variable vorhergesagt werden soll. Die Variable die vorhergesagt werden soll nennt man bei der Regression *Kriterium* ($y$). Die Variable die für die Vorhersage eingesetzt wird bezeichnet man als *Prädiktor* ($x_i$)[^7]. Anhand des Prädiktors wird demzufolge das Kriterium vorhergesagt.

[^7]: wobei $i$ als Index für die Anzahl der verwendeten Prädiktoren steht. Bei einem einfachen Modell ist $i = 1$

## Definition {-}

Die formale Definition eines einfachen linearen Modells ist:

\begin{equation} 
  y = b_0 + b_1 \cdot x_1 + \varepsilon_1
  (\#eq:LinModFehler)
\end{equation}

Die wesentlichen Parameter dieses einfachen Modells sind:

1. Intercept $b_0$: jener Wert den $y$ einnimmt, wenn $x_1 = 0$ ist.
2. Steigung $b_1$: die Zunahme von $y$, wenn $x_1$ sich um eine Einheit erhöht.

Des Weiteren berücksichtigt dieses Modell auch einen Fehler ($\varepsilon_1$). Damit kommt auch ein ganz zentraler Teil bei der Modellbildung zum Ausdruck. Die meisten Modelle definieren sich also aus:

\begin{equation} 
  \textrm{wahrer Wert} = \textrm{Modell} + \textrm{Fehler}
  (\#eq:AllgModellvorstellung)
\end{equation}

Daraus lässt sich auch folgende Erkenntnis bezüglich des Modells direkt ableiten:

1. Je kleiner die Summe der Fehler sind, desto besser ist das Modell.
2. Je genauer das Modell, desto kleiner wird auch der Fehler sein.

Mit dieser Erkenntnis wird auch klar, dass i.A. ein ganz einfaches Modell (mit einem einzigen Prädiktor) nur zu einer bedingten Reduktion des Fehlers geeignet ist. Wir werden uns im weiteren Verlauf mit erweiterten Modellen beschäftigen, wollen aber zunächst die Eigenschaften des einfachen linearen Modells näher betrachten. Im folgenden Link findet man eine gute [Veranschaulichung des einfachen linearen Modells](https://phet.colorado.edu/sims/html/least-squares-regression/latest/least-squares-regression_en.html).

Betrachtet man das Modell isoliert (also ohne Fehlerterm), ist folgende Schreibweise üblich:

\begin{equation} 
  \hat{y} = b_0 + b_1 \cdot x_1
  (\#eq:LinMod)
\end{equation}

### Berechnung der Koeffizienten {-}

Für die Berechnung der Koeffizienten wird das Kriterium der kleinste Quadrate (MLS) angewandet. Einfach ausgedrückt wird eine Gerade durch die beobachteten Daten gesucht, die folgenden Eigenschaften aufweist:

1. die Summe der quadratischen Abstände jeder Beobachtung zum entsprechenden Punkt auf der Geraden ist ein Minimum, also $\sum_{i=1}^{N} \varepsilon_1^2 = min$.
2. es gibt keine andere Gerade die eine kleinere Summe dieser Fehler liefert.

Die Berechnung der Parameter entspricht daher einer Extremwertaufgabe, d.h. die partiellen Ableitungen werden auf Null gesetzt. Daraus lassen sich dann die Parameter $b_0, b_1$ berechnent. Details dazu siehe [Wikipedia](https://de.wikipedia.org/wiki/Einfache_lineare_Regression).

## Modellanwendung {-}

Zur Anwendung eines einfachen linearen Modell betrachten wir wiederum die bereits bekannten Daten aus dem Datensatz *CPS85*. Diese Mal wollen wir das Gehalt (*wage*) durch die Ausbildungsdauer (*educ* in Jahren) vorhersagen. Formal lautet das Modell demnach:

\begin{equation} 
   \hat{\textrm{wage}} = b_0 + b_1 \cdot \textrm{educ}
  (\#eq:LinModBsp1)
\end{equation}

Die Werte der Parameter $b_0, b_1$ können für dieses Beispiel entsprechend der obigen Erläuterung folgendermaßen interpretiert werden:

1. Für eine Person mit keiner Ausbildung ($\textrm{wage} = x_1 = 0$) wird durch das Modell ein Einkommen $y = b_0$ vorhergesagt.
2. Erhöht man die Ausbildungsdauer $x_1$ um ein Jahr, steigt der Gehalt $y$ um das $b_1$-fache an.

Kopiere zur Veranschaulichung folgenden Code in dein R-Script und führe diesen aus.


```r
  DF <- CPS85
  ggplot(CPS85, aes(x = educ, y = wage)) + 
    geom_point() +
    geom_smooth(method=lm,
                se=FALSE) +
    theme_bw()
```

<img src="03_Modelle_Mehr_Variablen_files/figure-html/Modell1-1.png" width="672" />

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

Die in der Tabelle angegebenen Werte der Spalte **Estimate** entsprechen dabei den Parametern $b_0, b_1$ des Modells. Eine weitere wesentliche Kennzahl für die Interpretation des Modells ist der Spalte $R^2$ zu entnehmen. Dieser Wert wird als *Determinationskoeffizient*[^8] bezeichnet. Umgerechnet in \% (im vorliegenden Beispiel also 14.43\%) besagt der Wert, wie viel der Variablität des Gehaltes durch den Prädiktor Ausbilung erklärt wird. Wir werden im weiteren Verlauf noch öfter auf diesen Kennwert zurückkommen.

[^8]: häufig auch als Varianzaufklärung

Welche Gehälter würden für Ausbildungszeiten zwischen 10 und 14 Jahren vorhergesagt werden? Kopiere folgenden Code in dein R-Script und führe diesen aus. Änder auch den Wertebereich der Prädiktoren und beobachte was dabei passiert!


```r
  new_input <- data.frame(educ = 10:14)
  pander(predict(model_1, newdata = new_input), style = "rmarkdown")
```


------------------------------------
   1       2      3      4      5   
------- ------- ------ ------ ------
 6.759   7.509   8.26   9.01   9.76 
------------------------------------

Im Vergleich zum Mittelwert-Modell zeigt sich mit steigender Ausbildung ein höheres Einkommen. Der Fehler bei der Vorhersage des Einkommens wird sich daher durch diese Modellvorstellung verringern (mehr zur Abschätzung der Fehlerreduktion später).

## Residualanalyse {-}

Ein zentrales Thema der Modellbildung ist die Beurteilung und (statistische) Auswertung der Abweichungen des Modells von den Beobachtungen (Fehler, Residum). Folgende Kennwerte bilden die Möglichkeit, die Güte des Modells abzuschätzen:

1. *Vorhergesagte Werte*: vorhergesagte Werte der Regressionsgleichung (= Werte die auf der Geraden liegen).
2. *Residuen*: tatsächliche Wert der abhängigen Variablen minus des vorhergesagten Werts aus der Regressionsgleichung.
3. *Distanzen*: Maße zum Auffinden von Fällen mit ungewöhnlichen Wertekombinationen bei den unabhängigen Variablen und von Fällen, die einen großen Einfluss auf das Modell haben könnten.
4. *Vorhersageintervalle*: obere und untere Grenzen sowohl für Mittelwert als auch für einzelne Vorhersageintervalle.
5. *Einflussstatistiken*: Änderung in den Regressionskoeffizienten (DfBeta(s)) und vorhergesagten Werten (DfFit), die sich aus dem Ausschluss eines bestimmten Falls ergeben. 

Die Detailanalyse der Residuen soll dazu dienen, die Güte eines Modells besser beurteilen zu können.


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

Mit der Residualanalyse kann man auf relativ einfache Weise jene Werte ermitteln (und auch graphisch darstellen), die z.B. um mehr als eine Standardabweichung abweichen. Diese Werte könnte man nochmals genauer untersuchen und gegebenenfalls vor einer weiterführenden Analyse ausschließen[^9]. Keinesfalls sollte sie jedoch dazu verwendet werden, um einen erwünschten Effekt durch schrittweises löschen störender Daten zu erreichen! Kopiere folgenden Code in dein R-Script und führe diesen aus.

[^9]: der Ausschluss von Werten ist nur dann erlaubt, wenn eine entsprechende Begründung (nachvollziehbarer Messfehler, falsche Datenübertragung, etc.) vorliegt!


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

<img src="03_Modelle_Mehr_Variablen_files/figure-html/Modell1_ResidStat_Graph1-1.png" width="672" />

