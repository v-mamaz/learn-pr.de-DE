Das Erfassen von Wetterdaten ist eine wichtige Aufgabe, weil das Wetter vieles beeinflusst – von Verkehrsmustern bis hin zum Betrieb von Heizungs-, Lüftungs- und Klimasystemen (Heating, Ventilation, Air Conditioning, HVAC) im Einzelhandel. In dieser Übung interagieren Sie mit dem Raspberry Pi-Onlinesimulator, der in der vorherigen Einheit vorgestellt wurde, um simulierte Wetterdaten zu erfassen und über Azure IoT Hub zu speichern.

[!include[](../../../includes/azure-sandbox-activate.md)]

Diese Übung wird zwar in einer simulierten Umgebung durchgeführt, die auf dem simulierten Gerät ausgeführte Anwendung kann jedoch später auf ein echtes Gerät übertragen werden.

## <a name="create-an-iot-hub"></a>Erstellen einer IoT Hub-Instanz
Auf der Grundlage der Features und des Erweiterungsmodells von Azure IoT Hub können Geräte- und Back-End-Entwickler stabile Geräteverwaltungslösungen entwickeln. Das Spektrum der Geräte reicht von einfachen Sensoren und zweckgebundenen Microcontrollern bis hin zu leistungsfähigen Gateways zur Weiterleitung der Kommunikation für Gerätegruppen. Die Anwendungsfälle und Anforderungen für IoT-Betreiber sind außerdem sehr branchenspezifisch. Trotz dieser Vielfalt bietet die Geräteverwaltung mit Azure IoT Hub Funktionen, Muster und Codebibliotheken für unterschiedlichste Geräte und Endbenutzer.

Um mit dem Sammeln von Daten aus dem Raspberry Pi-Simulator beginnen zu können, müssen Sie zunächst eine IoT Hub-Instanz erstellen.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.

2. Klicken Sie links oben im Azure-Portal auf **Ressource erstellen**.

3. Klicken Sie auf **Internet der Dinge** und anschließend auf **IoT Hub**.

![Screenshot der Navigation zu IoT Hub im Azure-Portal](../media/fa40d1bc51bc4490f657e3c1a8371b5b.png)

4. Geben Sie im Bereich **IoT Hub** die folgenden Informationen für Ihre IoT Hub-Instanz ein:
   
   - **Abonnement:** Verwenden Sie für dieses Beispiel das Standardabonnement.
   - **Ressourcengruppe:** Verwenden Sie die vorhandene Ressourcengruppe. Indem Sie alle verwandten Ressourcen in der gleichen Gruppe zusammenfassen, können Sie sie alle zusammen verwalten. Wenn Sie also beispielsweise die Ressourcengruppe löschen, werden alle Ressourcen in dieser Gruppe gelöscht.
   - **Name:** Erstellen Sie einen eindeutigen Namen für Ihre IoT Hub-Instanz. Ist der eingegebene Name verfügbar, wird ein grünes Häkchen angezeigt.
   - **Region:** Wählen Sie in der folgenden Liste den nächstgelegenen Standort aus.

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    > [!IMPORTANT]
    > Der IoT Hub wird öffentlich als DNS-Endpunkt ermittelbar sein, sodass Sie beim Benennen die Verwendung von sensiblen Informationen vermeiden sollten.
    
    ![Fenster mit IoT Hub-Grundeinstellungen](./../media/dbb7319388673b8ee0e0b407536156c0.png)

1. Klicken Sie auf **Nächster Schritt: Größe festlegen und skalieren**, um die Erstellung Ihres IoT-Hubs fortzusetzen.
2. Wählen Sie eine Option für **Tarif und Skalierung** aus. Verwenden Sie für dieses Beispiel den Tarif **F1 – Free**.

    ![Fenster für IoT Hub-Größe und -Skalierung](../media/b506eb3293fa4aa9d4785ad498fc476c.png)

3. Klicken Sie auf **Überprüfen + erstellen**.

