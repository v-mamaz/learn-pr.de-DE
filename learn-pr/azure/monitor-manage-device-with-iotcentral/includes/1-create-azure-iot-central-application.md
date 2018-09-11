 Dieses Tutorial basiert auf dem Szenario, in dem eine Remote-Kaffeemaschine zur Überwachung und Problembewältigung mit Azure IoT Central verbunden ist. Sie können Telemetriedaten wie Wassertemperatur und Luftfeuchtigkeit sowie den Zustand der Maschine überwachen, die optimale Temperatur festlegen, den Garantiestatus abfragen und Befehle senden, um beispielsweise den Brühvorgang zu starten. Wenn die Wassertemperatur der Kaffeemaschine innerhalb des Garantiezeitraums bestimmte Schwellenwerte übersteigt, sendet Microsoft Flow eine Mobiltelefonbenachrichtigung an das Mobilgerät eines Remotetechnikers. Liegt die Wassertemperatur nach Ablauf der Garantie außerhalb des erwarteten Bereichs, wird von IoT Central eine E-Mail an die entsprechende Wartungsabteilung des Kunden gesendet, damit diese entsprechende Maßnahmen ergreifen kann.

Zur Implementierung des Szenarios erstellen Sie zunächst eine Gerätevorlage im Azure IoT Central (eine SaaS-Lösung), um Messungen (Telemetrie- und Zustandsdaten), Einstellungen, Eigenschaften und Befehle zu definieren. Anschließend verbinden Sie Ihre Kaffeemaschine mit Azure IoT Central und konfigurieren Regeln für Wartungsbenachrichtigungen, wenn die Wassertemperatur außerhalb des optimalen Bereichs liegt.

![Datenfluss von der Maschine zu IoT Central](../images/1-data-flow.png)

In diesem Tutorial lernen Sie Folgendes:
> [!div class="checklist"]
> * Erstellen einer benutzerdefinierten Azure IoT Central-Anwendungsvorlage
> * Erstellen und Definieren Ihrer Gerätevorlage
> * Verbinden Ihrer Anwendung mit der simulierten Kaffeemaschine
> * Überprüfen der Verbindung und des Datenflusses
> * Konfigurieren von Regeln für Wartungsbenachrichtigungen
 
## <a name="sign-in-to-azure-iot-central"></a>Anmelden bei Azure IoT Central

Azure IoT Central ist eine vollständig verwaltete SaaS-Lösung (Software-as-a-Service), mit der Sie Ihre IoT-Ressourcen einfach vernetzen, überwachen und verwalten können. In diesem Modul melden Sie sich bei IoT Central an, um eine neue benutzerdefinierte Anwendung zu erstellen. Bei der Registrierung für ein Azure-Konto können Sie den Testzeitraum auf 30 Tage verlängern. Eine 30-Tage-Testversion wird für Modul 5 vorausgesetzt, wenn Sie Microsoft Flow verwenden, um eine Mobiltelefonbenachrichtigung zu senden.

1. Navigieren Sie zur Azure IoT Central-Seite [Application Manager](https://aka.ms/iotcentral) (Anwendungs-Manager). 

1. Geben Sie die E-Mail-Adresse und das Kennwort für den Zugriff auf Ihr Microsoft-Konto ein.
![Zugreifen auf Ihr Microsoft-Konto](../images/1-create-app-a.png)

## <a name="create-a-new-custom-application"></a>Erstellen einer neuen benutzerdefinierten Anwendung

1. Klicken Sie auf **Neue Anwendung**, um eine neue Azure IoT Central-Anwendung zu erstellen. 
![Erstellen einer Central-Anwendung](../images/1-create-app-b.png)

1. Erstellen Sie eine neue Azure IoT Central-Anwendung:
* Wählen Sie den Zahlungsplan **Free** aus.
* Wählen Sie die Anwendungsvorlage **Benutzerdefinierte Anwendung** aus.
* Wählen Sie einen Anzeigenamen für die Anwendung (beispielsweise **Coffee Maker 01**). 
* Azure IoT Central generiert automatisch ein eindeutiges URL-Präfix. Klicken Sie auf **Erstellen**.

![Auswählen eines Central-Anwendungsplans](../images/1-create-app-c.png)

* Die Verlängerung des Testzeitraums auf 30 Tage ist zwar optional, sie wird jedoch vorausgesetzt, wenn Sie das Modul für die Integration von Microsoft Flow absolvieren möchten, um eine Aktion zum Senden von Mobiltelefonbenachrichtigungen auszulösen. Wenn Sie den Testzeitraum auf 30 Tage verlängern möchten, wählen Sie eine Azure Active Directory-Instanz und ein Azure-Abonnement aus. Mit einem Azure-Abonnement können Sie Instanzen von Azure-Diensten erstellen. Azure IoT Central sucht automatisch nach allen Azure-Abonnements, auf die Sie Zugriff haben, und zeigt sie im Dropdownmenü an.
        
![Verlängern des Testzeitraums](../images/1-create-app-d.png)
    
* Wenn Sie kein Azure-Abonnement besitzen, können Sie auf der Seite [Azure-Registrierungsseite](https://aka.ms/createazuresubscription) ein Abonnement erstellen. Navigieren Sie nach Erstellung des Azure-Abonnements wieder zur Seite **Anwendung erstellen**. Ihr neues Abonnement wird in der Dropdownliste **Azure-Abonnement** angezeigt.
        
![Registrieren für ein Abonnement](../images/1-create-app-e.png)

## <a name="summary"></a>Zusammenfassung

In diesem Modul haben Sie eine benutzerdefinierte Azure IoT-Anwendung erstellt. Möglicherweise haben Sie sich auch für ein Azure-Abonnement registriert. Das nächste Modul baut auf dem erstellten Anwendungsframework auf. 