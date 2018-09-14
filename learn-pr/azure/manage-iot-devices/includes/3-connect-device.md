Erfassung von Wetterdaten ist eine wichtige Aufgabe, wie das Wetter beeinflussen kann alles von Mustern des Anwendungsdatenverkehrs, wie heizungs-, lüftungs- und Klimaanlagen (HVAC)-Systeme im Einzelhandel betrieben werden. In dieser Übung werden Sie mit dem Raspberry Pi-onlinesimulator interagieren, die Sie in der vorherigen Einheit zu erfassen, die simulierte Wetterdaten und über den Azure IoT Hub Informationen zu erhalten.

Während dieser Übung in einer simulierten Umgebung durchgeführt wird, kann die Anwendung ausgeführt wird, auf dem simulierten Gerät in der Zukunft ein echtes Gerät übertragen werden.

[!include[](../../../includes/azure-sandbox-activate.md)]

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

## <a name="create-an-iot-hub"></a>Erstellen eines IoT Hubs
Auf der Grundlage der Features und des Erweiterungsmodells von Azure IoT Hub können Geräte- und Back-End-Entwickler stabile Geräteverwaltungslösungen entwickeln. Das Spektrum der Geräte reicht von einfachen Sensoren und zweckgebundenen Microcontrollern bis hin zu leistungsfähigen Gateways zur Weiterleitung der Kommunikation für Gerätegruppen. Die Anwendungsfälle und Anforderungen für IoT-Betreiber sind außerdem sehr branchenspezifisch. Trotz dieser Vielfalt bietet die Geräteverwaltung mit Azure IoT Hub Funktionen, Muster und Codebibliotheken für unterschiedlichste Geräte und Endbenutzer.

Um das Sammeln von Daten aus den Raspberry Pi-Simulator zu starten, müssen Sie zuerst einen iothub zu erstellen.

