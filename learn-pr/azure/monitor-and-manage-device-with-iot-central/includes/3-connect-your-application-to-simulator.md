[!include[](../../../includes/azure-sandbox-activate.md)]

In dieser Übung stellen Sie eine Verbindung zwischen Azure IoT Central und einem physischen Gerät her, in diesem Fall mit einer IoT-fähigen Kaffeemaschine. Hier simulieren Sie ein Gerät mithilfe einer Node.js-Anwendung und verbinden es mit der Azure IoT Central-Anwendung. Die gemessenen Telemetriedaten der simulierten Kaffeemaschine werden zur Überwachung und Analyse an IoT Central gesendet.

![Illustration einer Kaffeemaschine](../media/3-coffee-machine.png) 

## <a name="add-the-coffee-machine-in-iot-central"></a>Hinzufügen der Kaffeemaschine in IoT Central 
Um die Kaffeemaschine zu Ihrer Anwendung hinzuzufügen, verwenden Sie die Gerätevorlage **Connected Coffee Maker**, die Sie in der vorherigen Einheit erstellt haben.

1. Klicken Sie im linken Navigationsmenü auf **Device Explorer**, um ein neues Gerät hinzuzufügen.

    Klicken Sie zum Herstellen einer Verbindung für die Kaffeemaschine auf **+ Neu**, **Real** und anschließend auf **Erstellen**. Daraufhin wird eine Liste mit Geräten angezeigt, die Sie unter Verwendung der Vorlage „Connected Coffee Maker“ (Verbundene Kaffeemaschine) erstellt haben.
   
    *   Die verbundene Kaffeemaschine wird der Liste hinzugefügt, wenn Sie auf **+ Neu** und dann auf **Real** klicken. 
    *   Die simulierte verbundene Kaffeemaschine wird von IoT Central automatisch zu Testzwecken erstellt. 

1.  Zur Unterscheidung können Sie den Namen der neu hinzugefügten Kaffeemaschine optional mit dem Suffix „Real“ versehen. Klicken Sie zum Umbenennen des neuen Geräts auf das Gerät, und bearbeiten Sie den Namen im Namensfeld. 

    ![Kaffeemaschine](../media/3-connect-device-a.png) 

    Beachten Sie die Position von **Connect this device** (Dieses Gerät verbinden) für das Verbinden Ihrer Kaffeemaschine im nächsten Abschnitt. Vorerst wird angezeigt, dass Daten fehlen, da Sie noch keine Verbindung mit der Kaffeemaschine hergestellt haben. Der Bildschirm wird mit echten Telemetriedaten gefüllt, sobald die Verbindung hergestellt wurde. 
 
## <a name="generate-connection-string-for-the-coffee-machine-from-your-application"></a>Generieren der Verbindungszeichenfolge für die Kaffeemaschine über Ihre Anwendung
Die Verbindungszeichenfolge für Ihre echte Kaffeemaschine wird in den Code eingebettet, der auf dem Gerät ausgeführt wird. Mit der Verbindungszeichenfolge kann die Kaffeemaschine eine sichere Verbindung mit Ihrer Azure IoT Central-Anwendung herstellen. Jede Geräteinstanz besitzt eine eindeutige Verbindungszeichenfolge. In den nächsten Schritten generieren Sie die Verbindungszeichenfolge im Rahmen der Erstellung einer Node.js-Anwendung.

## <a name="create-a-nodejs-application"></a>Erstellen einer Node.js-Anwendung
In den folgenden Schritten wird gezeigt, wie Sie eine Clientanwendung zur Implementierung der Kaffeemaschine erstellen, die Sie der Anwendung hinzugefügt haben.

> [!TIP]
> In dieser Übung erstellen Sie die App in Azure Cloud Shell, damit Sie nichts auf Ihrem lokalen Computer installieren müssen. 

1. Führen Sie den folgenden Befehl in Azure Cloud Shell aus, um einen `coffee-maker`-Ordner zu erstellen und zu diesem zu navigieren:

    ```azurecli
    mkdir ~/coffee-maker
    cd ~/coffee-maker
    ```

1. Führen Sie den folgenden Befehl im `coffee-maker`-Ordner in Cloud Shell aus, um den DPS-Schlüsselgenerator zu installieren: 

   ```azurecli
    npm install dps-keygen
   ```
    Dieser Befehl installiert das Paket „dps-keygen“ im lokalen `coffee-maker`-Ordner. Die Option `-g` wird ausgelassen, da Sie über keine Berechtigungen für die Installation als globales Paket verfügen.

    <!-- TODO: Add more information about the DPS key generator and what it's used for -->
 
1. Führen Sie den folgenden Befehl in Cloud Shell aus, um das Hilfsprogramm für die DPS-Verbindungszeichenfolge von GitHub herunterzuladen: 

    ```azurecli
    wget https://github.com/Azure/dps-keygen/blob/master/bin/linux/dps_cstr?raw=true -O dps_cstr 
    ```

    > [!NOTE]
    > Mit diesem Befehl wird die Linux-Version von **dps_cstr** heruntergeladen, da diese Übung in Cloud Shell durchgeführt wird.

