## <a name="intro-to-deep-learning"></a>Einführung in Deep Learning

Das Ziel von Machine Learning (ML) besteht darin, Merkmale zu finden, mit denen ein Modell trainiert werden kann, um Eingabedaten (etwa Bild-, Zeitreihen- oder Audiodaten) in eine bestimmte Ausgabe (etwa Untertitel, Preiswerte oder Transkriptionen) umzuwandeln. Bei herkömmlicher Data Science werden die Merkmale häufig von Hand ausgewählt.

![Canonical-Beispiel eines Deep Neural Network mit Feed Forward.](../media/2-image1.PNG)

Bei Deep Learning (DL) basiert die Extraktion von Merkmalen auf einem Lernprozess. Dabei werden Eingaben als Vektoren dargestellt und mithilfe einiger intelligenter Algebra-Operationen in eine bestimmte Ausgabe umgewandelt.  

Die Ausgabe des Modells wird dann unter Verwendung einer Gleichung (Verlustfunktion) mit der erwarteten Ausgabe abgeglichen. Der Wert, der von der Verlustfunktion für jede Trainingseingabe zurückgegeben wird, dient zur Optimierung des Modells, sodass beim nächsten Mal Merkmale mit einem geringeren Verlustwert extrahiert werden können.  
 
Die Matrixoperationen, die im Rahmen der linearen Algebra-Komponente ausgeführt werden, sind häufig sehr rechenintensiv und stark parallelisierbar. Für eine effiziente Berechnung werden daher spezielle Prozessoren (beispielsweise GPUs) benötigt.

## <a name="data-science-virtual-machine"></a>Data Science Virtual Machine

![DSVM-Optionen](../media/2-image2.PNG)

DSVM-Instanzen sind Images für virtuelle Azure-Computer, die mit verschiedenen beliebten Tools vorinstalliert, konfiguriert und getestet wurden. Diese Images werden häufig in den Bereichen Datenanalyse, maschinelles Lernen und Deep Learning-Training eingesetzt.

Sie bieten Folgendes:

- Konsistente Einrichtung im gesamten Team, Förderung von Freigabe und Zusammenarbeit, Azure-Skalierung und -Verwaltung, so gut wie kein Einrichtungsaufwand, vollständig cloudbasierter Desktop für Data Science.
- Flexible Kapazität bei Bedarf: Möglichkeit zum Ausführen von Analysen für sämtliche Azure-Hardwarekonfigurationen mit vertikaler und horizontaler Skalierung. Nutzungsbasiertes Zahlungsmodell.
- Deep Learning mit GPUs: Sofort verfügbare GPU-Cluster mit bereits vorkonfigurierten Deep Learning-Tools. 

DSVM enthält mehrere KI-Tools. Dazu zählen unter anderem GPU-Editionen beliebter Deep Learning-Frameworks und -Tools wie Microsoft R Server Developer Edition, Anaconda Python, Jupyter-Notebooks für Python und R, IDEs für Python und R, SQL-Datenbank und viele andere Data Science- und ML-Tools.

DSVM kann in Azure VM-Instanzen mit GPU der NC-Serie ausgeführt werden. Dank diskreter Gerätezuordnung erzielen diese GPUs eine mit Bare-Metal-Hardware vergleichbare Leistung und eignen sich somit perfekt für Deep Learning-Aufgaben.

<!--### Quiz? 

What is the goal of machine learning? 
How is traditional machine learning different from deep learning? 
Why are GPU's often used for deep learning? 
What does the DSVM provide? -->
