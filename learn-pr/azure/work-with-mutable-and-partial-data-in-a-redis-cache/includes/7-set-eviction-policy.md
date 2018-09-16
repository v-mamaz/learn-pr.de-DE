<span data-ttu-id="2c944-101">Hier fügen Sie dem Azure Redis Cache eine Entfernungsrichtlinie hinzu.</span><span class="sxs-lookup"><span data-stu-id="2c944-101">Here you'll add an eviction policy to our Azure Redis Cache.</span></span>

## <a name="set-an-eviction-policy"></a><span data-ttu-id="2c944-102">Festlegen einer Entfernungsrichtlinie</span><span class="sxs-lookup"><span data-stu-id="2c944-102">Set an eviction policy</span></span>

<span data-ttu-id="2c944-103">Um eine Entfernungsrichtlinie in Azure festzulegen, verwenden wir einfach ein Dropdownmenü im Portal.</span><span class="sxs-lookup"><span data-stu-id="2c944-103">To set an eviction policy in Azure, we simply use a drop-down menu in the portal.</span></span>

1. <span data-ttu-id="2c944-104">Öffnen Sie Ihren Redis Cache im Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="2c944-104">Open your Redis Cache in the Azure portal.</span></span>

1. <span data-ttu-id="2c944-105">Wählen Sie das Blatt **Erweiterte Einstellungen** aus.</span><span class="sxs-lookup"><span data-stu-id="2c944-105">Select the **Advanced settings** blade.</span></span>

1. <span data-ttu-id="2c944-106">Verwenden Sie das **maxmemory-policy**-Dropdownmenü, und wählen Sie **allkeys-random** aus.</span><span class="sxs-lookup"><span data-stu-id="2c944-106">Use the **maxmemory-policy** drop-down menu and select **allkeys-random**.</span></span>

1. <span data-ttu-id="2c944-107">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="2c944-107">Click **Save**.</span></span> 

<span data-ttu-id="2c944-108">Wenn Ihnen nun der Speicherplatz ausgeht, wählt Redis einen zufälligen Schlüssel zum Löschen aus, um Platz für Ihre neuen Daten zu schaffen.</span><span class="sxs-lookup"><span data-stu-id="2c944-108">At this point, if you run out of memory, Redis will select a random key to delete to make room for your new data.</span></span>