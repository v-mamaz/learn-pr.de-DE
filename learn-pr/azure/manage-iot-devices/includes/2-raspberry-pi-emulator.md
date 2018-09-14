Raspberry Pi-Boards sind neuerdings sehr beliebt, um Theorien zu testen oder um coole Dinge zu entwickeln. Die Kosten für diese Boards sind recht niedrig, aber möglicherweise möchten Sie die Raspberry Pi-Funktionalität dennoch testen, bevor Sie in ein solches Board investieren.

Microsoft hat einen Raspberry Pi-Onlinesimulator entwickelt, mit dem Benutzer die emulierte Hardware per Code steuern können. Der Emulator zeigt eine Grafik eines Raspberry Pi-Boards, der über ein Lochraster an einen Temperatur-, Feuchtigkeits- und Drucksensor sowie eine rote LED angeschlossen ist, sodass die Schaltkreise verbunden werden können. Die angezeigte Seitenleiste ermöglicht dem Benutzer die Eingabe von Node.js-JavaScript-Code, um die LED zu steuern und Dummydaten von den simulierten Sensoren zu erfassen.

Im ersten Durchlauf führt der Simulator ein einfaches Programm zur Temperaturerfassung aus, das über die Befehlszeile angezeigt wird. Die Beispielanwendung kann auch auf einem echten Pi-Board ausgeführt werden, weil der Simulator das Testen von Code ermöglicht, bevor dieser auf ein echtes Gerät übertragen wird.

## <a name="web-simulator"></a>Websimulator

Der Websimulator umfasst drei Bereiche:

1.  Assembly-Bereich: In der Standardschaltung stellt das Pi-Board eine Verbindung mit einem BME280-Sensor und einer LED her. Der Bereich ist in der Vorschauversion gesperrt, daher sind zurzeit keine Anpassungen möglich.

2.  Codingbereich: Ein Online-Code-Editor zum Codieren mit Raspberry Pi. Mit der Standard-Beispielanwendung können Sie Sensordaten von einem BME280-Sensor erfassen und diese an Azure IoT Hub senden. Die Anwendung ist vollständig mit echten Pi-Geräten kompatibel.

3.  Integriertes Konsolenfenster: Hier wird die Ausgabe des Codes angezeigt. Oben im Fenster werden drei Schaltflächen angezeigt.

    -   **Ausführen:** Hiermit wird die Anwendung im Codingbereich ausgeführt.

    -   **Zurücksetzen:** Hiermit wird der Codingbereich auf die Standard-Beispielanwendung zurückgesetzt.

    -   **Minimieren/Maximieren**: Auf der rechten Seite befindet sich eine Schaltfläche, mit der Sie das Konsolenfenster minimieren/maximieren können.

[Übersicht über den Pi-Onlinesimulator](./../media-draft/image1.png)

<!-- Reference links 
-   Online Raspberry Pi Emulator:
    <https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started>

-   <https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted>-->

