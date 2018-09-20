![Docker-Logo](../media/3-image1.PNG)

Mit dem Docker-Tool können Sie Ihre Anwendungen in einer Sandbox bereitstellen und unter einem Hostbetriebssystem Ihrer Wahl ausführen. Sie können eine standardisierte Einheit erstellen, die Ihre App und alle dazugehörigen Abhängigkeiten enthält. Aber warum sollten Sie überhaupt Docker verwenden, wenn im DSVM-Basisimage bereits die beliebtesten Deep Learning-Frameworks vorinstalliert sind?

Beim Ausführen von Deep Learning-Aufgaben werden Entwickler häufig mit Abhängigkeitsproblemen konfrontiert. Beispiele: 

- Erstellung benutzerdefinierter Pakete: Deep Learning-Forscher machen sich in der Regel wenig Gedanken über die Produktion, wenn sie Code auf GitHub veröffentlichen. Nachdem das Paket in ihrer eigenen Entwicklungsumgebung funktioniert, gehen sie häufig davon aus, dass andere das Paket ebenso verwenden können.
- Verwaltung von GPU-Treiberversionen: CUDA ist eine von NVIDIA entwickelte Plattform und Anwendungsprogrammierschnittstelle (API) für paralleles Computing. Sie ermöglicht Entwicklern die Verwendung einer CUDA-fähigen GPU (Graphics Processing Unit, Grafikprozessor) für die allgemeine Verarbeitung. Bestimmte Versionen von Tensorflow sind mit CUDA-Versionen über 9.1 nicht kompatibel. Andere Frameworks (etwa PyTorch) scheinen mit höheren CUDA-Versionen besser zu funktionieren.

Um diese Probleme zu umgehen und die Nutzbarkeit des Codes zu verbessern, können Sie Docker oder dessen GPU-Variante NVIDIA Docker für die Verwaltung und Ausführung von Deep Learning-Projekten verwenden. 

<!--Quiz 
What is CUDA? 
What versioning issues do deep learning engineers deal with? -->