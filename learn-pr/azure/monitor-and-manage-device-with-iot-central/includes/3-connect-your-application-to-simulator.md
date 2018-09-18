<span data-ttu-id="5dd8a-101">In der Praxis würden Sie Azure IoT Central wahrscheinlich mit einem echten Gerät (in diesem Fall: mit einer echten Kaffeemaschine) verbinden.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-101">In real life, it's assumed that you will connect Azure IoT Central to a real device or in this case, a real coffee machine.</span></span> <span data-ttu-id="5dd8a-102">Im Rahmen dieser Einheit verbinden Sie dagegen eine Node.js-Anwendung, die eine physische/echte Kaffeemaschine darstellt, mit der Azure IoT Central-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-102">But for the purpose of this unit, you connect a Node.js application, representing a physical/real coffee machine, to the Azure IoT Central application.</span></span> <span data-ttu-id="5dd8a-103">Über diese Verbindung werden Telemetriemessungen der Kaffeemaschine zur Überwachung und Analyse an IoT Central gesendet.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-103">As a result of this connection, telemetry measurements from the coffee machine is sent to IoT Central for monitoring and analysis.</span></span>

![Kaffeemaschine](../images/3-coffee-machine.png) 

## <a name="add-the-coffee-machine-in-iot-central"></a><span data-ttu-id="5dd8a-105">Hinzufügen der Kaffeemaschine in IoT Central</span><span class="sxs-lookup"><span data-stu-id="5dd8a-105">Add the coffee machine in IoT Central</span></span> 
<span data-ttu-id="5dd8a-106">Um die Kaffeemaschine zu Ihrer Anwendung hinzuzufügen, verwenden Sie die Gerätevorlage **Connected Coffee Maker**, die Sie in der vorherigen Einheit erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-106">To add your coffee machine to your application, you use the **Connected Coffee Maker** device template you created in the previous unit.</span></span>

1. <span data-ttu-id="5dd8a-107">Klicken Sie im linken Navigationsmenü auf **Device Explorer**, um ein neues Gerät hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="5dd8a-107">To add a new device, choose **Device Explorer** in the left navigation menu.</span></span>

    <span data-ttu-id="5dd8a-108">Klicken Sie zum Herstellen einer Verbindung für die Kaffeemaschine auf **+ Neu** und anschließend auf **Real**.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-108">To start connecting your coffee machine, choose **+ New**, then **Real**.</span></span> <span data-ttu-id="5dd8a-109">Daraufhin wird eine Liste mit Geräten angezeigt, die Sie unter Verwendung der Vorlage „Connected Coffee Maker“ (Verbundene Kaffeemaschine) erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-109">When you're finished, you see a list of devices you've created using the same Connected Coffee Maker template.</span></span>
   
    *   <span data-ttu-id="5dd8a-110">Die verbundene Kaffeemaschine wird der Liste hinzugefügt, wenn Sie auf „+ Neu“ und anschließend auf „Real“ klicken.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-110">The Connected Coffee Maker is added to the list when you choose + New, then Real.</span></span> 
    *   <span data-ttu-id="5dd8a-111">Die simulierte verbundene Kaffeemaschine wird von IoT Central automatisch zu Testzwecken erstellt.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-111">The Connected Coffee Maker (Simulate) is automatically created by IoT Central for testing purposes.</span></span> 

1.  <span data-ttu-id="5dd8a-112">Zur Unterscheidung können Sie den Namen der neu hinzugefügten Kaffeemaschine optional mit dem Suffix „Real“ versehen.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-112">Optionally, you can differentiate the newly added coffee machine by appending the word “Real” in its name.</span></span> <span data-ttu-id="5dd8a-113">Klicken Sie zum Umbenennen des neuen Geräts auf das Gerät, und bearbeiten Sie den Namen im Namensfeld.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-113">To rename your new device, choose the device and edit the name in the name field.</span></span> 

    ![Kaffeemaschine](../images/3-connect-device-a.png) 

    <span data-ttu-id="5dd8a-115">Beachten Sie die Position von **Connect this device** (Dieses Gerät verbinden) für die Verbindungsherstellung mit Ihrer Kaffeemaschine im nächsten Abschnitt.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-115">Note the location of **Connect this device** for connecting your coffee machine in the next section.</span></span> <span data-ttu-id="5dd8a-116">Vorerst wird jedoch angezeigt, dass Daten fehlen. Das liegt daran, dass Sie noch keine Verbindung mit der Kaffeemaschine hergestellt haben.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-116">For now the screen displays "Missing Data", this is because you haven't connected to the coffee machine.</span></span> <span data-ttu-id="5dd8a-117">Der Bildschirm wird mit echten Telemetriedaten gefüllt, sobald die Verbindung hergestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-117">The real telemetry begins to populate the screen once the connection is made.</span></span> 
 
