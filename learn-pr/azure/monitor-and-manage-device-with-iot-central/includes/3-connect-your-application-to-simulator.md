In der Praxis würden Sie Azure IoT Central wahrscheinlich mit einem echten Gerät (in diesem Fall: mit einer echten Kaffeemaschine) verbinden. Im Rahmen dieser Einheit, Sie aber eine Node.js-Anwendung, physische bzw. Real Kaffee Computer, auf die Azure IoT Central-Anwendung darstellt. Aufgrund dieser Verbindung Messungen von Telemetriedaten aus der Kaffeemaschine wird gesendet, IoT Central zur Überwachung und Analyse.

![Kaffeemaschine](../images/3-coffee-machine.png) 

## <a name="add-the-coffee-machine-in-iot-central"></a>Fügen Sie der Kaffeemaschine in IoT Central 
Um Ihre Kaffeemaschine für Ihre Anwendung hinzuzufügen, verwenden Sie die **Kaffeemaschine verbunden** Geräte aus, die Sie in der vorherigen Einheit erstellt haben.

1. Wählen Sie zum Hinzufügen eines neuen Geräts **Device Explorer** im linken Navigationsmenü.

    Wählen Sie zum Herstellen einer Verbindung Ihrer Kaffeemaschine starten **+ neu**, klicken Sie dann **echte**. Wenn Sie fertig sind, sehen Sie eine Liste der Geräte, die Sie mit der gleichen Kaffeemaschine verbunden-Vorlage erstellt haben.
   
    *   Die Kaffeemaschine verbunden wird die Liste, die bei der Auswahl "+" neu, und "Real hinzugefügt. 
    *   Kaffeemaschine verbunden (simulieren) wird automatisch von IoT Central zu Testzwecken erstellt. 

1.  Optional können Sie die neu hinzugefügte Kaffeemaschine unterscheiden, durch Anhängen des Worts "Real" in ihrem Namen. Wenn Sie das neue Gerät umbenennen möchten, wählen Sie das Gerät aus, und bearbeiten Sie den Namen in das Namensfeld. 

    ![Kaffeemaschine](../images/3-connect-device-a.png) 

    Beachten Sie den Speicherort der **dieses Gerät verbinden** für die Verbindung Ihrer Kaffeemaschine im nächsten Abschnitt. Für der Bildschirm nun zeigt "Missing Data" ist, da Sie nicht mit der Kaffeemaschine verbunden haben. Die tatsächliche Telemetriedaten beginnt damit, den Bildschirm zu füllen, sobald die Verbindung hergestellt wird. 
 
## <a name="get-connection-string-for-the-coffee-machine-from-your-application"></a>Abrufen der Verbindungszeichenfolge für die Kaffeemaschine aus Ihrer Anwendung
Die Verbindungszeichenfolge für Ihre echte Kaffeemaschine wird in den Code eingebettet, der auf dem Gerät ausgeführt wird. Mit der Verbindungszeichenfolge kann die Kaffeemaschine eine sichere Verbindung mit Ihrer Azure IoT Central-Anwendung herstellen. Jede Geräteinstanz besitzt eine eindeutige Verbindungszeichenfolge. So finden Sie die Verbindungszeichenfolge für eine Geräteinstanz in Ihrer Anwendung:

1.  Wählen Sie auf den Bildschirm "Gerät" für Ihre verbundene Kaffee Computer Real **dieses Gerät verbinden**.

1.  Kopieren Sie auf der Seite **Verbinden** den Wert für **Primäre Verbindungszeichenfolge**, und speichern Sie ihn. Dieser Wert wird in der auf dem Gerät ausgeführten Clientanwendung verwendet.