1. Führen Sie den folgenden Befehl aus, um `dps_cstr` die Ausführungsberechtigungen zu erteilen:

    ```azurecli
    chmod +x dps_cstr
    ```

    Sie benötigen drei Informationen aus dem Azure IoT Central-Portal, um eine Verbindungszeichenfolge für Ihr Gerät zu generieren:
    - **Bereichs-ID**
    - **Geräte-ID**
    - **Primärschlüssel**

1. Kehren Sie zum IoT Central-Portal zurück. Klicken Sie auf dem Gerätebildschirm für das Gerät *Connected Coffee Maker - Real* (Verbundene Kaffeemaschine – Real) in der oberen rechten Ecke des Bildschirms auf **Verbinden**.

1. Speichern Sie die Werte für die **Bereichs-ID**, die **Geräte-ID** und den **Primärschlüssel**, die im angezeigten Dialogfeld „Geräteverbindung“ angezeigt werden, da Sie sie im späteren Verlauf dieser Übung benötigen. 

1. Führen Sie den folgenden Befehl in Cloud Shell aus, und ersetzen Sie hierbei **<scope_id>**, **<device_id>** und **<primary_key>** durch die im vorherigen Schritt gespeicherten Werte. 

   ```azurecli
   ./dps_cstr [scope_id] [device_id] [primary_key] > connection.txt
   ```
  
    Mit diesem Befehl wird eine Verbindungszeichenfolge basierend auf den Werten generiert, die Sie zugewiesen haben, und diese wird in eine Datei eingefügt, der Sie den Namen **connection.txt** gegeben haben.

    > [!IMPORTANT]
    > Der Befehl `dps_cstr` befindet sich in Ihrer PATH-Variable in der Shell. Stellen Sie also sicher, dass Sie ihn mit `./dps_cstr` aufrufen.

1. Öffnen Sie den integrierten Code-Editor in Cloud Shell, indem Sie den folgenden Befehl ausführen. 

    ```azurecli
    code
    ```
1. Wählen Sie **connection.txt** in der Dateiliste des Menüs **FILES** des Editors aus.

1. Stellen Sie sicher, dass **connection.txt** eine Verbindungszeichenfolge enthält, die mit ``HostName=`` beginnt.

1. Schließen Sie den Editor, indem Sie im Menü (*...*) oben rechts im Editor auf **Editor schließen** klicken. 

1. Führen Sie den folgenden Befehl in Cloud Shell aus, um ein Node.js-Projekt im `coffee-maker`-Ordner zu initialisieren:

    ```azurecli
    npm init
    ```
    > [!NOTE]
    > Das Initialisierungsskript fordert Sie zur Eingabe von Projekteigenschaften auf. Drücken Sie die EINGABETASTE, um für diese Übung alle Standardwerte zu verwenden.

1. Führen Sie den folgenden Befehl im `coffee-maker`-Ordner aus, um die erforderlichen Pakete zu installieren:

    ```azurecli
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. Führen Sie den folgenden Befehl aus, um eine neue Datei in Cloud Shell zu erstellen:

    ```azurecli
    touch coffeeMaker.js
    ```
1. Öffnen Sie den integrierten Code-Editor, indem Sie folgenden Befehl in der Befehlszeile in Cloud Shell ausführen: 

     ```azurecli
    code
    ```
    
1. Nachdem der Code-Editor geöffnet wurde, klicken Sie in der **FILES**-Liste auf die Schaltfläche zum Aktualisieren, und wählen Sie die neue Date **coffeeMaker.js** aus. 

1. Kopieren Sie den folgenden Code, und fügen Sie ihn in das leere Editorfenster ein:

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
        
        // Cup timer - every 20 seconds randomly decide if the cup is present or not
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
            
            // Set up device command callbacks
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
                
                    // Send device properties once on device startup
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

    Der Code der Kaffeemaschine für diese Übung ist in Node.js geschrieben. Zunächst wird eine Verbindung zu Azure IoT Central hergestellt. Dann sendet die App die ersten Eigenschaften an Azure IoT Central, synchronisiert die Einstellungen, registriert zwei Befehlshandler für Wartung und Brühvorgang und startet letztendlich den Timer zum Senden von Telemetriedaten im Sekundentakt.

1.  Ersetzen Sie den Platzhalter `{your device connection string}` am Anfang des Codes durch die Verbindungszeichenfolge, die Sie zuvor erstellt und in der Datei **connection.txt** gespeichert haben. Die Verbindungszeichenfolge beginnt mit `HostName=`.

1. Klicken Sie oben rechts im Editor auf die drei Punkte (`...`), um das Editor-Menü zu erweitern. Klicken Sie dann auf **Speichern**, um die Änderungen an „coffeeMaker.js“ zu speichern.

1. Führen Sie den folgenden Befehl im Cloud Shell-Fenster aus, um die App zu starten:

    ```azurecli
    node coffeeMaker.js
    ```
1. Stellen Sie sicher, dass die App mit den Nachrichten *Device successfully connected to Azure IoT Central* (Gerät wurde erfolgreich mit Azure IoT Central verbunden) und *Telemetry send:* (Telemetriedaten senden:) gestartet wird. Herzlichen Glückwunsch! Ihre App ist in Betrieb und kommuniziert mit IoT Central.