## <a name="get-connection-string-for-the-coffee-machine-from-your-application"></a><span data-ttu-id="5dd8a-118">Abrufen der Verbindungszeichenfolge für die Kaffeemaschine aus Ihrer Anwendung</span><span class="sxs-lookup"><span data-stu-id="5dd8a-118">Get connection string for the coffee machine from your application</span></span>
<span data-ttu-id="5dd8a-119">Die Verbindungszeichenfolge für Ihre echte Kaffeemaschine wird in den Code eingebettet, der auf dem Gerät ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-119">You embed the connection string for your real coffee machine in the code that runs on the device.</span></span> <span data-ttu-id="5dd8a-120">Mit der Verbindungszeichenfolge kann die Kaffeemaschine eine sichere Verbindung mit Ihrer Azure IoT Central-Anwendung herstellen.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-120">The connection string enables the coffee machine to connect securely to your Azure IoT Central application.</span></span> <span data-ttu-id="5dd8a-121">Jede Geräteinstanz besitzt eine eindeutige Verbindungszeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-121">Every device instance has a unique connection string.</span></span> <span data-ttu-id="5dd8a-122">So finden Sie die Verbindungszeichenfolge für eine Geräteinstanz in Ihrer Anwendung:</span><span class="sxs-lookup"><span data-stu-id="5dd8a-122">Here is how to find the connection string for a device instance in your application:</span></span>

1.  <span data-ttu-id="5dd8a-123">Klicken Sie im Gerätebildschirm für Ihre echte verbundene Kaffeemaschine auf **Connect this device** (Dieses Gerät verbinden).</span><span class="sxs-lookup"><span data-stu-id="5dd8a-123">On the device screen for your Connected Coffee Machine Real, choose **Connect this device**.</span></span>