1. Öffnen Sie das [Azure-Portal](https://portal.azure.com?azure-portal=true).
2. Klicken Sie im Azure-Portal links oben auf **Ressource erstellen**.
3. Wählen Sie **Internet der Dinge**, und wählen Sie dann **IoT Hub**.

![Screenshot der Navigation zu IoT Hub im Azure-Portal](../media-draft/fa40d1bc51bc4490f657e3c1a8371b5b.png)

4. Geben Sie im Bereich **IoT Hub** die folgenden Informationen für Ihren IoT Hub ein:
   
   **Abonnement**: Verwenden Sie das Standardabonnement für dieses Beispiel.
   **Ressourcengruppe**: Erstellen Sie eine Ressourcengruppe, die den IoT Hub enthält, oder verwenden Sie eine vorhandene. Wenn Sie alle verwandten Ressourcen in einer Gruppe (z.B *TestResources*) zusammenfassen, können Sie sie alle zusammen verwalten. Wenn Sie beispielsweise die Ressourcengruppe löschen, werden alle Ressourcen in dieser Gruppe gelöscht.
   **Region**: Wählen Sie den nächstgelegenen Standort aus.
   **Name**: Erstellen Sie einen eindeutigen Namen für Ihren IoT Hub. Wenn der eingegebene Name verfügbar ist, wird ein grünes Häkchen angezeigt.

> [!IMPORTANT]
> Der IoT Hub wird öffentlich als DNS-Endpunkt ermittelbar sein, sodass Sie beim Benennen die Verwendung von sensiblen Informationen vermeiden sollten.

   ![Fenster mit IoT Hub-Grundeinstellungen](./../media-draft/dbb7319388673b8ee0e0b407536156c0.png)

5. Klicken Sie auf **Next: Size and scale** (Nächster Schritt: Größe festlegen und skalieren), um die Erstellung Ihres IoT-Hubs fortzusetzen.
6. Wählen Sie eine Option für **Tarif und Skalierung** aus. Wählen Sie für dieses Beispiel die **F1 – Free** Ebene.

   ![Fenster für IoT Hub-Größe und -Skalierung](../media-draft/b506eb3293fa4aa9d4785ad498fc476c.png)

7. Klicken Sie auf **Überprüfen + erstellen**.

8. Überprüfen Sie die Informationen zum IoT-Hub, und klicken Sie auf **Erstellen**. Die Erstellung des IoT Hubs kann mehrere Minuten dauern. Sie können den Fortschritt im Bereich **Benachrichtigungen** überwachen.

<!--STOPPED HERE-->
<!--
Now that you have created an IoT hub, it's time to locate the important information that you use to connect devices and applications to your IoT hub. In your IoT hub navigation menu, open **Shared access policies**. Select the **iothubowner** policy, and then copy the **Connection string---primary key** of your IoT hub. For more information, see [Control access to IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security).

> [!NOTE]
> You do not need this iothubowner connection string for this set-up tutorial. However, you may need it for some of the tutorials or different IoT scenarios after you complete this set-up.

![Get your IoT hub connection string](../media-draft/a4b41e6ea46ccbef653c411a9829610c.png)
-->

## <a name="register-a-device"></a>Registrieren eines Geräts
Ein Gerät muss bei Ihrer IoT Hub-Instanz registriert sein, um eine Verbindung herstellen zu können.

1. Öffnen Sie in Ihrem IoT Hub-Navigationsmenü die Option **IoT-Geräte**, und klicken Sie auf **Hinzufügen**, um ein Gerät in Ihrem IoT Hub zu registrieren.

   ![Hinzufügen eines Geräts im Bereich „IoT-Geräte“ Ihres IoT Hubs](../media-draft/ee5f177abcf06b86dd007fce3b8448ad.png)

2. Geben Sie eine **Geräte-ID** für das neue Gerät ein. Bei Geräte-IDs wird die Groß-/Kleinschreibung beachtet.

> [!IMPORTANT]
> Diese Geräte-ID ist unter Umständen in den Protokollen sichtbar, die für den Kundensupport und die Problembehandlung erfasst werden. Stellen Sie also sicher, dass Sie beim Benennen keine sensiblen Informationen verwenden.

3. Klicken Sie auf **Speichern**.
4. Öffnen Sie das Gerät nach der Erstellung in der Liste im Bereich **IoT-Geräte**.
5. Kopieren Sie **Verbindungszeichenfolge – Primärschlüssel** zur späteren Verwendung.

   ![Abrufen der Geräte-Verbindungszeichenfolge](../media-draft/fba4413dcb652be92a6ab0f6bb638561.png)

## <a name="send-simulated-telemetry"></a>Senden simulierter Telemetriedaten

1. Öffnen der [Azure IoT Raspberry Pi-Simulator](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true).
2. Ersetzen Sie Platzhalter in Zeile 15 durch die Azure IoT Hub-Gerät-Verbindungszeichenfolge aus, die Sie gerade kopiert haben.
3. Klicken Sie auf die `Run` Schaltfläche oder ein Typ `npm start` im Konsolenfenster angezeigt, die Anwendung auszuführen.
   
   ![Ersetzen Sie die Verbindungszeichenfolge des Geräts](../media-draft/Line15.png)

Sie sollten die folgende Ausgabe angezeigt, die anzeigt, die Sensordaten und Nachrichten, die mit Ihrem iothub gesendet werden

![Ausgabe: Von Raspberry Pi an Ihren IoT Hub gesendete Sensordaten](../media-draft/96b28d30e317b04347abb0d613738117.png)

## <a name="read-the-telemetry-from-your-hub"></a>Lesen der Telemetriedaten aus Ihrem Hub
 Was ist also das Problem? Iothub empfängt die vom simulierten Gerät gesendeten Gerät-zu-Cloud-Nachrichten. Um zu sehen, dass wir nehmen einen kurzen Blick auf die Funktionsweise von Azure Iothub die eingehenden Daten verarbeitet wird. In Ihrem IoT-Hub unter **Überwachung**Option **Metriken**. Geben Sie ihm ein paar Minuten, während Sie warten, bis die Daten ins Spiel.
   
   ![IoT Hub-Metriken](../media-draft/HubMetrics.png)


<!--Reference links
https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started-->
