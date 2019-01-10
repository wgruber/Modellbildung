

# (PART\*) Teil II: Modelle mit einer Variablen {-}



# Datenbeschreibung {-}

Betrachten wir zunächst einen einfachen Datensatz aus dem Projekt MOSAIC Data Sets (Paket mosaicData, **CPS85**)[^2]. 



[^2]: [Project MOSAIC](http://mosaic-web.org/), is a community of educators working to develop a new way to introduce mathematics, statistics, computation and modeling to students in colleges and universities.

Diese Datei beinhaltet *N =* ``534`` Beobachtungen und *k =* ``11`` Variablen, deren Namen in folgender Tabelle nochmals separat angeführt sind:


 LNr  Variablenname 
----  --------------
   1  wage          
   2  educ          
   3  race          
   4  sex           
   5  hispanic      
   6  south         
   7  married       
   8  exper         
   9  union         
  10  age           
  11  sector        

Angenommen Sie müssten auf Basis der vorliegenden Daten für eine Person das durchschnittliche Einkommen (*wage*) schätzen, ohne dabei andere Variablen zu berücksichtigen. Welchen Wert würden Sie wählen?

# Deskriptive Statistik {-}

Bevor man diese Frage beantwortet, sollte man sich die deskriptive Statistik der entsprechenden Variablen genauer ansehen. In der vorliegenden Fragestellung handelt es sich um eine intervallskalierte Variable, daher ist die Betrachtung der Kennwerte für zentrale Tendenzen (Mittelwert, Median, Modus, Minimum, Maximum und Range), der Dispersion (Varianz, Standardabweichung, Quartile, Standardfehler, Konfidenzintervalle, Schiefe und Kurtosis), sowie die Darstellung der Verteilung in einem Histogramm sehr hilfreich. 

## Tabellen {-}

Kopiere den nachfolgenden Code in den Editor und führe in aus. Diskutiere die Ergebnisse.


```r
  Income <- CPS85$wage
  library(pastecs)
    kable(stat.desc(Income))
    # DT::datatable(data.frame(stat.desc(Income)))
  library(psych)
    kable(describe(Income))
    # DT::datatable(data.frame(describe(Income)))

  # HÃ¤ufigkeitstabellen
  SR  <- table(CPS85$sex, CPS85$race)
  kable(SR)
  SRM <- table(CPS85$sex, CPS85$race, CPS85$married)
  kable(SRM)
  # HÃ¤ufigkeitstabellen mit Randsummen
  x0 <- addmargins(table(CPS85$sex, CPS85$race))
  kable(x0)
```

Um die Eigenschaften des Mittelwertes bei vorliegen von starken Abweichungen in den Daten noch besser zu verdeutlichen, setzen wir bei 50 zufällig gewählten Personen das Einkommen drastisch hinauf. Kopiere den folgenden Code ins RStudio und führe diesen dann aus.


```r
  IncomeNew     <- CPS85$wage
  ID            <- sample(1:534, 50)
  IncomeNew[ID] <- IncomeNew[ID] + 18
```

## Aufgabenstellung 1 {-}

Erstelle nun für die neuen Daten eine Tabelle und ein Histogramm. Berechne den Mittelwert:

* ohne Berücksichtigung der Ausreißer (Funktion *mean(???, na.rm = TRUE)*)
* unter Berücksichtigung der Ausreißer (Funktion *mean(???, trim = ???, na.rm = TRUE)*)

Diskutiere die Ergebnisse. Die Lösung zu diesen Aufgaben findest du in [Lösung Aufgabe 1](#aufgabe_1)

## Codebooks in R {-}

In R hat man die Möglichkeit, mit Hilfe des Pakets *codebook* eine genaue Beschreibung der Daten (inklusive einer deskriptiven Statistik für jede Variable) zu erstellen. Für den vorliegenden Datensatz wurde auszugsweise eines erstellt, welches in Kapitel [Codebook CPS85](#codebook-cps85) zu finden ist.

# Mittelwerts-Modell {-}

Eine gute Schätzung wäre daher unter bestimmten Voraussetzungen (Verteilungseigenschaften) der Mittelwert, da dieser die folgende Eigenschaft besitzt:

* Die Summe der quadrierten Abweichungen der Beobachtungswerte $x_i$ von einem beliebigen Punkt $m$ wird minimal, wenn dieser Punkt $m = \bar{x}$, also der arithmetische Mittelwert ist!

Damit diese Schätzung inhaltlich auch Sinn ergibt, ist jedoch eine (halbwegs) symmetrische Verteilung in Form einer Glockenkurve erforderlich. Weicht diese Verteilung stark davon ab, so wird der Mittelwert nur ein schlechtes Modell für die Population sein.

Zur Veranschaulichung von Verteilungseigenschaften einer Variablen eignen sich vor allem Histogramme, Boxplots und Q-Q-Plots. Kopiere den folgenden Code ins RStudio und führe diesen dann aus. Diskutiere die Ergebnisse.


```r
  # Histogramme und Density-Plots
  p1 <- ggplot(CPS85, aes(x = wage)) + geom_histogram()
  p2 <- ggplot(CPS85, aes(x = age)) + geom_histogram(binwidth = 4)
  p3 <- ggplot(CPS85, aes(x = exper)) + geom_density()
  # Boxplots
  x1 <- mosaic::mean_(wage ~ sex, data = CPS85)
  x2 <- mosaic::sd(wage ~ sex, data = CPS85)
  x3 <- mosaic::quantile(wage ~ sex, data = CPS85)
  x4 <- mosaic::favstats(wage ~ sex, data = CPS85)
  x5 <- gf_boxplot(wage ~ sex, data = CPS85)
  x6 <- gf_point(wage ~ sex, data = CPS85)
  # Q-Q Plots
  qqnorm(CPS85$wage, pch = 1, frame = FALSE)
  qqline(CPS85$wage, col = "steelblue", lwd = 2)
```

Eine der häufigsten Ursachen für Verzerrungen in den Verteilungseigenschaften einer Variablen sind Ausreißer. Die Behandlung von Ausreißern ist ein eigenes und heftig diskutiertes Thema in der Statistik. Wir wollen uns im Rahmen dieser LV nicht weiter damit auseinandersetzen. Eine (wenngleich nicht unbedenkliche) Methode ist das sogenannte *Trimmen* der Daten. Nachfolgendes Beispiel zeigt eine weitere Möglichkeit[^3], Ausreißer aus einer Analyse zu entfernen. Es sei an dieser Stelle nochmals explizit darauf hingewiesen, dass ein beliebiges Weglassen von *störenden* Werten durchaus bedenklich ist und eigentlich nur im Sinne einer explorativen Analyse von Daten (was wäre, wenn die Daten keine Ausreißer hätten[^4]?) gerechtfertigt werden kann! Kopiere den folgenden Code ins RStudio und führe diesen dann aus. Diskutiere die Ergebnisse.

[^3]: wir haben bereits bei der Mittelwertsfunktion *mean()* das Argument *trim* kennengelernt. 

[^4]: liegen z.B. Kenntnisse der Verteilungseigenschaften in der Population vor, aber die vorliegende Stichprobe ist sehr klein, könnte man eventuell 


```r
  # panderOptions("table.split.table", 120)
  # pander(head(CPS85), style = "rmarkdown")
  MW_Wage    <- mean(CPS85$wage, na.rm = TRUE)
  Med_Wage   <- median(CPS85$wage, na.rm = TRUE)
  SD_Wage    <- sd(CPS85$wage, na.rm = TRUE)
  CPS85_1    <- CPS85[!CPS85$wage %in% boxplot.stats(CPS85$wage)$out,]
  MW_Wage_1  <- mean(CPS85_1$wage, na.rm = TRUE)
  Med_Wage_1 <- median(CPS85_1$wage, na.rm = TRUE)
  SD_Wage_1  <- sd(CPS85_1$wage, na.rm = TRUE)
  # Modell0_Graph_1 ----
  ggplot(CPS85, aes(x = wage)) +
    geom_histogram(aes(y    = ..density..),
                   binwidth = .5,
                   colour   = "black", fill = "white") +
    geom_density(alpha = .2, fill = "#FF6666") +
    geom_vline(aes(xintercept = mean(wage, na.rm = T)),
               color = "red", linetype = "dashed", size = 1) +
    geom_vline(aes(xintercept=median(wage, na.rm=T)),
               color = "blue", linetype = "dotted", size = 1) +
    theme_bw()
  # Modell0_Graph_2
  ggplot(CPS85_1, aes(x = wage)) +
    geom_histogram(aes(y    = ..density..),
                   binwidth = .5,
                   colour   = "black", 
                   fill     = "white") +
    geom_density(alpha = .2,
                 fill  = "#FF6666") +
    geom_vline(aes(xintercept = mean(wage, na.rm = T)),
               color    = "red",
               linetype = "dashed",
               size = 1) +
    geom_vline(aes(xintercept = median(wage, na.rm = T)),
               color    = "blue",
               linetype = "dotted",
               size     = 1) +
    theme_bw()
  
  pander(shapiro.test(CPS85_1$wage), style = "rmarkdown")
```

## Güteschätzung des Mittelwertsmodells {-}

Ein wichtiger Bestandteil einer Modellbildung ist die Abschätzung der Güte des jeweilig erstellten Modells. Für das Mittelwertsmodell eignet sich der Standardfehler (siehe Eq. \@ref(eq:SE)) als Kennwert zu Abschätzung der Genauigkeit des Modells.

\begin{eqnarray} 
  SE &=& \frac{s}{\sqrt{N}} \\
  s  &=& \frac{\sum_{i = 1}^{N} (x_i - \bar{x})^2}{N-1} \\
  (\#eq:SE)
\end{eqnarray} 

Der Standardfehler (englisch: standard error, meist $SE$ abgekürzt) ist die Standardabweichung der Stichprobenverteilung einer Stichprobenfunktion. In der Regel bezieht sich der Standardfehler dabei auf den Mittelwert und wird meistens dann als standard error of the mean ($SEM$ abgekürzt) bezeichnet.

Erläuterung zum $SE$:

Wenn wir viele zufällige Stichproben aus derselben Grundgesamtheit ziehen und jeweils den Mittelwert berechnen, würden diese Mittelwerte in der Regel unterschiedlich sein. 

Die Mittelwerte haben ihre eigene Verteilung (die wiederum ihren eigenen Mittelwert und ihre eigene Standardabweichung hat). Der Standardfehler des Mittelwerts (also der SEM und damit die Schätzung des Mittelwerts der Grundgesamtheit aus dem Mittelwert der Stichprobe) ist die Standardabweichung der Mittelwerte für alle möglichen Stichproben (mit jeder möglichen Stichprobengröße) die aus der Grundgesamtheit gezogen werden können.

Offenbar spielt bei der Berechnung dieser Kennwerte die Stichprobengröße $N$ eine Rolle. Welche Werte nimmt $s$ und respektive $SE$ ein, wenn $N \rightarrow \infty$ geht?

Wir halten fest, dass die Stichprobenstreuung $s$ abhängig ist von:

* der Streuung $\sigma$ in der Grundgesamtheit
* der Stichprobengröße $N$

Die Streuung in der Grundgesamtheit ist (auch wenn meist unbekannt) ein fixer Wert. Wird $N$ sehr groß nähert sich die Standardabweichung diesem Wert. Im Extremfall, also wenn $N = N_{Pop}$, streuen die Werte genau mit $\sigma$!

Beim Standardfehler hingegen nähert sich mit zunehmenden $N$ der Wert von $SE$  der Null! Im Extremfall, also wenn $N = N_{Pop}$, gibt es nur mehr einen Mittelwert (und der ist gleich $\mu$), welcher auch nicht mehr streut $\Rightarrow$ die Streuung $SE = 0$.

## Konfidenzintervall um den Mittelwert {-}

Aus Stichproben errechnen wir einen oder mehrere verschiedene Werte, die Schätzwerte für die Grundgesamtheit darstellen sollen. Man spricht hier von *Punktschätzer*, da eben jeweils genau ein Wert (Anteils-, Mittelwert oder andere Größe, z. B. Regressionskoeffizient) geschätzt wird.

Wünschenswerte Eigenschaften von Schätzern sind:

* *Erwartungstreue*: Der Erwartungswert (Mittelwert) der Kennwerteverteilung soll dem wahren Parameter in der Grundgesamtheit entsprechen.
* *Effizienz*: Die Streuung des Schätzers soll möglichst klein sein (d. h., die Schätzwerte sollen möglichst häufig möglichst nahe am wahren Wert liegen) 
* *Konsistenz*: Mit zunehmendem Stichprobenumfang sollen Abweichungen vom wahren Wert geringer werden.

Der Punktschätzer ist der beste Schätzer für den (unbekannte) Parameter der Grundgesamtheit. Dennoch ist es recht unwahrscheinlich, dass der Punktschätzer genau dem Parameter entspricht[^5]. Daher sollte man die Punktschätzung durch eine Intervallschätzung ergänzen, die eine größere Wahrscheinlichkeit aufweist – um den Preis einer größeren Bandbreite.

Die Intervallschätzung zielt nun darauf ab, einen Bereich anzugeben, der mit einer gewissen (von der Forscherin gewählten) Wahrscheinlichkeit den wahren Wert enthält (überdeckt). Dieser Bereich heißt [*Konfidenzintervall*](https://de.wikipedia.org/wiki/Konfidenzintervall). Die Wahrscheinlichkeit, mit der das Intervall den wahren Wert enthält, sollte in der Regel möglichst hoch sein. Der trade-off: Je größer die gewählte Wahrscheinlichkeit, desto breiter das resultierende Intervall.

Das Konfidenzintervall berechnet sich aus:

\begin{equation} 
  KI = \bar{x} \pm SE \cdot t_{1 - \frac{\alpha}{2}; n - 1}
  (\#eq:KI)
\end{equation} 

Die Eigenschaften des Konfidenzintervalls lassen sich sehr schön in einer Simulation von [Geoff Cumming](https://thenewstatistics.com/itns/esci/) veranschaulichen.

[^5]: siehe [Prof. Dr. Wolfgang Ludwig-Mayerhofer, Uni Siegen, Punkt- und Intervallschätzungen ](https://www.uni-siegen.de/phil/sozialwissenschaften/soziologie/mitarbeiter/ludwig-mayerhofer/statistik/statistik_downloads/statistik_ii_4.pdf), oder [Springer](https://link.springer.com/content/pdf/10.1007/978-3-642-41995-9_8.pdf)

# Codebook CPS85 {-}

Das nachfolgende [Codebook](#codebooks-in-r) stellt einen Auszug der Daten von NHANES dar.

===========================================================================

   wage

---------------------------------------------------------------------------

   Storage mode: double

          Min.:   1.000
       1st Qu.:   5.250
        Median:   7.780
          Mean:   9.024
       3rd Qu.:  11.250
          Max.:  44.500

===========================================================================

   educ

---------------------------------------------------------------------------

   Storage mode: integer

          Min.:   2.000
       1st Qu.:  12.000
        Median:  12.000
          Mean:  13.019
       3rd Qu.:  15.000
          Max.:  18.000

===========================================================================

   race

---------------------------------------------------------------------------

   Storage mode: integer
   Factor with 2 levels

   Values and labels    N    Percent 
                                     
              1 'NW'   67   12.5     
              2 'W'   467   87.5     

===========================================================================

   sex

---------------------------------------------------------------------------

   Storage mode: integer
   Factor with 2 levels

   Values and labels    N    Percent 
                                     
               1 'F'  245   45.9     
               2 'M'  289   54.1     

===========================================================================

   hispanic

---------------------------------------------------------------------------

   Storage mode: integer
   Factor with 2 levels

   Values and labels    N    Percent 
                                     
            1 'Hisp'   27    5.1     
            2 'NH'    507   94.9     

===========================================================================

   south

---------------------------------------------------------------------------

   Storage mode: integer
   Factor with 2 levels

   Values and labels    N    Percent 
                                     
              1 'NS'  378   70.8     
              2 'S'   156   29.2     

===========================================================================

   married

---------------------------------------------------------------------------

   Storage mode: integer
   Factor with 2 levels

   Values and labels    N    Percent 
                                     
         1 'Married'  350   65.5     
         2 'Single'   184   34.5     

===========================================================================

   exper

---------------------------------------------------------------------------

   Storage mode: integer

          Min.:   0.000
       1st Qu.:   8.000
        Median:  15.000
          Mean:  17.822
       3rd Qu.:  26.000
          Max.:  55.000

===========================================================================

   union

---------------------------------------------------------------------------

   Storage mode: integer
   Factor with 2 levels

   Values and labels    N    Percent 
                                     
           1 'Not'    438   82.0     
           2 'Union'   96   18.0     

===========================================================================

   age

---------------------------------------------------------------------------

   Storage mode: integer

          Min.:  18.000
       1st Qu.:  28.000
        Median:  35.000
          Mean:  36.833
       3rd Qu.:  44.000
          Max.:  64.000

===========================================================================

   sector

---------------------------------------------------------------------------

   Storage mode: integer
   Factor with 8 levels

   Values and labels    N    Percent 
                                     
        1 'clerical'   97   18.2     
        2 'const'      20    3.7     
        3 'manag'      55   10.3     
        4 'manuf'      68   12.7     
        5 'other'      68   12.7     
        6 'prof'      105   19.7     
        7 'sales'      38    7.1     
        8 'service'    83   15.5     


# Lösungen {-}

## Aufgabe_1 {-}


```r
  IncomeNew     <- CPS85$wage
  ID            <- sample(1:534, 50)
  IncomeNew[ID] <- IncomeNew[ID] + 180
  
  hist(IncomeNew)
  # DT::datatable(data.frame(stat.desc(IncomeNew)))
  mean(IncomeNew, trim = .0, na.rm = TRUE)
  mean(IncomeNew, trim = .1, na.rm = TRUE)
```

[zurück zur Aufgabenstellung](#aufgabenstellung-1)
