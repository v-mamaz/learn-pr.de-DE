<span data-ttu-id="64f90-101">Sie haben nun sowohl die Azure IoT Central-Anwendung verwendet als auch die Kaffeemaschine mit Azure IoT Central verbunden.</span><span class="sxs-lookup"><span data-stu-id="64f90-101">You’ve now worked with the Azure IoT Central application and connected the coffee machine to Azure IoT Central.</span></span> <span data-ttu-id="64f90-102">Das heißt, Sie können bald mit der Überwachung und Verwaltung Ihrer Remote-Kaffeemaschine beginnen.</span><span class="sxs-lookup"><span data-stu-id="64f90-102">You are well on your way to begin to monitor and manage your remote coffee machine.</span></span> <span data-ttu-id="64f90-103">In dieser Einheit überprüfen Sie Ihr Setup und die Verbindung unter Verwendung der zuvor definierten Vorlage „Connected Coffee Maker“ (Verbundene Kaffeemaschine).</span><span class="sxs-lookup"><span data-stu-id="64f90-103">In this unit, you take a moment to validate your setup and connection by using the Connected Coffee Maker template that you defined earlier.</span></span> <span data-ttu-id="64f90-104">Sie aktualisieren die optimale Temperatur in den Einstellungen, führen Befehle zur Überprüfung des Zustands der Maschine aus und sehen sich Ihre verbundene Kaffeemaschine auf dem Dashboard an.</span><span class="sxs-lookup"><span data-stu-id="64f90-104">You update the optimal temperature in settings, run commands to check for the state of your machine, and view your connected coffee machine in the dashboard.</span></span> 

## <a name="update-settings-to-sync-your-application-with-the-coffee-machine"></a><span data-ttu-id="64f90-105">Aktualisieren von Einstellungen, um Ihre Anwendung mit der Kaffeemaschine zu synchronisieren</span><span class="sxs-lookup"><span data-stu-id="64f90-105">Update settings to sync your application with the coffee machine</span></span>

<span data-ttu-id="64f90-106">Auf der Seite **Einstellungen** senden Sie Konfigurationsdaten von Ihrer Anwendung an die Kaffeemaschine.</span><span class="sxs-lookup"><span data-stu-id="64f90-106">On the **Settings** page, you send configuration data to the coffee machine from your application.</span></span> 

<span data-ttu-id="64f90-107">In diesem Szenario ändern Sie die optimale Temperatur und klicken anschließend auf **Aktualisieren**.</span><span class="sxs-lookup"><span data-stu-id="64f90-107">In this scenario, change the optimal temperature and choose **Update**.</span></span> <span data-ttu-id="64f90-108">Die geänderte Einstellung wird auf der Benutzeroberfläche als ausstehend markiert, bis die Kaffeemaschine bestätigt, dass sie auf die Einstellungsänderung reagiert hat.</span><span class="sxs-lookup"><span data-stu-id="64f90-108">When the setting is changed, the setting is marked as pending in the UI until the coffee machine acknowledges that it has responded to the setting change.</span></span> 

> [!NOTE]
> <span data-ttu-id="64f90-109">Die erfolgreiche Einstellungsänderung zeigt, dass der Datenfluss und somit die Verbindung funktioniert.</span><span class="sxs-lookup"><span data-stu-id="64f90-109">Successful updates in the setting indicate data flow and validate your  connection.</span></span> <span data-ttu-id="64f90-110">Die Telemetriemessungen reagieren auf das Update der optimalen Temperatur.</span><span class="sxs-lookup"><span data-stu-id="64f90-110">The telemetry measurements will respond to the update in optimal temperature.</span></span> <span data-ttu-id="64f90-111">Die Änderung kann auf der Seite mit den **Messungen** beobachtet werden.</span><span class="sxs-lookup"><span data-stu-id="64f90-111">You can observe the change on the **Measurements** page.</span></span> 

## <a name="run-commands-on-the-coffee-machine"></a><span data-ttu-id="64f90-112">Ausführen von Befehlen für die Kaffeemaschine</span><span class="sxs-lookup"><span data-stu-id="64f90-112">Run commands on the coffee machine</span></span> 
<span data-ttu-id="64f90-113">Navigieren Sie für die folgende Übung zur Seite **Befehle**.</span><span class="sxs-lookup"><span data-stu-id="64f90-113">Navigate to the **Commands** page for the following exercise.</span></span> <span data-ttu-id="64f90-114">Zur Überprüfung des Befehlssetups führen Sie über IoT Central Remotebefehle für die Kaffeemaschine aus.</span><span class="sxs-lookup"><span data-stu-id="64f90-114">To validate the commands setup, you remotely run commands on the coffee machine from IoT Central.</span></span> <span data-ttu-id="64f90-115">Nach erfolgreicher Ausführung der Befehle sendet die Kaffeemaschine Bestätigungsmeldungen.</span><span class="sxs-lookup"><span data-stu-id="64f90-115">If the commands are successful, confirmation messages are sent from the coffee machine.</span></span>