## <a name="create-a-nodejs-application"></a>Erstellen einer Node.js-Anwendung
Die folgenden Schritte zeigen, wie eine Client-Anwendung zu erstellen, die Kaffeemaschine implementiert, die Sie der Anwendung hinzugefügt.
1. Installieren Sie [Node.js](https://nodejs.org/) Version 4.0.x oder höher auf Ihrem Computer. Node.js ist für eine Vielzahl von Betriebssystemen verfügbar.

1. Erstellen Sie auf Ihrem Computer den Ordner „coffee-maker“. Navigieren Sie in der Befehlszeilenumgebung zu diesem Ordner.

1. Führen Sie die folgenden Befehle aus, um das Node.js-Projekt zu initialisieren:
    ```cmd/sh
    npm init
    ```
    > [!NOTE]
    > Die Init-Skript fordert Sie auf die Projekteigenschaften eingeben. Für diese Übung ist das unter Verwendung der Standardwerte ausreichend und empfehlenswert. 
1. Führen Sie den folgenden Befehl aus, um die erforderlichen Pakete zu installieren:
    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. Erstellen Sie im Ordner „coffee-maker“ mithilfe eines Text-Editors eine Datei namens „coffeeMaker.js“.

1. Kopieren Sie den Code in die Datei „coffeeMaker.js“, und klicken Sie auf **Speichern**.

    Der Code, den echten Kaffee-Computer in dieser Einheit darstellt, ist in Node.js geschrieben. Sie beginnen, durch die Einrichtung der Verbindung mit der Anwendung, und senden Sie die ursprüngliche Eigenschaften an Azure IoT Central, synchronisieren Sie die Einstellungen, zwei Befehlshandler für Wartung und Brewing registrieren und starten Sie anschließend den Timer für das Senden von Telemetriedaten Informationen pro Sekunde.

    > [!NOTE]
    > Aktualisieren Sie den Platzhalter `{your device connection string}`. 


    ```js
    "use strict";

    // Use the Azure IoT device SDK for devices that connect to Azure IoT Central
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;

    // Connection string (TODO: CHANGE HERE)
    const connectionString = `{your device connection string}`;

    // Global variables
    var client = clientFromConnectionString(connectionString);
    var optimalTemperature = 96;
    var cupState = true;
    var brewingState = false;
    var cupTimer = 20;
    var brewingTimer = 0;
    var maintenanceState = false;
    var warrantyState = Math.random() < 0.5?0:1;

    // Helper function to produce nice numbers (##.#)
    function niceNumber(value) 
    {
        var number = (Math.round(value * 10.0)).toString();
        return number.substr(0, 2) + '.' + number.substr(2, 1);
    }

    // Send device simulated telemetry measurements
    function sendTelemetry() 
    {   
        // Simulate the telemetry values
        var temperature = optimalTemperature + (Math.random() * 4) - 2;
        var humidity = 20 + (Math.random() * 80);
        
        // Cup timer - every 20 second randomly decide if the cup is present or not
        cupTimer--;
        
        if (cupTimer == 0)
        {
            cupTimer = 20;
            cupState = Math.random() < 0.5?false:true;
        }
        
        // Brewing timer
        if (brewingTimer > 0)
        {
            brewingTimer--;
            
            // Finished brewing
            if (brewingTimer == 0)
            {
                brewingState = false;
            }
        }
    
        // Create the data JSON package
        var data = JSON.stringify(
        { 
            waterTemperature: temperature, 
            airHumidity: humidity, 
        });

        // Create the message with the above defined data
        var message = new Message(data);
        
        // Set the state flags
        message.properties.add('stateCupDetected', cupState);
        message.properties.add('stateBrewing', brewingState);
        
        // Show the information in console
        var infoTemperature = niceNumber(temperature);
        var infoHumidity = niceNumber(humidity);
        var infoCup = cupState ? 'Y' :'N';
        var infoBrewing = brewingState ? 'Y':'N';
        var infoMaintenance = maintenanceState ? 'Y':'N';
        
        console.log('Telemetry send: Temperature: ' + infoTemperature + 
                    ' Humidity: ' + infoHumidity + '%' + 
                    ' Cup Detected: ' + infoCup + 
                    ' Brewing: ' + infoBrewing + 
                    ' Maintenance Mode: ' + infoMaintenance);
        
        // Send the message
        client.sendEvent(message, function (errorMessage) 
        {
            // Error
            if (errorMessage) 
            {
                console.log('Failed to send message to Azure IoT Hub: ${err.toString()}');
            }
        });
    }

    // Send device properties
    function sendDeviceProperties(deviceTwin) 
    {
        var properties = 
        {
            propertyWarrantyExpired: warrantyState
        };
        
        console.log(' * Property - Warranty State: ' + warrantyState.toString());
        
        deviceTwin.properties.reported.update(properties, (errorMessage) => 
            console.log(` * Sent device properties ` + (errorMessage ? `Error: ${errorMessage.toString()}` : `(success)`)));
    }

    // Optimal temperature setting
    var settings = 
    {
        'setTemperature': (newValue, callback) => 
        {
            setTimeout(() => 
            {
                optimalTemperature = newValue;
                callback(optimalTemperature, 'completed');
            }, 1000);
        }
    };

    // Handle settings changes that come from Azure IoT Central via the device twin.
    function handleSettings(deviceTwin) 
    {
        deviceTwin.on('properties.desired', function (desiredChange) 
        {
            // Iterate all settings looking for the defined one
            for (let setting in desiredChange) 
            {
                // Setting we defined
                if (settings[setting]) 
                {
                    // Console info
                    console.log(` * Received setting: ${setting}: ${desiredChange[setting].value}`);
                    
                    // Update 
                    settings[setting](desiredChange[setting].value, (newValue, status, message) => 
                    {
                        var patch = 
                        {
                            [setting]: 
                            {
                                value: newValue,
                                status: status,
                                desiredVersion: desiredChange.$version,
                                message: message
                            }
                        }
                        deviceTwin.properties.reported.update(patch, (err) => console.log(` * Sent setting update for ${setting} ` +
                        (err ? `error: ${err.toString()}` : `(success)`)));
                    });
                }
            }
        });
    }

    // Maintenance mode command
    function onCommandMaintenance(request, response) 
    {
        // Display console info
        console.log(' * Maintenance command received');

        // Console warning
        if (maintenanceState)
        {
            console.log(' - Warning: The device is already in the maintenance mode.');
        }
        
        // Set state
        maintenanceState = true;

        // Respond
        response.send(200, 'Success', function (errorMessage) 
        {
            // Failure
            if (errorMessage) 
            {
                console.error('[IoT hub Client] Failed sending a method response:\n' + errorMessage.message);
            }
        });
    }

    function onCommandStartBrewing(request, response) 
    {
        // Display console info
        console.log(' * Brewing command received');

        // Console warning
        if (brewingState == true)
        {
            console.log(' - Warning: The device is already brewing.');
        }
        
        if (cupState == false)
        {
            console.log(' - Warning: The cup has not been detected.');
        }
        
        if (maintenanceState == true)
        {
            console.log(' - Warning: The device is in maintenance state.');
        }
        
        // Set state - brew for 30 seconds
        if ((cupState == true) && (brewingState == false) && (maintenanceState == false))
        {
            brewingState = true;
            brewingTimer = 30;
        }
        
        // Respond
        response.send(200, 'Success', function (errorMessage) 
        {
            // Failure
            if (errorMessage) 
            {
                console.error('[IoT hub Client] Failed sending a method response:\n' + errorMessage.message);
            }
        });
    }

    // Handle device connection to Azure IoT Central
    var connectCallback = (errorMessage) => 
    {
        // Connection error
        if (errorMessage) 
        {
            console.log(`Device could not connect to Azure IoT Central: ${errorMessage.toString()}`);
        } 
        // Successfully connected
        else 
        {
            // Notify the user
            console.log('Device successfully connected to Azure IoT Central');

            // Send telemetry measurements to Azure IoT Central every 1 second.
            setInterval(sendTelemetry, 1000);
            
            // Setup device command callbacks
            client.onDeviceMethod('cmdSetMaintenance', onCommandMaintenance);
            client.onDeviceMethod('cmdStartBrewing', onCommandStartBrewing);
            
            // Get device twin from Azure IoT Central
            client.getTwin((errorMessage, deviceTwin) => 
            {
                // Failed to retrieve device twin
                if (errorMessage) 
                {
                    console.log(`Error getting device twin: ${errorMessage.toString()}`);
                } 
                // Success
                else 
                {
                    // Notify the user
                    console.log('Device Twin successfully retrieved from Azure IoT Central');
                
                    // Send device properties once on device start up
                    sendDeviceProperties(deviceTwin);
                    
                    // Apply device settings and handle changes to device settings
                    handleSettings(deviceTwin);
                }
            });
        }
    };

    // Start the device (connect it to Azure IoT Central)
    client.open(connectCallback);



    ```

1.  Ersetzen Sie den Platzhalter „{your device connection string}“ durch die Verbindungszeichenfolge Ihres Geräts. Diesen Wert haben Sie auf der Seite mit den Verbindungsdetails kopiert, als Sie Ihr echtes Gerät hinzugefügt haben. 

## <a name="run-your-nodejs-application"></a>Ausführen der Node.js-Anwendung
```cmd/sh
node coffeeMaker.js
```

## <a name="summary"></a>Zusammenfassung
In dieser Einheit müssen Sie Ihren Kaffee-Computer mit Azure IoT Central verbunden und begann, Senden von Daten zur Überwachung und Analyse. Zur Verbindungsherstellung haben Sie zuerst eine Verbindungszeichenfolge aus IoT Central abgerufen und sie anschließend für die Kaffeemaschine konfiguriert.
