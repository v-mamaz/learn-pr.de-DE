Die **Data Science Virtual Machine** für Linux ist das Image eines virtuellen Computers, das Ihnen den Einstieg in Data Science erleichtert. Dabei sind zahlreiche Tools bereits erstellt, installiert und konfiguriert, damit Sie so schnell wie möglich beginnen können. Der NVIDIA-GPU-Treiber, NVIDIA CUDA und die NVIDIA CUDA Deep Neural Network-Bibliothek (cuDNN) sind ebenso enthalten wie Jupyter und TensorFlow. Alle vorinstallierten Frameworks sind sowohl GPU- als auch CPU-fähig.

## <a name="what-is-covered-in-this-lab"></a>Welche Themen werden in dieser Übungseinheit behandelt?

 Diese Übungseinheit deckt Folgendes ab:
* Erstellen einer Data Science Virtual Machine für Linux in Azure
* Herstellen einer Verbindung mit der DSVM über Remotedesktop
* Trainieren eines TensorFlow-Modells zum Klassifizieren von Bildern in solche, die Hotdogs enthalten und solche, die keine Hotdogs enthalten
* Verwenden des Modells in einer Python-App

Für diese Übung benötigen Sie ein Azure-Abonnement und einen Xfce-Remotedesktopclient. Ausführlichere Informationen hierzu finden Sie im Abschnitt „Voraussetzungen“. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.

### <a name="prerequisites-for-the-lab"></a>Voraussetzungen für diese Übungseinheit

 1. Ein **Microsoft Azure-Konto**: Für diese Übung benötigen Sie ein gültiges und aktives Azure-Konto. Wenn Sie kein Konto haben, können Sie sich für eine [kostenlose Testversion](https://azure.microsoft.com/en-us/free/) registrieren.

    * Wenn Sie ein Visual Studio Active-Abonnement besitzen, können Sie eine monatliche Gutschrift von 50–150 US-Dollar in Anspruch nehmen. Weitere Informationen finden Sie unter diesem [Link](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/). Hier erfahren Sie auch, wie Sie Ihre monatliche Azure-Gutschrift aktivieren und nutzen können.

    * Wenn Sie kein Visual Studio-Abonnement besitzen, können Sie sich für ein KOSTENLOSES [Visual Studio Dev Essentials](https://www.visualstudio.com/dev-essentials/)-Programm registrieren, um ein **kostenloses Azure-Konto** zu erstellen (einschließlich kostenlose Dienste für 1 Jahr, 200 US-Dollar im 1. Monat).

    * Schüler und Studenten können sich für ein [kostenloses Azure for Students-Konto](https://aka.ms/azure4students) registrieren, mit dem Sie eine kostenlose Azure-Gutschrift von 100 US-Dollar und ein Jahr kostenlose Dienste erhalten (keine Kreditkarte erforderlich). 

1. Einen [Xfce](https://xfce.org/)-Remotedesktopclient, z.B. [X2Go](https://wiki.x2go.org/doku.php/download:start)