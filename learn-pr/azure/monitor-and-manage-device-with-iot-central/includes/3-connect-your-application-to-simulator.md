[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="cfdc2-101">In dieser Übung stellen Sie eine Verbindung zwischen Azure IoT Central und einem physischen Gerät her, in diesem Fall mit einer IoT-fähigen Kaffeemaschine.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-101">In practice, you will connect Azure IoT Central to a physical device, i.e. an IoT enabled coffee machine.</span></span> <span data-ttu-id="cfdc2-102">Hier simulieren Sie ein Gerät mithilfe einer Node.js-Anwendung und verbinden es mit der Azure IoT Central-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-102">Here, you'll simualate a device with a Node.js applicatio and connect it to the Azure IoT Central application.</span></span> <span data-ttu-id="cfdc2-103">Die gemessenen Telemetriedaten der simulierten Kaffeemaschine werden zur Überwachung und Analyse an IoT Central gesendet.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-103">Telemetry measurements from the simulated coffee machine are sent to IoT Central for monitoring and analysis.</span></span>

![Illustration einer Kaffeemaschine](../media/3-coffee-machine.png) 

## <a name="add-the-coffee-machine-in-iot-central"></a><span data-ttu-id="cfdc2-105">Hinzufügen der Kaffeemaschine in IoT Central</span><span class="sxs-lookup"><span data-stu-id="cfdc2-105">Add the coffee machine in IoT Central</span></span> 
<span data-ttu-id="cfdc2-106">Um die Kaffeemaschine zu Ihrer Anwendung hinzuzufügen, verwenden Sie die Gerätevorlage **Connected Coffee Maker**, die Sie in der vorherigen Einheit erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-106">To add your coffee machine to your application, you use the **Connected Coffee Maker** device template you created in the previous unit.</span></span>

1. <span data-ttu-id="cfdc2-107">Klicken Sie im linken Navigationsmenü auf **Device Explorer**, um ein neues Gerät hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-107">To add a new device, choose **Device Explorer** in the left navigation menu.</span></span>

    <span data-ttu-id="cfdc2-108">Klicken Sie zum Herstellen einer Verbindung für die Kaffeemaschine auf **+ Neu**, **Real** und anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-108">To start connecting your coffee machine, choose **+ New**, **Real**, and then **Create**.</span></span> <span data-ttu-id="cfdc2-109">Daraufhin wird eine Liste mit Geräten angezeigt, die Sie unter Verwendung der Vorlage „Connected Coffee Maker“ (Verbundene Kaffeemaschine) erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-109">When you're finished, you see a list of devices you've created using the same Connected Coffee Maker template.</span></span>
   
    *   <span data-ttu-id="cfdc2-110">Die verbundene Kaffeemaschine wird der Liste hinzugefügt, wenn Sie auf **+ Neu** und dann auf **Real** klicken.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-110">The Connected Coffee Maker is added to the list when you choose **+ New** and then **Real**.</span></span> 
    *   <span data-ttu-id="cfdc2-111">Die simulierte verbundene Kaffeemaschine wird von IoT Central automatisch zu Testzwecken erstellt.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-111">The Connected Coffee Maker (Simulate) is automatically created by IoT Central for testing purposes.</span></span> 

1.  <span data-ttu-id="cfdc2-112">Zur Unterscheidung können Sie den Namen der neu hinzugefügten Kaffeemaschine optional mit dem Suffix „Real“ versehen.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-112">Optionally, you can differentiate the newly added coffee machine by appending the word “Real” in its name.</span></span> <span data-ttu-id="cfdc2-113">Klicken Sie zum Umbenennen des neuen Geräts auf das Gerät, und bearbeiten Sie den Namen im Namensfeld.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-113">To rename your new device, choose the device and edit the name in the name field.</span></span> 

    ![Kaffeemaschine](../media/3-connect-device-a.png) 

    <span data-ttu-id="cfdc2-115">Beachten Sie die Position von **Connect this device** (Dieses Gerät verbinden) für das Verbinden Ihrer Kaffeemaschine im nächsten Abschnitt.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-115">Note the location of **Connect this device** for connecting your coffee machine in the next section.</span></span> <span data-ttu-id="cfdc2-116">Vorerst wird angezeigt, dass Daten fehlen, da Sie noch keine Verbindung mit der Kaffeemaschine hergestellt haben.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-116">For now, the screen displays "Missing Data" because you haven't connected to the coffee machine.</span></span> <span data-ttu-id="cfdc2-117">Der Bildschirm wird mit echten Telemetriedaten gefüllt, sobald die Verbindung hergestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-117">The real telemetry begins to populate the screen once the connection is made.</span></span> 
 
## <a name="generate-connection-string-for-the-coffee-machine-from-your-application"></a><span data-ttu-id="cfdc2-118">Generieren der Verbindungszeichenfolge für die Kaffeemaschine über Ihre Anwendung</span><span class="sxs-lookup"><span data-stu-id="cfdc2-118">Generate connection string for the coffee machine from your application</span></span>
<span data-ttu-id="cfdc2-119">Die Verbindungszeichenfolge für Ihre echte Kaffeemaschine wird in den Code eingebettet, der auf dem Gerät ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-119">You embed the connection string for your real coffee machine in the code that runs on the device.</span></span> <span data-ttu-id="cfdc2-120">Mit der Verbindungszeichenfolge kann die Kaffeemaschine eine sichere Verbindung mit Ihrer Azure IoT Central-Anwendung herstellen.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-120">The connection string enables the coffee machine to connect securely to your Azure IoT Central application.</span></span> <span data-ttu-id="cfdc2-121">Jede Geräteinstanz besitzt eine eindeutige Verbindungszeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-121">Every device instance has a unique connection string.</span></span> <span data-ttu-id="cfdc2-122">In den nächsten Schritten generieren Sie die Verbindungszeichenfolge im Rahmen der Erstellung einer Node.js-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-122">In the next steps, you generate the connection string as part of creating your node.js application.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="cfdc2-123">Erstellen einer Node.js-Anwendung</span><span class="sxs-lookup"><span data-stu-id="cfdc2-123">Create a Node.js application</span></span>
<span data-ttu-id="cfdc2-124">In den folgenden Schritten wird gezeigt, wie Sie eine Clientanwendung zur Implementierung der Kaffeemaschine erstellen, die Sie der Anwendung hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-124">The following steps show you how to create a client application that implements the coffee machine you added to the application.</span></span>

> [!TIP]
> <span data-ttu-id="cfdc2-125">In dieser Übung erstellen Sie die App in Azure Cloud Shell, damit Sie nichts auf Ihrem lokalen Computer installieren müssen.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-125">In this exercise, we'll create the app in the Azure Cloud Shell so that you don't have to install anything on your local machine.</span></span> 

1. <span data-ttu-id="cfdc2-126">Führen Sie den folgenden Befehl in Azure Cloud Shell aus, um einen `coffee-maker`-Ordner zu erstellen und zu diesem zu navigieren:</span><span class="sxs-lookup"><span data-stu-id="cfdc2-126">Execute the following command in the Azure Cloud Shell to create a `coffee-maker` folder and navigate to it:</span></span>

    ```azurecli
    mkdir ~/coffee-maker
    cd ~/coffee-maker
    ```

1. <span data-ttu-id="cfdc2-127">Führen Sie den folgenden Befehl im `coffee-maker`-Ordner in Cloud Shell aus, um den DPS-Schlüsselgenerator zu installieren:</span><span class="sxs-lookup"><span data-stu-id="cfdc2-127">From the `coffee-maker` folder in Cloud Shell, execute the following command to install the DPS key generator:</span></span> 

   ```azurecli
    npm install dps-keygen
   ```
    <span data-ttu-id="cfdc2-128">Dieser Befehl installiert das Paket „dps-keygen“ im lokalen `coffee-maker`-Ordner.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-128">This command installs the dps-keygen package to our local folder, `coffee-maker`.</span></span> <span data-ttu-id="cfdc2-129">Die Option `-g` wird ausgelassen, da Sie über keine Berechtigungen für die Installation als globales Paket verfügen.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-129">We leave out the `-g` option because we don't have permissions to install as a global package.</span></span>

    <!-- TODO: Add more information about the DPS key generator and what it's used for -->
 
1. <span data-ttu-id="cfdc2-130">Führen Sie den folgenden Befehl in Cloud Shell aus, um das Hilfsprogramm für die DPS-Verbindungszeichenfolge von GitHub herunterzuladen:</span><span class="sxs-lookup"><span data-stu-id="cfdc2-130">Execute the following command in the Cloud Shell to download the DPS connection string utility from GitHub:</span></span> 

    ```azurecli
    wget https://github.com/Azure/dps-keygen/blob/master/bin/linux/dps_cstr?raw=true -O dps_cstr 
    ```

    > [!NOTE]
    > <span data-ttu-id="cfdc2-131">Mit diesem Befehl wird die Linux-Version von **dps_cstr** heruntergeladen, da diese Übung in Cloud Shell durchgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-131">We downloaded the Linux version of **dps_cstr** because we're running in the Cloud Shell.</span></span>

1. <span data-ttu-id="cfdc2-132">Führen Sie den folgenden Befehl aus, um `dps_cstr` die Ausführungsberechtigungen zu erteilen:</span><span class="sxs-lookup"><span data-stu-id="cfdc2-132">Execute the following command to give `dps_cstr` execute permissions:</span></span>

    ```azurecli
    chmod +x dps_cstr
    ```

    <span data-ttu-id="cfdc2-133">Sie benötigen drei Informationen aus dem Azure IoT Central-Portal, um eine Verbindungszeichenfolge für Ihr Gerät zu generieren:</span><span class="sxs-lookup"><span data-stu-id="cfdc2-133">To generate a connection string for our device, we need three pieces of information from the Azure IoT Central portal:</span></span>
    - <span data-ttu-id="cfdc2-134">**Bereichs-ID**</span><span class="sxs-lookup"><span data-stu-id="cfdc2-134">**Scope ID**</span></span>
    - <span data-ttu-id="cfdc2-135">**Geräte-ID**</span><span class="sxs-lookup"><span data-stu-id="cfdc2-135">**Device ID**</span></span>
    - <span data-ttu-id="cfdc2-136">**Primärschlüssel**</span><span class="sxs-lookup"><span data-stu-id="cfdc2-136">**Primary Key**</span></span>

1. <span data-ttu-id="cfdc2-137">Kehren Sie zum IoT Central-Portal zurück.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-137">Return to the IoT Central portal.</span></span> <span data-ttu-id="cfdc2-138">Klicken Sie auf dem Gerätebildschirm für das Gerät *Connected Coffee Maker - Real* (Verbundene Kaffeemaschine – Real) in der oberen rechten Ecke des Bildschirms auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-138">On the device screen for the *Connected Coffee Maker - Real* device, select **Connect** in the top right of the screen.</span></span>

1. <span data-ttu-id="cfdc2-139">Speichern Sie die Werte für die **Bereichs-ID**, die **Geräte-ID** und den **Primärschlüssel**, die im angezeigten Dialogfeld „Geräteverbindung“ angezeigt werden, da Sie sie im späteren Verlauf dieser Übung benötigen.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-139">On the Device Connection dialog that opens, save the values **Scope ID**, **Device ID** and **Primary Key** somewhere, because we'll use them later in this exercise.</span></span> 

1. <span data-ttu-id="cfdc2-140">Führen Sie den folgenden Befehl in Cloud Shell aus, und ersetzen Sie hierbei **<scope_id>**, **<device_id>** und **<primary_key>** durch die im vorherigen Schritt gespeicherten Werte.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-140">Execute the following command in the Cloud Shell, replacing **<scope_id>**, **<device_id>**, and **<primary_key>** with the values you saved in the last step.</span></span> 

   ```azurecli
   ./dps_cstr [scope_id] [device_id] [primary_key] > connection.txt
   ```
  
    <span data-ttu-id="cfdc2-141">Mit diesem Befehl wird eine Verbindungszeichenfolge basierend auf den Werten generiert, die Sie zugewiesen haben, und diese wird in eine Datei eingefügt, der Sie den Namen **connection.txt** gegeben haben.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-141">This command generates a connection string based on the values you gave it and writes them to a file that we've named **connection.txt**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="cfdc2-142">Der Befehl `dps_cstr` befindet sich in Ihrer PATH-Variable in der Shell.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-142">The command `dps_cstr` is not in your PATH in the shell.</span></span> <span data-ttu-id="cfdc2-143">Stellen Sie also sicher, dass Sie ihn mit `./dps_cstr` aufrufen.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-143">So, make sure to call it with `./dps_cstr`</span></span>

1. <span data-ttu-id="cfdc2-144">Öffnen Sie den integrierten Code-Editor in Cloud Shell, indem Sie den folgenden Befehl ausführen.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-144">Open the integrated code editor in the Cloud Shell by running the following command:</span></span> 

    ```azurecli
    code
    ```
1. <span data-ttu-id="cfdc2-145">Wählen Sie **connection.txt** in der Dateiliste des Menüs **FILES** des Editors aus.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-145">Select **connection.txt** from the list of files in the **FILES** menu of the editor.</span></span>

1. <span data-ttu-id="cfdc2-146">Stellen Sie sicher, dass **connection.txt** eine Verbindungszeichenfolge enthält, die mit ``HostName=`` beginnt.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-146">Verify that **connection.txt** contains a connection string that starts with ``HostName=``.</span></span>

1. <span data-ttu-id="cfdc2-147">Schließen Sie den Editor, indem Sie im Menü (*...*) oben rechts im Editor auf **Editor schließen** klicken.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-147">Close the editor by selecting **Close Editor** from the menu (*...*) at the top right of the editor.</span></span> 

1. <span data-ttu-id="cfdc2-148">Führen Sie den folgenden Befehl in Cloud Shell aus, um ein Node.js-Projekt im `coffee-maker`-Ordner zu initialisieren:</span><span class="sxs-lookup"><span data-stu-id="cfdc2-148">Execute the following command in the Cloud Shell to initialize a Node.js project in our `coffee-maker` folder:</span></span>

    ```azurecli
    npm init
    ```
    > [!NOTE]
    > <span data-ttu-id="cfdc2-149">Das Initialisierungsskript fordert Sie zur Eingabe von Projekteigenschaften auf.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-149">The init script prompts you to enter project properties.</span></span> <span data-ttu-id="cfdc2-150">Drücken Sie die EINGABETASTE, um für diese Übung alle Standardwerte zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-150">For this exercise, press ENTER to use all default values.</span></span>

1. <span data-ttu-id="cfdc2-151">Führen Sie den folgenden Befehl im `coffee-maker`-Ordner aus, um die erforderlichen Pakete zu installieren:</span><span class="sxs-lookup"><span data-stu-id="cfdc2-151">To install the necessary packages, run the following command in our `coffee-maker` folder:</span></span>

    ```azurecli
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="cfdc2-152">Führen Sie den folgenden Befehl aus, um eine neue Datei in Cloud Shell zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="cfdc2-152">Execute the following command to create a new file in the Cloud Shell:</span></span>

    ```azurecli
    touch coffeeMaker.js
    ```
1. <span data-ttu-id="cfdc2-153">Öffnen Sie den integrierten Code-Editor, indem Sie folgenden Befehl in der Befehlszeile in Cloud Shell ausführen:</span><span class="sxs-lookup"><span data-stu-id="cfdc2-153">Open the integrated code editor by executing the following at the command line in the Cloud Shell:</span></span> 

     ```azurecli
    code
    ```
    
1. <span data-ttu-id="cfdc2-154">Nachdem der Code-Editor geöffnet wurde, klicken Sie in der **FILES**-Liste auf die Schaltfläche zum Aktualisieren, und wählen Sie die neue Date **coffeeMaker.js** aus.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-154">When the code editor opens, select the refresh button on the **FILES** list and select our new file **coffeeMaker.js**.</span></span> 

1. <span data-ttu-id="cfdc2-155">Kopieren Sie den folgenden Code, und fügen Sie ihn in das leere Editorfenster ein:</span><span class="sxs-lookup"><span data-stu-id="cfdc2-155">Copy and paste the following code into the empty editor window:</span></span>

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

    <span data-ttu-id="cfdc2-156">Der Code der Kaffeemaschine für diese Übung ist in Node.js geschrieben.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-156">Our coffee machine is written in Node.js.</span></span> <span data-ttu-id="cfdc2-157">Zunächst wird eine Verbindung zu Azure IoT Central hergestellt.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-157">It first connects to Azure IoT Central.</span></span> <span data-ttu-id="cfdc2-158">Dann sendet die App die ersten Eigenschaften an Azure IoT Central, synchronisiert die Einstellungen, registriert zwei Befehlshandler für Wartung und Brühvorgang und startet letztendlich den Timer zum Senden von Telemetriedaten im Sekundentakt.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-158">Then the app sends initial properties to Azure IoT Central, synchronizes settings, registers two command handlers for maintenance and brewing, and finally starts the timer for sending the telemetry information every second.</span></span>

1.  <span data-ttu-id="cfdc2-159">Ersetzen Sie den Platzhalter `{your device connection string}` am Anfang des Codes durch die Verbindungszeichenfolge, die Sie zuvor erstellt und in der Datei **connection.txt** gespeichert haben.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-159">Update the placeholder `{your device connection string}` at the top of this code with the connection string you created earlier and saved in **connection.txt**.</span></span> <span data-ttu-id="cfdc2-160">Die Verbindungszeichenfolge beginnt mit `HostName=`.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-160">The connection string begins with `HostName=`.</span></span>

1. <span data-ttu-id="cfdc2-161">Klicken Sie oben rechts im Editor auf die drei Punkte (`...`), um das Editor-Menü zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-161">Select the three dots `...` to the top right of the editor to expand the editor menu.</span></span> <span data-ttu-id="cfdc2-162">Klicken Sie dann auf **Speichern**, um die Änderungen an „coffeeMaker.js“ zu speichern.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-162">Then select **Save** to save the edits we made to \`coffeeMaker.js'</span></span>

1. <span data-ttu-id="cfdc2-163">Führen Sie den folgenden Befehl im Cloud Shell-Fenster aus, um die App zu starten:</span><span class="sxs-lookup"><span data-stu-id="cfdc2-163">Execute the following command in the Cloud Shell window to start the app:</span></span>

    ```azurecli
    node coffeeMaker.js
    ```
1. <span data-ttu-id="cfdc2-164">Stellen Sie sicher, dass die App mit den Nachrichten *Device successfully connected to Azure IoT Central* (Gerät wurde erfolgreich mit Azure IoT Central verbunden) und *Telemetry send:* (Telemetriedaten senden:) gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-164">Verify that the app starts in the Cloud Shell window with the message *Device successfully connected to Azure IoT Central* along with *Telemetry send:* messages.</span></span> <span data-ttu-id="cfdc2-165">Herzlichen Glückwunsch!</span><span class="sxs-lookup"><span data-stu-id="cfdc2-165">Congratulations!</span></span> <span data-ttu-id="cfdc2-166">Ihre App ist in Betrieb und kommuniziert mit IoT Central.</span><span class="sxs-lookup"><span data-stu-id="cfdc2-166">Your app is up and running and communicating with IoT Central!</span></span>