1.  <span data-ttu-id="5dd8a-124">Kopieren Sie auf der Seite **Verbinden** den Wert für **Primäre Verbindungszeichenfolge**, und speichern Sie ihn.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-124">On the **Connect** page, copy the **Primary connection string**, and save it.</span></span> <span data-ttu-id="5dd8a-125">Dieser Wert wird in der auf dem Gerät ausgeführten Clientanwendung verwendet.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-125">You use this value in the client application that runs on the device.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="5dd8a-126">Erstellen einer Node.js-Anwendung</span><span class="sxs-lookup"><span data-stu-id="5dd8a-126">Create a Node.js application</span></span>
<span data-ttu-id="5dd8a-127">In den folgenden Schritten wird gezeigt, wie Sie eine Clientanwendung zur Implementierung der Kaffeemaschine erstellen, die Sie der Anwendung hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-127">The following steps show you how to create a client application that implements the coffee machine you added to the application.</span></span>
1. <span data-ttu-id="5dd8a-128">Installieren Sie auf Ihrem Computer mindestens die Version 4.0.x von [Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="5dd8a-128">Install [Node.js](https://nodejs.org/) version 4.0.x or later on your machine.</span></span> <span data-ttu-id="5dd8a-129">Node.js ist für eine Vielzahl von Betriebssystemen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-129">Node.js is available for a wide variety of operating systems.</span></span>

1. <span data-ttu-id="5dd8a-130">Erstellen Sie auf Ihrem Computer den Ordner „coffee-maker“.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-130">Create a folder called coffee-maker on your machine.</span></span> <span data-ttu-id="5dd8a-131">Navigieren Sie in der Befehlszeilenumgebung zu diesem Ordner.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-131">Navigate to that folder in your command-line environment.</span></span>

1. <span data-ttu-id="5dd8a-132">Führen Sie die folgenden Befehle aus, um das Node.js-Projekt zu initialisieren:</span><span class="sxs-lookup"><span data-stu-id="5dd8a-132">To initialize your Node.js project, run the following commands:</span></span>
    ```cmd/sh
    npm init
    ```
    > [!NOTE]
    > <span data-ttu-id="5dd8a-133">Das Initialisierungsskript fordert Sie zur Eingabe von Projekteigenschaften auf.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-133">The init script prompts you to enter project properties.</span></span> <span data-ttu-id="5dd8a-134">Verwenden Sie für diese Übung die Standardwerte.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-134">For this exercise, using the default values is sufficient and recommended.</span></span> 
1. <span data-ttu-id="5dd8a-135">Führen Sie den folgenden Befehl aus, um die erforderlichen Pakete zu installieren:</span><span class="sxs-lookup"><span data-stu-id="5dd8a-135">To install the necessary packages, run the following command:</span></span>
    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="5dd8a-136">Erstellen Sie im Ordner „coffee-maker“ mithilfe eines Text-Editors eine Datei namens „coffeeMaker.js“.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-136">Using a text editor, create a file called coffeeMaker.js in the coffee-maker folder.</span></span>

1. <span data-ttu-id="5dd8a-137">Kopieren Sie den Code in die Datei „coffeeMaker.js“, und klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-137">Copy and paste the code into your coffeeMaker.js file and **Save**.</span></span>

    <span data-ttu-id="5dd8a-138">Der Code, der in dieser Einheit die echte Kaffeemaschine darstellt, ist in Node.js geschrieben.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-138">The code, representing the real coffee machine in this unit, is written in Node.js.</span></span> <span data-ttu-id="5dd8a-139">Sie stellen zunächst eine Verbindung mit der Anwendung her, senden die ersten Eigenschaften an Azure IoT Central, synchronisieren die Einstellungen, registrieren zwei Befehlshandler für Wartung und Brühvorgang und starten schließlich den Timer, sodass Telemetriedaten im Sekundentakt gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-139">You begin by establishing connection with the application, then you send initial properties to Azure IoT Central, synchronize the settings, register two command handlers for Maintenance and Brewing, and finally start the timer for sending the telemetry information every second.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5dd8a-140">Aktualisieren Sie den Platzhalter `{your device connection string}`.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-140">Update the placeholder `{your device connection string}`.</span></span> 


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

1.  <span data-ttu-id="5dd8a-141">Ersetzen Sie den Platzhalter „{your device connection string}“ durch die Verbindungszeichenfolge Ihres Geräts.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-141">Update the placeholder {your device connection string} with your device connection string.</span></span> <span data-ttu-id="5dd8a-142">Diesen Wert haben Sie auf der Seite mit den Verbindungsdetails kopiert, als Sie Ihr echtes Gerät hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-142">You copied this value from the connection details page when you added your real device.</span></span> 

## <a name="run-your-nodejs-application"></a><span data-ttu-id="5dd8a-143">Ausführen der Node.js-Anwendung</span><span class="sxs-lookup"><span data-stu-id="5dd8a-143">Run your Node.js application</span></span>
```cmd/sh
node coffeeMaker.js
```

## <a name="summary"></a><span data-ttu-id="5dd8a-144">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="5dd8a-144">Summary</span></span>
<span data-ttu-id="5dd8a-145">In dieser Einheit haben Sie Ihre Kaffeemaschine mit Azure IoT Central verbunden und damit begonnen, Daten zur Überwachung und Analyse zu senden.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-145">In this unit, you connected your coffee machine to Azure IoT Central and began sending data for monitoring and analysis.</span></span> <span data-ttu-id="5dd8a-146">Zur Verbindungsherstellung haben Sie zuerst eine Verbindungszeichenfolge aus IoT Central abgerufen und sie anschließend für die Kaffeemaschine konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-146">You achieved the connectivity by first acquiring a connection string from IoT Central, followed by configuring the string in the coffee machine.</span></span>
