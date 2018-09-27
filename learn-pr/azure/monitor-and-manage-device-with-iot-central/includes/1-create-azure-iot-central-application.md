Azure IoT Central ist eine vollständig verwaltete IoT-Lösung, mit der Sie Ihre globalen IoT-Ressourcen einfach vernetzen, überwachen und verwalten können.

Hier folgen Sie dem Szenario, in dem eine Remotekaffeemaschine zur Überwachung und Problembewältigung mit Azure IoT Central verbunden ist. Sie können Telemetriedaten wie Wassertemperatur und Luftfeuchtigkeit überwachen, den Zustand der Maschine beobachten, die optimale Temperatur festlegen, den Garantiestatus abfragen und Befehle senden. Liegt die Wassertemperatur nach Ablauf der Garantie außerhalb des erwarteten Bereichs, wird von IoT Central eine E-Mail an die entsprechende Wartungsabteilung des Kunden gesendet, damit diese entsprechende Maßnahmen ergreifen kann.

Sie beginnen mit der Erstellung eines Geräts in Azure IoT Central, das die Daten und Befehle definiert, die mit dem IoT-Gerät ausgetauscht werden können.

In diesem Modul lernen Sie Folgendes:
  - Erstellen einer benutzerdefinierten Azure IoT Central-Anwendung
  - Erstellen und Definieren Ihrer Gerätevorlage
  - Verbinden eines Kaffeemaschinensimulators mit Ihrer Anwendung in Azure IoT Central
  - Überprüfen der Verbindung und des Datenflusses
  - Konfigurieren von Regeln für Wartungsbenachrichtigungen
 
## <a name="sign-in-to-azure-iot-central"></a>Anmelden bei Azure IoT Central
In dieser Einheit melden Sie sich bei IoT Central an, um eine neue benutzerdefinierte Anwendung zu erstellen. Eine sieben Tage kostenlose Testversion ist für dieses Modul ausreichend. 

1. Navigieren Sie zur Azure IoT Central-Seite [Anwendungs-Manager](https://aka.ms/iotcentral?azure-portal=true). 

1. Geben Sie auf der Anmeldeseite die E-Mail-Adresse und das Kennwort für den Zugriff auf Ihr Microsoft-Konto ein.

## <a name="create-a-new-custom-application"></a>Erstellen einer neuen benutzerdefinierten Anwendung

1. Klicken Sie auf **Neue Anwendung**, um eine neue Azure IoT Central-Anwendung zu erstellen. 

1. Gehen Sie auf der Seite **Anwendung erstellen** so vor: 
    * Wählen Sie den Zahlungsplan **Free** aus.
    * Wählen Sie die Anwendungsvorlage **Benutzerdefinierte Anwendung** aus.
    * Legen Sie einen Anzeigenamen für die Anwendung (beispielsweise **Coffee Maker 01-A**) fest.
    * (Optional) Bearbeiten Sie die URL. Dies ist erforderlich, wenn der von Ihnen gewählte Name bereits verwendet wird.
    * Klicken Sie auf **Erstellen**.