1. <span data-ttu-id="64f90-116">Klicken Sie auf **Ausführen**, um per Remotezugriff einen Brühvorgang zu starten.</span><span class="sxs-lookup"><span data-stu-id="64f90-116">Start brewing remotely by choosing **Run**.</span></span> 
    
    <span data-ttu-id="64f90-117">Die Kaffeemaschine startet den Vorgang, wenn die drei folgenden Bedingungen erfüllt sind:</span><span class="sxs-lookup"><span data-stu-id="64f90-117">The coffee machine will start if these three conditions are satisfied:</span></span>
    - <span data-ttu-id="64f90-118">Tasse erkannt</span><span class="sxs-lookup"><span data-stu-id="64f90-118">Cup detected</span></span>
    - <span data-ttu-id="64f90-119">Nicht im Wartungsmodus</span><span class="sxs-lookup"><span data-stu-id="64f90-119">Not in maintenance</span></span>
    - <span data-ttu-id="64f90-120">Noch kein Brühvorgang gestartet</span><span class="sxs-lookup"><span data-stu-id="64f90-120">Not brewing already</span></span>  

    > [!NOTE]
    > <span data-ttu-id="64f90-121">Nach erfolgreichem Start des Brühvorgangs wechselt der Zustand der Maschine unter **Measurements** > **State** (Messungen > Zustand) zu gelb.</span><span class="sxs-lookup"><span data-stu-id="64f90-121">When you've successfully started brewing, the state of the machine changes to yellow as indicated in **Measurements** > **State**.</span></span> 
    
    <span data-ttu-id="64f90-122">Prüfen Sie das Konsolenprotokoll der simulierten Node.js-Kaffeemaschine auf Bestätigungsmeldungen.</span><span class="sxs-lookup"><span data-stu-id="64f90-122">Look for confirmation messages in the console log on the node.js simulated coffee machine.</span></span> 

    ![Ausführen von Befehlen](../media/4-commands-brewing.png)

1. <span data-ttu-id="64f90-124">Klicken Sie auf **Ausführen**, um den Wartungsmodus festzulegen.</span><span class="sxs-lookup"><span data-stu-id="64f90-124">Set maintenance mode by choosing **Run**.</span></span> <span data-ttu-id="64f90-125">Die Kaffeemaschine wird in den Wartungsmodus versetzt, sofern Sie sich *nicht* bereits im Wartungsmodus befindet.</span><span class="sxs-lookup"><span data-stu-id="64f90-125">The coffee machine will set to maintenance if it's *not* already in maintenance.</span></span>
    
    <span data-ttu-id="64f90-126">Prüfen Sie das Konsolenprotokoll der Kaffeemaschine auf Bestätigungsmeldungen.</span><span class="sxs-lookup"><span data-stu-id="64f90-126">Look for confirmation messages in the console log on the coffee machine.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="64f90-127">Die Kaffeemaschine bleibt im Wartungsmodus, bis Sie den Clientcode neu starten – genau wie in der Realität, wenn ein Techniker die Maschine offline schaltet, um notwendige Reparaturen durchzuführen, und sie anschließend wieder online schaltet.</span><span class="sxs-lookup"><span data-stu-id="64f90-127">As in real life, when the technician takes the machine offline to perform necessary repairs before switching it back online, the coffee machine continues to stay in the maintenance mode until you reboot the client code.</span></span>

    ![Ausführen von Befehlen](../media/4-commands-maintenance.png)

> [!IMPORTANT]
> <span data-ttu-id="64f90-129">Es empfiehlt sich, die Node.js-Anwendung nicht länger als etwa 60 Minuten auszuführen, um zu verhindern, dass Sie von der Anwendung unerwünschte Benachrichtigungen/E-Mails erhalten.</span><span class="sxs-lookup"><span data-stu-id="64f90-129">It's recommended that you run the Node.js application no more than 60 minutes or so to prevent the application from sending you unwanted notifications/emails.</span></span> <span data-ttu-id="64f90-130">Außerdem empfiehlt es sich, die Anwendung zu beenden, um das tägliche Nachrichtenkontingent nicht aufzubrauchen, wenn Sie nicht an dem Modul arbeiten.</span><span class="sxs-lookup"><span data-stu-id="64f90-130">Stopping the application when you're not working on the module also prevents you from exhausting the daily message quota.</span></span>

## <a name="view-the-coffee-machine-in-the-dashboard"></a><span data-ttu-id="64f90-131">Anzeigen der Kaffeemaschine auf dem Dashboard</span><span class="sxs-lookup"><span data-stu-id="64f90-131">View the coffee machine in the dashboard</span></span>