4. Überprüfen Sie die Informationen zum IoT-Hub, und klicken Sie auf **Erstellen**. Die Erstellung des IoT Hubs kann mehrere Minuten dauern. Sie können den Fortschritt im Bereich **Benachrichtigungen** überwachen.

<!--STOPPED HERE-->
<!--
Now that you have created an IoT hub, it's time to locate the important information that you use to connect devices and applications to your IoT hub. In your IoT hub navigation menu, open **Shared access policies**. Select the **iothubowner** policy, and then copy the **Connection string---primary key** of your IoT hub. For more information, see [Control access to IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security).

> [!NOTE]
> You do not need this iothubowner connection string for this set-up exercise. However, you may need it for some of the tutorials or different IoT scenarios after you complete this set-up.

![Get your IoT hub connection string](../media/a4b41e6ea46ccbef653c411a9829610c.png)
-->

## <a name="register-a-device"></a>Registrieren eines Geräts
Ein Gerät muss bei Ihrer IoT Hub-Instanz registriert werden, um eine Verbindung herstellen zu können.

1. Öffnen Sie in Ihrem IoT Hub-Navigationsmenü die Option **IoT-Geräte**, und klicken Sie auf **Hinzufügen**, um ein Gerät bei Ihrer IoT Hub-Instanz zu registrieren.

   ![Hinzufügen eines Geräts im Bereich „IoT-Geräte“ Ihres IoT Hubs](../media/ee5f177abcf06b86dd007fce3b8448ad.png)

2. Geben Sie eine **Geräte-ID** für das neue Gerät ein. Bei Geräte-IDs wird die Groß-/Kleinschreibung beachtet.

    > [!IMPORTANT]
    > Diese Geräte-ID ist unter Umständen in den Protokollen sichtbar, die für den Kundensupport und die Problembehandlung erfasst werden. Stellen Sie also sicher, dass Sie beim Benennen keine sensiblen Informationen verwenden.
    
3. Klicken Sie auf **Speichern**.
4. Öffnen Sie das Gerät nach der Erstellung in der Liste im Bereich **IoT-Geräte**.
5. Kopieren Sie **Verbindungszeichenfolge – Primärschlüssel** zur späteren Verwendung.

   ![Abrufen der Geräte-Verbindungszeichenfolge](../media/fba4413dcb652be92a6ab0f6bb638561.png)

## <a name="send-simulated-telemetry"></a>Senden simulierter Telemetriedaten

1. Öffnen Sie den [Azure IoT-Simulator für den Raspberry Pi](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true).
1. Ersetzen Sie den Platzhalter in Zeile 15 durch die soeben kopierte Verbindungszeichenfolge für das Azure IoT Hub-Gerät.
1. Klicken Sie auf die Schaltfläche `Run`, oder geben Sie im Konsolenfenster `npm start` ein, um die Anwendung auszuführen.
   
    ![Ersetzen der Geräte-Verbindungszeichenfolge](../media/Line15.png)

1. Die folgende Ausgabe sollte angezeigt werden, die die Sensordaten und Nachrichten zeigt, die an Ihren IoT Hub gesendet werden.

    ![Ausgabe: Von Raspberry Pi an Ihren IoT Hub gesendete Sensordaten](../media/96b28d30e317b04347abb0d613738117.png)

## <a name="read-the-telemetry-from-your-hub"></a>Lesen der Telemetriedaten aus Ihrem Hub
Nun passiert Folgendes: IoT Hub empfängt die vom simulierten Gerät gesendeten Gerät-zu-Cloud-Nachrichten. Um das zu sehen, schauen wir uns kurz an, wie Azure IoT Hub die eingehenden Daten verarbeitet. Klicken Sie in Ihrer IoT Hub-Instanz unter **Überwachung** auf **Metriken**. Warten Sie ein paar Minuten, bis die Daten eintreffen.
   
![IoT Hub-Metriken](../media/HubMetrics.png)


<!--Reference links
https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started-->
