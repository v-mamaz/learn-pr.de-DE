Das Erfassen von Wetterdaten ist eine wichtige Aufgabe, weil das Wetter vieles beeinflusst – von Verkehrsmustern bis hin zum Betrieb von Heizungs-, Lüftungs- und Klimasystemen im Einzelhandel. In dieser Übung verwenden Sie den Raspberry Pi-Onlinesimulator, um simulierte Wetterdaten zu erfassen und diese Daten über Azure IoT Hub zu speichern.

Wenngleich diese Übung in einer simulierten Umgebung durchgeführt wird, kann die auf dem simulierten Gerät ausgeführte Anwendung später auf ein echtes Gerät übertragen werden.

## <a name="create-an-iot-hub"></a>Erstellen eines IoT Hubs

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/) an.

1. Wählen Sie **Ressource erstellen**\>**Internet der Dinge (IoT)**\>**IoT Hub** aus.

![Screenshot der Navigation zu IoT Hub im Azure-Portal](../media-draft/fa40d1bc51bc4490f657e3c1a8371b5b.png)

1. Geben Sie im Bereich **IoT Hub** die folgenden Informationen für Ihren IoT Hub ein:

 - **Abonnement**: Wählen Sie das Abonnement aus, das Sie zum Erstellen dieses IoT-Hubs verwenden möchten.
 - **Ressourcengruppe**: Erstellen Sie eine Ressourcengruppe zum Hosten des IoT Hubs, oder verwenden Sie eine vorhandene Ressourcengruppe. Weitere Informationen finden Sie unter [Verwenden von Ressourcengruppen zum Verwalten von Azure-Ressourcen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).
 - **Region**: Wählen Sie den nächstgelegenen Standort aus.
 - **Name**: Erstellen Sie einen Namen für Ihren IoT-Hub. Wenn der eingegebene Name verfügbar ist, wird ein grünes Häkchen angezeigt.

> [!IMPORTANT]
> Der IoT Hub wird öffentlich als DNS-Endpunkt ermittelbar sein, sodass Sie beim Benennen die Verwendung von sensiblen Informationen vermeiden sollten.

   ![Fenster mit IoT Hub-Grundeinstellungen](./../media-draft/dbb7319388673b8ee0e0b407536156c0.png)

1.  Klicken Sie auf **Nächster Schritt: Größe festlegen und skalieren**, um die Erstellung Ihres IoT-Hubs fortzusetzen.

1.  Wählen Sie eine Option für **Tarif und Skalierung** aus. Legen Sie für diesen Artikel den Tarif **F1 – Free** fest, wenn er für Ihr Abonnement noch verfügbar ist. Weitere Informationen hierzu finden Sie unter [Tarif und Skalierung](https://azure.microsoft.com/pricing/details/iot-hub/).

   ![Fenster für IoT Hub-Größe und -Skalierung](../media-draft/b506eb3293fa4aa9d4785ad498fc476c.png)

1.  Klicken Sie auf **Überprüfen + erstellen**.

1.  Überprüfen Sie die Informationen zum IoT-Hub, und klicken Sie auf **Erstellen**. Die Erstellung des IoT Hubs kann mehrere Minuten dauern. Sie können den Fortschritt im Bereich **Benachrichtigungen** überwachen.

Nachdem Sie nun einen IoT Hub erstellt haben, können Sie nach den wichtigen Informationen suchen, die Sie zum Herstellen einer Verbindung für Geräte und Anwendungen mit Ihrem IoT Hub nutzen.

Öffnen Sie in Ihrem IoT Hub-Navigationsmenü die Option  **	Richtlinien für gemeinsamen Zugriff**. Wählen Sie die Richtlinie **iothubowner** aus, und kopieren Sie die **Verbindungszeichenfolge – Primärschlüssel** Ihres IoT Hub. Weitere Informationen finden Sie unter [Verwalten des Zugriffs auf IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security).

> [!NOTE]
> Die Verbindungszeichenfolge „iothubowner“ wird für dieses Tutorial nicht benötigt. Sie benötigen sie allerdings unter Umständen für einige Tutorials oder andere IoT-Szenarios, nachdem Sie diese Einrichtung abgeschlossen haben.

![Abrufen der IoT Hub-Verbindungszeichenfolge](../media-draft/a4b41e6ea46ccbef653c411a9829610c.png)

## <a name="register-a-device-in-the-iot-hub-for-your-device"></a>Registrieren eines Geräts beim IoT Hub für Ihr Gerät
------------------------------------------------

1.  Öffnen Sie in Ihrem IoT Hub-Navigationsmenü die Option **IoT-Geräte**, und klicken Sie auf **Hinzufügen**, um ein Gerät in Ihrem IoT Hub zu registrieren.

   ![Hinzufügen eines Geräts im Bereich „IoT-Geräte“ Ihres IoT Hubs](../media-draft/ee5f177abcf06b86dd007fce3b8448ad.png)

1.  Geben Sie eine **Geräte-ID** für das neue Gerät ein. Bei Geräte-IDs wird die Groß-/Kleinschreibung beachtet.

> [!IMPORTANT]
> Diese Geräte-ID ist unter Umständen in den Protokollen sichtbar, die für den Kundensupport und die Problembehandlung erfasst werden. Stellen Sie also sicher, dass Sie beim Benennen keine sensiblen Informationen verwenden.

1.  Klicken Sie auf **Speichern**.

1.  Öffnen Sie das Gerät nach der Erstellung in der Liste im Bereich **IoT-Geräte**.

1.  Kopieren Sie **Verbindungszeichenfolge – Primärschlüssel** zur späteren Verwendung.

   ![Abrufen der Geräte-Verbindungszeichenfolge](../media-draft/fba4413dcb652be92a6ab0f6bb638561.png)

## <a name="run-a-sample-application-on-pi-web-simulator"></a>Ausführen einer Beispielanwendung im Pi-Websimulator

1. Stellen Sie im Codingbereich sicher, dass Sie mit der Standard-Beispielanwendung arbeiten. Ersetzen Sie den Platzhalter in Zeile 15 durch die Verbindungszeichenfolge für das Azure IoT Hub-Gerät.

    ![Ersetzen der Verbindungszeichenfolge für das Gerät](../media-draft/92ea2c31d42f5b939fb5512e7220e957.png)

2.  Klicken Sie auf **Ausführen**, oder geben Sie „npm start“ ein, um die Anwendung auszuführen.

Sie sollten die folgende Ausgabe sehen, die die Sensordaten und Nachrichten zeigt, die an Ihren IoT Hub gesendet werden.

   ![Ausgabe: Von Raspberry Pi an Ihren IoT Hub gesendete Sensordaten](../media-draft/96b28d30e317b04347abb0d613738117.png)

<!--Reference links
https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started-->