1. <span data-ttu-id="64f90-132">Navigieren Sie zur Registerkarte **Dashboard** .</span><span class="sxs-lookup"><span data-stu-id="64f90-132">Navigate to the **Dashboard** tab.</span></span>

1. <span data-ttu-id="64f90-133">Klicken Sie auf **Vorlage bearbeiten**, um das Dashboard zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="64f90-133">Select **Edit Template** to edit the dashboard.</span></span>

1. <span data-ttu-id="64f90-134">Wählen Sie aus dem seitlichen Menü **Liniendiagramm** aus.</span><span class="sxs-lookup"><span data-stu-id="64f90-134">Choose **Line Chart** from the side menu.</span></span>

1. <span data-ttu-id="64f90-135">Geben Sie unter **Configure Chart** (Diagramm konfigurieren) in das Feld **Titel** `Telemetry` ein.</span><span class="sxs-lookup"><span data-stu-id="64f90-135">In **Configure Chart**  enter `Telemetry` in the **Title** field.</span></span> <span data-ttu-id="64f90-136">Zeigen Sie die Telemetriedaten mit diesem Diagramm an.</span><span class="sxs-lookup"><span data-stu-id="64f90-136">We'll view our telemetry data with this chart.</span></span> 

1. <span data-ttu-id="64f90-137">Wählen Sie unter **Zeitbereich** die Option **Past 30 minutes** (Letzte 30 Minuten) aus.</span><span class="sxs-lookup"><span data-stu-id="64f90-137">Select **Past 30 minutes** for **Time Range**.</span></span> 

1. <span data-ttu-id="64f90-138">Klicken Sie im Bereich **Measures** auf das Sichtbarkeitssymbol jeweils rechts neben jeder Messung, um diese für unser Diagramm sichtbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="64f90-138">In the **Measures** area, select the visibility icon to the right of each measurement to make that measurement visible for our chart.</span></span> 

1. <span data-ttu-id="64f90-139">Klicken Sie auf **Speichern**, um die Konfiguration zu speichern und das Liniendiagramm anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="64f90-139">Select **Save** to save our configuration and display the line chart.</span></span> 

    ![Anzeigen des Dashboards](../media/4-dashboard-a.png)

1. <span data-ttu-id="64f90-141">Klicken Sie im linken Menü auf **Settings and Properties** (Einstellungen und Eigenschaften), um den Bereich **Configure Device Details** (Gerätedetails konfigurieren) zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="64f90-141">Choose **Settings and Properties** in the left-hand menu to open the **Configure Device Details** panel.</span></span> 

1. <span data-ttu-id="64f90-142">Geben Sie in das Feld **Titel** `Device properties` ein.</span><span class="sxs-lookup"><span data-stu-id="64f90-142">Enter `Device properties` in the **Title** filed.</span></span>

1. <span data-ttu-id="64f90-143">Wählen Sie unter **Hinzufügen/Entfernen** die Optionen **Coffee Makers Max Temperature** (Höchste Kaffeemaschinentemperatur), **Coffee Makers Min Temperature** (Niedrigste Kaffeemaschinentemperatur), **Device Warranty Expired** (Gerätegarantie abgelaufen) und dann **OK** aus.</span><span class="sxs-lookup"><span data-stu-id="64f90-143">In **Add/Remove**, choose **Coffee Makers Max Temperature**, **Coffee Makers Min Temperature**, **Device Warranty Expired** and then select **OK** to complete the selection.</span></span>

1. <span data-ttu-id="64f90-144">Klicken Sie auf **Speichern**, um das neue Panel *Geräteeigenschaften* im Dashboard zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="64f90-144">Select **Save** to create a new *Device properties* panel in our dashboard.</span></span> 

1. <span data-ttu-id="64f90-145">Klicken Sie noch einmal auf **Settings and Properties** (Einstellungen und Eigenschaften), und geben Sie `Optimal Temperature` als Titel ein.</span><span class="sxs-lookup"><span data-stu-id="64f90-145">Choose **Settings and Properties** again,  and enter `Optimal Temperature` as the title.</span></span> <span data-ttu-id="64f90-146">Wählen Sie unter **Hinzufügen/Entfernen** die Option **Optimal Temperature** (Optimale Temperatur) aus.</span><span class="sxs-lookup"><span data-stu-id="64f90-146">In **Add/Remove**, choose **Optimal  Temperature**.</span></span>

1. <span data-ttu-id="64f90-147">Klicken Sie auf **Speichern**, um Ihre Arbeit zu speichern und einen neuen Bereich im Dashboard anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="64f90-147">Select **Save** to save your work and display a new pane in our dashboard.</span></span> 

1. <span data-ttu-id="64f90-148">Klicken Sie auf **Fertig**, um den Bearbeitungsmodus zu beenden und das neue Dashboard anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="64f90-148">Select **Done** to exit edit mode and display the new dashboard.</span></span> 