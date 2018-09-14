Raspberry Pi-Boards haben viel Interesse später für die Tests, Theorien oder ein Ereignis, sodass das coole löste. Die Kosten auf diesem Boards sind, zwar relativ gering möglicherweise einige von Interesse sein Testen der Raspberry Pi-Funktionalität vor der Investition in eine.

Microsoft hat eine online erstellte [Raspberry Pi-Azure-IoT-Simulator](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true) ermöglicht Benutzern die Kontrolle über der emulierten Hardware über Code. Der Emulator zeigt Informationen zur eine Grafik des Raspberry Pi verbunden werden, um eine Temperatur, Luftfeuchtigkeit, Drucksensor und eine rote LED über steckplatine, sodass Verbindungen miteinander verbunden sein. Im Bereich der angezeigten Seite kann Benutzer zur Eingabe von Node.js-JavaScript-Code zum Steuern der LED und Sammeln von unechten Daten aus dem simulierten Sensor.

![Raspberry Pi-Simulator](../media-draft/RaspberryPiSimulator.png)

## <a name="raspberry-pi-azure-iot-online-simulator"></a>Raspberry Pi-Onlinesimulator Azure IoT

Bei der ersten Ausführung wird der Simulator ein Temperatur Capture-Beispielprogramm die angezeigt wird, über die Befehlszeile ausgeführt. Dieselbe beispielanwendung kann auch auf einem echten Pi ausgeführt werden, wie der Simulator vorgesehen ist, Personen, um Code zu testen, bevor sie in einem echten Gerät übertragen können.

Im websimulator werden drei Bereiche:

1. **Assembly-Bereich**. Dies ist in der Ihre Gerätestatus angezeigt. Standardmäßig ist dies ein Pi Herstellen einer Verbindung mit einem BME280-Sensor und eine LED leuchtet. Diese Konfiguration ist zu diesem Zeitpunkt nicht angepasst.
2. **Codingbereich**. Ein online-Code-Editor für Sie zu einer app auf dem Raspberry Pi mit Node.js. Die Standard-beispielanwendung kann zum Sammeln von Daten von triebwerksensoren vom BME280-Sensor und sendet sie an Azure IoT Hub.
3. **Integriertes Konsolenfenster**. Dies ist, in dem Sie die Ausgabe der app sehen können. In der Konsole stehen drei Funktionen zur Verfügung:
    - `run` – Den Code ausgeführt wird (wenn das Beispiel ausgeführt wird, Code ist schreibgeschützt).
    - `Stop` – Beendet den Beispielcode, der ausgeführt wird.
    - `Reset` – Setzt der Code.

Nun, da Sie eine Übersicht über den Raspberry Pi-Simulator haben, untersuche ich die IoT Hub in Azure, in dem Sie eine neue Ressource zum Erfassen von Daten aus den Simulator erstellt.

<!-- Reference links 
-   Online Raspberry Pi Emulator:
    <https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started>
-   <https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted>-->