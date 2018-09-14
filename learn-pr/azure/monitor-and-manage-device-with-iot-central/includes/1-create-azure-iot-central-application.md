 In diesem Tutorial führen Sie das Szenario, in dem ein remote Kaffeemaschine für Überwachung und Verwaltung von Problemen mit Azure IoT Central verbunden ist. Sie können Telemetriedaten wie Anzahl der Wasser Temperatur- und luftfeuchtigkeitsdaten zu überwachen, beobachten Sie den Zustand des Computers, legen Sie optimale Temperatur, Garantiestatus empfangen und Senden von Befehlen. Wenn die Wassertemperatur der Kaffeemaschine innerhalb des Garantiezeitraums bestimmte Schwellenwerte übersteigt, sendet Microsoft Flow eine Mobiltelefonbenachrichtigung an das Mobilgerät eines Remotetechnikers. Liegt die Wassertemperatur nach Ablauf der Garantie außerhalb des erwarteten Bereichs, wird von IoT Central eine E-Mail an die entsprechende Wartungsabteilung des Kunden gesendet, damit diese entsprechende Maßnahmen ergreifen kann.

Um das Szenario zu implementieren, zunächst erstellen Sie eine Gerätevorlage im Azure IoT Central um Messungen (Telemetrie- und Statusdaten), Einstellungen, Eigenschaften und Befehle zu definieren. Anschließend verbinden Sie Ihre Kaffeemaschine mit Azure IoT Central und konfigurieren Regeln für Wartungsbenachrichtigungen, wenn die Wassertemperatur außerhalb des optimalen Bereichs liegt.

In diesem Modul werden Sie zu:
- Erstellen einer benutzerdefinierten Azure IoT Central-Anwendung 
- Erstellen und Definieren Ihrer Gerätevorlage
- Herstellen einer Verbindung der Anwendung mit Ihren Kaffee-Computer
- Überprüfen der Verbindung und des Datenflusses
- Konfigurieren von Regeln für Wartungsbenachrichtigungen
 
## <a name="sign-in-to-azure-iot-central"></a>Anmelden bei Azure IoT Central
In dieser Einheit melden Sie IoT Central um eine neue benutzerdefinierte Anwendung zu erstellen. Eine 7-Tage-Testversion ist ausreichend Einheiten 1 – 4 ausführen. Wenn Sie die optionale Übung zur Verwendung von Microsoft Flow zum Senden einer benachrichtigungs auf Ihrem Mobilgerät Einheit 5 abschließen möchten, müssen Sie Verlängerung des Testzeitraums IoT Central auf 30 Tage. Die Erweiterung wird aktiviert, wenn Sie ein Azure-Abonnement verfügen.  

1. Navigieren Sie zur Azure IoT Central-Seite [Application Manager](https://aka.ms/iotcentral) (Anwendungs-Manager). 

1. Geben Sie auf der Anmeldeseite angezeigt den e-Mail-Adresse und das Kennwort, mit denen Sie Zugriff auf Ihr Microsoft-Konto ein.

## <a name="create-a-new-custom-application"></a>Erstellen einer neuen benutzerdefinierten Anwendung

1. Wählen Sie zum Erstellen einer neuen Azure IoT Central-Anwendung **neue Anwendung**. 

1. Auf der Seite für die Anwendung zu erstellen: 
    * Wählen Sie **Free** für den Zahlungsplan
    * Wählen Sie **benutzerdefinierte Anwendung** wie die Application-Vorlage
    * Wählen Sie einen benutzerfreundlichen Anwendungsnamen, z. B. **Kaffeemaschine 01**
    * Azure IoT Central generiert ein eindeutige URL-Präfix für Sie wählen **erstellen**
    
   > [!NOTE]
   > Erweitern Ihre auf 30-Tage-Testversion ist optional, aber es ist eine Voraussetzung, wenn Sie die Übung zur Verwendung von Microsoft Flow zum Senden einer benachrichtigungs auf Ihrem Mobilgerät Einheit 5 abschließen möchten. Die 30-Tage-Erweiterung ist aktiviert, wenn Sie ein Azure-Abonnement verfügen. Anweisungen zum Aktivieren der Erweiterungs finden Sie zum Konfigurieren von Regeln und Aktionen zum Überwachen Ihrer Kaffeemaschine Einheit 5.

In dieser Einheit haben Sie eine benutzerdefinierte Azure-IoT-Anwendung erstellt. Möglicherweise haben Sie sich auch für ein Azure-Abonnement registriert. In der nächsten Einheit werden Sie weiterhin auf das Anwendungsframework erstellen, die Sie erstellt haben. 