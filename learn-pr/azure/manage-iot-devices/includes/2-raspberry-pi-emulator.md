Raspberry Pi-Boards sind neuerdings sehr beliebt, um Theorien zu testen oder um coole Dinge zu entwickeln. Die Boards sind zwar nicht teuer, möglicherweise möchten Sie die Raspberry Pi-Funktionalität aber erst einmal testen, bevor Sie in ein solches Board investieren.

Microsoft hat einen [Azure IoT-Onlinesimulator für den Raspberry Pi](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true) entwickelt, mit dem Benutzer die emulierte Hardware per Code steuern können. Der Emulator stellt eine Grafik eines Raspberry Pi-Boards dar, das über ein Lochraster, welches die Verbindung der Schaltkreise ermöglicht, mit einem Temperatur-, Feuchtigkeits- und Drucksensor sowie mit einer roten LED verbunden ist. Die angezeigte Seitenleiste ermöglicht dem Benutzer die Eingabe von Node.js-JavaScript-Code, um die LED zu steuern und Dummydaten von den simulierten Sensoren zu erfassen.

![Raspberry Pi-Simulator](../media/RaspberryPiSimulator.png)

## <a name="raspberry-pi-azure-iot-online-simulator"></a>Azure IoT-Onlinesimulator für den Raspberry Pi

Im ersten Durchlauf führt der Simulator ein einfaches Programm zur Temperaturerfassung aus, das über die Befehlszeile angezeigt wird. Die Beispielanwendung kann auch auf einem echten Pi-Board ausgeführt werden, da der Simulator das Testen von Code ermöglicht, bevor dieser auf ein echtes Gerät übertragen wird.

Der Websimulator umfasst drei Bereiche:

1. **Assemblybereich:** Hier sehen Sie den Status Ihres Geräts. Standardmäßig handelt es sich hierbei um ein Pi-Board mit einem BME280-Sensor und einer LED. Diese Konfiguration kann momentan nicht angepasst werden.
2. **Programmierbereich:** Ein onlinebasierter Code-Editor, mit dem Sie eine Node.js-App für den Raspberry Pi erstellen können. Mit der Standard-Beispielanwendung können Sie Sensordaten von einem BME280-Sensor erfassen und diese an Azure IoT Hub senden.
3. **Integriertes Konsolenfenster:** Hier wird die Ausgabe Ihrer App angezeigt. In der Konsole stehen drei Funktionen zur Verfügung:
    - `run`: Führt den Beispielcode aus. (Während der Ausführung ist der Code schreibgeschützt.)
    - `Stop`: Beendet die Ausführung des Beispielcodes.
    - `Reset`: Setzt den Code zurück.

Nachdem Sie sich nun einen Überblick über den Raspberry Pi-Simulator verschafft haben, sehen wir uns als Nächstes IoT Hub in Azure an. Dort erstellen Sie eine neue Ressource, um Daten aus dem Simulator zu erfassen.

<!-- Reference links 
-   Online Raspberry Pi Emulator:
    <https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started>
-   <https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted>-->