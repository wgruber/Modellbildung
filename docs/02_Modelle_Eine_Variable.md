

# (PART\*) Teil II: Modelle mit einer Variablen {-}



# Datensatz {-}

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

Unter bestimmten Voraussetzungen, eignet sich der Mittelwert als bester Schätzer (bzw. als einfachste Modellvorstellung). Bevor man sich jedoch der Auswertung von Daten widmet, ist es sehr empfehlenswert die zugrundeliegende Datenstruktur zu analysieren und auch zu dokumentieren. Im nachfolgenden Kapitel wird ein sehr nützliches Paket für genau diese Analyse kurz vorgestellt.

## Codebooks in R {-}

In R hat man die Möglichkeit, mit Hilfe des Pakets *codebook* eine genaue Beschreibung der Daten (inklusive einer deskriptiven Statistik für jede Variable) zu erstellen. Für den vorliegenden Datensatz wurde auszugsweise eines erstellt, welches in Kapitel [Codebook CPS85](#codebook-cps85) zu finden ist.

### Tabellen {-}

Im Codebook werden neben den deskriptiven Kennwerten (für kategorielle Variablen) Häufigkeitstabellen angegeben. Wir wollen uns daher einen kurzen Überblick über Häufigkeitstabellen in R verschaffen. Kopiere den nachfolgenden Code in den Editor und führe in aus. Diskutiere die Ergebnisse.


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
  # HÃ¤ufigkeitstabellen in Prozent
  x1 <- addmargins(round(100*prop.table(table(CPS85$sex, CPS85$race)), 2))
  kable(x1)
```

# Mittelwerts-Modell {-}

Wie bereits erwähnt, wäre unter bestimmten Voraussetzungen (Verteilungseigenschaften) der Mittelwert ein guter Schätzer, da dieser die folgende Eigenschaft besitzt:

* Die Summe der quadrierten Abweichungen der Beobachtungswerte $x_i$ von einem beliebigen Punkt $m$ wird minimal, wenn dieser Punkt $m = \bar{x}$, also der arithmetische Mittelwert ist!

Formal berechnet sich das arithmetische Mittel:

\begin{equation} 
  \bar{x} = \frac{1}{N} \sum_{i=1}^{N} x_i
  (\#eq:MW)
\end{equation} 

Die Aussagekraft des arithmetischen Mittels beschränkt sich jedoch ganz wesentlich, wenn nicht weitere Kennwerte der Daten bekannt sind. Vor allem ist es von Interesse, die Streung (Variabilität) der Werte um den Mittelwert zu kennen. Diese wird durch das Streuungsmaß, welches als durchschnittliche Abweichung der Messwerte um den Mittelwert gesehen werden kann, beschrieben:

\begin{equation} 
  s = \sqrt{\sum_{i=1}^{N} (x_i \frac{x_i - \bar{x})^2}{N-1}}
  (\#eq:SD)
\end{equation} 

## Modell *idealer* Daten {-}

Betrachten wir zunächst einen Datensatz, in dem das Gehalt (*wage*) symmetrisch und in Form einer Glockenkurve gegeben ist. Kopiere den nachfolgenden Code in dein R-Script und führe diesen dann aus.


```r
  options(digits = 2)
  DF      <- CPS85
  set.seed(825)
  DF$wage <- rnorm(n = nrow(DF), mean = 8, sd = 2.3)
  Income  <- DF$wage
  
  # Kennwerte berechnen
  MW <- mean(Income)
  SD <- sd(Income)
  MD <- median(Income)
  RA <- range(Income)
  # Daten anzeigen
  # p1 <- hist(Income)
  # p2 <- boxplot(Income)
  
  # starke Abweichungen entfernen
  TrimmedIncome <- Income[!Income %in% boxplot.stats(Income)$out]
  # Kennwerte berechnen
  MW_T <- mean(TrimmedIncome)
  SD_T <- sd(TrimmedIncome)
  MD_T <- median(TrimmedIncome)
  RA_T <- range(TrimmedIncome)
  # Daten anzeigen
  # p3   <- hist(TrimmedIncome)
  # p4   <- boxplot(TrimmedIncome)
```

Die Ergebnisse der statistischen Kennwerte $\bar{x}$ = (8.0952214), $med$ = (8.2289139), $sd$ = (2.3218623) und vor allem (das hier nicht angezeigte) angezeigte Histogramm lassen vermuten, dass der Mittelwert als *Modell* durchaus geeignet ist. Vor allem wenn man noch durch *Beschneidung (trim)* der Daten die kleinsten und größten Werte entfernt, nehmen der Mittelwert $\bar{x}_{trim}$ =  8.1089335 und Median $med_{trim}$ = 8.2306598 den gleichen Wert ein.

## Modell *schiefer* Daten {-}

Um die Eigenschaften des Mittelwertes bei vorliegen von starken Abweichungen in den Daten noch besser zu verdeutlichen, verwenden wir einerseits die Originaldaten (welche für sich schon schiefverteilt sind) und setzen zusätzlich bei 50 zufällig gewählten Personen das Einkommen drastisch hinauf. Kopiere den folgenden Code ins RStudio und führe diesen dann aus.


```r
  IncomeNew     <- CPS85$wage
  ID            <- sample(1:534, 50)
  IncomeNew[ID] <- IncomeNew[ID] + 18
```

### Aufgabenstellung 1 {-}

Berechne für die neuen Daten folgende Kennwerte und zeichne sowohl ein Histogramm, als auch einen Boxplot. 

* Mittelwert
* Standardabweichung
* Median
* Range
* Getrimmten Mittelwert, wobei jeweils 10% der Daten vom unteren und oberen Wertebereich unberücksichtigt bleiben sollen.

Diskutiere die Ergebnisse. Die Lösung zu diesen Aufgaben findest du in [Lösung Aufgabe 1](#aufgabe_1).

### Graphische Darstellung {-}

Zur Veranschaulichung von Verteilungseigenschaften einer Variablen eignen sich vor allem Histogramme, Boxplots und Q-Q-Plots. In Kombination mit den entsprechenden Tabellen, können bereits durch die einfache deskriptive Statistik wertvolle Aussagen über die statistischen Eigenschaften der Daten gewonnen werden. Kopiere den folgenden Code ins RStudio und führe diesen dann aus. Diskutiere die Ergebnisse.


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

### Bemerkung Ausreißer {-}

Eine der häufigsten Ursachen für Verzerrungen in den Verteilungseigenschaften einer Variablen sind Ausreißer. Die Behandlung von Ausreißern ist ein eigenes und heftig diskutiertes Thema in der Statistik. Eine (wenngleich nicht unbedenkliche) Methode ist das bereits verwendete *Trimmen* der Daten. Nachfolgendes Beispiel zeigt eine weitere Möglichkeit[^3], Ausreißer aus einer Analyse zu entfernen. Es sei an dieser Stelle nochmals explizit darauf hingewiesen, dass ein beliebiges Weglassen von *störenden* Werten durchaus bedenklich ist und eigentlich nur im Sinne einer explorativen Analyse von Daten (was wäre, wenn die Daten keine Ausreißer hätten?) gerechtfertigt werden kann! Kopiere den folgenden Code ins RStudio und führe diesen dann aus. Diskutiere die Ergebnisse.

[^3]: wir haben bereits bei der Mittelwertsfunktion *mean()* das Argument *trim* kennengelernt. 



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

Der Standardfehler (englisch: standard error, meist $SE$ abgekürzt) ist die Standardabweichung der Stichprobenkennwertverteilung einer Stichprobenfunktion. In der Regel bezieht sich der Standardfehler dabei auf den Mittelwert und wird meistens dann als *standard error of the mean* ($SEM$ abgekürzt) bezeichnet.

### Erläuterung zum $SE$ {-}

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

Die Intervallschätzung zielt nun darauf ab, einen Bereich anzugeben, der mit einer gewissen (von der Forscherin gewählten) Wahrscheinlichkeit den wahren Wert enthält (überdeckt). Dieser Bereich heißt [*Konfidenzintervall*](https://de.wikipedia.org/wiki/Konfidenzintervall){target="_blank"}. Die Wahrscheinlichkeit, mit der das Intervall den wahren Wert enthält, sollte in der Regel möglichst hoch sein. Der trade-off: Je größer die gewählte Wahrscheinlichkeit, desto breiter das resultierende Intervall.

Das Konfidenzintervall berechnet sich aus:

\begin{equation} 
  KI = \bar{x} \pm SE \cdot t_{1 - \frac{\alpha}{2}; n - 1}
  (\#eq:KI)
\end{equation} 

Die Eigenschaften des Konfidenzintervalls lassen sich sehr schön in einer Simulation von [Geoff Cumming](https://thenewstatistics.com/itns/esci/) veranschaulichen.

[^5]: siehe [Prof. Dr. Wolfgang Ludwig-Mayerhofer, Uni Siegen, Punkt- und Intervallschätzungen ](https://www.uni-siegen.de/phil/sozialwissenschaften/soziologie/mitarbeiter/ludwig-mayerhofer/statistik/statistik_downloads/statistik_ii_4.pdf){target="_blank"}, oder [Springer](https://link.springer.com/content/pdf/10.1007/978-3-642-41995-9_8.pdf){target="_blank"}

# Codebook CPS85 {-}

Das nachfolgende [Codebook](#codebooks-in-r) zeigt die Datenstruktur des Datensatzes *CPS85*.

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
  set.seed(21430)
  ID            <- sample(1:534, 50)
  IncomeNew[ID] <- IncomeNew[ID] + 180

  # Kennwerte berechnen
  MW_A1         <- mean(IncomeNew)
  SD_A1         <- sd(IncomeNew)
  MD_A1         <- median(IncomeNew)
  RA_A1         <- range(IncomeNew)
  MW_A1_Trimmed <- mean(IncomeNew, trim = .1)
  
  # Daten anzeigen
  # p5 <- hist(IncomeNew)
  # p6 <- boxplot(IncomeNew)
```

[zurück zur Aufgabenstellung](#aufgabenstellung-1)
