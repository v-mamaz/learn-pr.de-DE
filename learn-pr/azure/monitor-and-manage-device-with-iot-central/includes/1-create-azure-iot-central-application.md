 Dieses Tutorial basiert auf dem Szenario, in dem eine Remote-Kaffeemaschine zur Überwachung und Problembewältigung mit Azure IoT Central verbunden ist. Sie können Telemetriedaten wie Wassertemperatur und Luftfeuchtigkeit überwachen, den Zustand der Maschine beobachten, die optimale Temperatur festlegen, den Garantiestatus abfragen und Befehle senden. Wenn die Wassertemperatur der Kaffeemaschine innerhalb des Garantiezeitraums bestimmte Schwellenwerte übersteigt, sendet Microsoft Flow eine Mobiltelefonbenachrichtigung an das Mobilgerät eines Remotetechnikers. Liegt die Wassertemperatur nach Ablauf der Garantie außerhalb des erwarteten Bereichs, wird von IoT Central eine E-Mail an die entsprechende Wartungsabteilung des Kunden gesendet, damit diese entsprechende Maßnahmen ergreifen kann.

Zur Implementierung des Szenarios erstellen Sie zunächst eine Gerätevorlage im Azure IoT Central, um Messungen (Telemetrie- und Zustandsdaten), Einstellungen, Eigenschaften und Befehle zu definieren. Anschließend verbinden Sie Ihre Kaffeemaschine mit Azure IoT Central und konfigurieren Regeln für Wartungsbenachrichtigungen, wenn die Wassertemperatur außerhalb des optimalen Bereichs liegt.

In diesem Modul führen Sie die folgenden Aufgaben aus:
- Erstellen einer benutzerdefinierten Azure IoT Central-Anwendung 
- Erstellen und Definieren Ihrer Gerätevorlage
- Verbinden Ihrer Kaffeemaschine mit der Anwendung
- Überprüfen der Verbindung und des Datenflusses
- Konfigurieren von Regeln für Wartungsbenachrichtigungen
 
## <a name="sign-in-to-azure-iot-central"></a>Anmelden bei Azure IoT Central
In dieser Einheit melden Sie sich bei IoT Central an, um eine neue benutzerdefinierte Anwendung zu erstellen. Eine 7 Tage kostenlose Testversion ist für die Einheiten 1-4 ausreichend. Wenn Sie die Übung zum Versenden einer SMS-Benachrichtigung mit Microsoft Flow in Einheit 5 absolvieren möchten, müssen Sie die IoT Central-Testversion auf 30 Tage verlängern. Die Verlängerung wird aktiviert, wenn Sie ein Azure-Abonnement haben.  

1. Navigieren Sie zur Azure IoT Central-Seite [Anwendungs-Manager](https://aka.ms/iotcentral). 

1. Geben Sie auf der Anmeldeseite die E-Mail-Adresse und das Kennwort für den Zugriff auf Ihr Microsoft-Konto ein.

## <a name="create-a-new-custom-application"></a>Erstellen einer neuen benutzerdefinierten Anwendung

1. Klicken Sie auf **Neue Anwendung**, um eine neue Azure IoT Central-Anwendung zu erstellen. 

1. Gehen Sie auf der Seite „Anwendung erstellen“ so vor: 
    * Wählen Sie den Zahlungsplan **Free** aus.
    * Wählen Sie die Anwendungsvorlage **Benutzerdefinierte Anwendung** aus.
    * Wählen Sie einen Anzeigenamen für die Anwendung (beispielsweise **Coffee Maker 01**).
    * Azure IoT Central generiert automatisch ein eindeutiges URL-Präfix. Klicken Sie auf **Erstellen**.
    
   > [!NOTE]
   > Die Verlängerung des Testzeitraums auf 30 Tage ist zwar optional, wird jedoch vorausgesetzt, wenn Sie in Einheit 5 die Übung zum Verwenden von Microsoft Flow absolvieren möchten, um eine SMS-Benachrichtigung zu senden. Die 30-tägige Verlängerung wird aktiviert, wenn Sie ein Azure-Abonnement haben. Eine Anleitung zur Aktivierung der Verlängerung finden Sie in Einheit 5 zur Konfiguration von Regeln und Aktionen zur Überwachung Ihrer Kaffeemaschine.

In dieser Einheit haben Sie eine benutzerdefinierte Azure IoT-Anwendung erstellt. Möglicherweise haben Sie sich auch für ein Azure-Abonnement registriert. Die nächste Einheit baut auf dem von Ihnen erstellten Anwendungsframework auf. 