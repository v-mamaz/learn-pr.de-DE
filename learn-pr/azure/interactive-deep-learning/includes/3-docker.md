## <a name="docker"></a>Docker

![Docker-Logo](../media/3-image1.PNG)

Docker ermöglicht es Entwicklern, beliebige Anwendungen auf einfache Weise als schlanken, portablen, selbstgenügsamen Container zu packen, versenden und auszuführen, der praktisch überall ausgeführt werden kann. Wenn das DSVM-Basisimage die beliebtesten Deep Learning-Frameworks bereits vorinstalliert enthält, warum gibt es dann einen Bedarf an Containerisierungsclients wie Docker?

Bei dem Versuch, Deep Learning-Aufgaben auszuführen, sehen sich Entwickler häufig alptraumhaften Szenarien hinsichtlich der Abhängigkeiten gegenüber, wie etwa diesen: 

- Das Erfordernis zum Erstellen benutzerdefinierter Pakete – Deep Learning-Forscher denken tendenziell eher wenig an die Produktion wenn sie Code auf Git Hub veröffentlichen. Wenn sie ein Paket in ihrer eigenen Entwicklungsumgebung ausführungsbereit bekommen, nehmen sie oft einfach an, dass das anderen genauso gelingen wird.
- Verwaltung von GPU-Treiberversionen – CUDA ist eine parallele Computingplattform und Anwendungsprogrammierschnittstelle (API), die von Nvidia entwickelt wurde. Sie ermöglicht Softwareentwicklern und Softwaretechnikern die Verwendung einer CUDA-fähigen GPU (Graphics Processing Unit, Grafikprozessor) für allgemeine Computingzwecke. Bestimmte Versionen von Tensorflow funktionieren nicht mit CUDA-Versionen über 9.1, aber andere Frameworks, wie z.B. PyTorch, scheinen mit höheren Versionen von CUDA eine bessere Leistung zu erreichen.

Um diese Probleme zu umgehen und die Benutzerfreundlichkeit des Codes zu erhöhen, können Sie Docker oder dessen GPU-Variante Nvidia-Docker verwenden, um Deep Learning-Projekte zu verwalten und auszuführen. 

<!--Quiz 
What is CUDA? 
What versioning issues do deep learning engineers deal with? -->