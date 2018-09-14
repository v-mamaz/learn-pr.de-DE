In dieser Übung erstellen Sie ein neues Speicherkonto für Ihr Azure-Abonnement. Verwenden Sie anschließend Azure Cloud Shell, um eine neue Warteschlange zu erstellen, eine Nachricht hinzuzufügen und diese dann zu lesen und aus der Warteschlange zu entfernen.

Hierbei handelt es sich um die gleichen Aktionen, die von Komponenten in einer verteilten Anwendung durchgeführt werden. Beispielsweise kann eine mobile App einer Warteschlange eine Nachricht hinzufügen, die dann darauf wartet, dass ein Webdienst sie abruft und verarbeitet.

## <a name="create-a-storage-account"></a>Erstellen eines Speicherkontos

Da Azure Storage-Warteschlangen ein Bestandteil von universellen Azure-Speicherkonten ist, müssen Sie zunächst ein Speicherkonto erstellen:

1. Navigieren Sie in einem Browser zum [Azure-Portal](http://portal.azure.com), und melden Sie sich mit Ihren regulären Anmeldeinformationen an.
1. Klicken Sie oben links auf **Alle Dienste**.
1. Scrollen Sie nach unten zum Abschnitt **Speicher**, und klicken Sie dann auf **Speicherkonten**.
1. Klicken Sie oben links auf dem Blatt **Speicherkonten** auf **Hinzufügen**.

    ![Screenshot: Blatt „Speicherkonten“ mit Hervorhebung der Option „Hinzufügen“](../images/5-create-a-storage-account-1.png)

1. Geben Sie im Textfeld **Name** einen eindeutigen Namen für das Speicherkonto ein.
1. Stellen Sie unter **Bereitstellungsmodell** sicher, dass **Resource Manager** ausgewählt ist.
1. Wählen Sie in der Dropdownliste **Kontoart** die Option **StorageV2 (universell, Version 2)** aus.
1. Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.
1. Wählen Sie in der Dropdownliste **Replikation** den Wert **Lokal redundanter Speicher** aus.
1. Wählen Sie unter **Leistung** die Option **Standard** aus.
1. Wählen Sie unter **Zugriffsebene** die Option **Kalt** aus.
1. Klicken Sie unter **Sichere Übertragung erforderlich** auf die Option **Deaktiviert**.
1. Wählen Sie unter **Abonnement** Ihr Abonnement aus.

    ![Screenshot: Dialogfeld „Speicherkonto erstellen“](../images/5-create-a-storage-account-2.png)

1. Klicken Sie unter **Ressourcengruppe** auf die Option **Neu erstellen**. Geben Sie **MusicSharingResourceGroup** in das Textfeld ein.
1. Wählen Sie unter **Virtuelle Netzwerke** die Option **Deaktiviert** aus, und klicken Sie dann auf **Erstellen**.

    ![Screenshot: Dialogfeld „Speicherkonto erstellen“ mit Hervorhebung der Option „Erstellen“](../images/5-create-a-storage-account-3.png)

Azure erstellt das neue Speicherkonto und die neue Ressourcengruppe.

## <a name="create-a-queue"></a>Erstellen einer Warteschlange

Nun ist das Speicherkonto erstellt, und Sie können eine neue Warteschlange hinzufügen. Sie müssen die Warteschlange mit PowerShell-Befehlen erstellen:

1. Klicken Sie in der oberen rechten Ecke des Portals auf den Link **Cloud Shell**.

    ![Screenshot: Azure-Portal mit Hervorhebung des Symbols „Cloud Shell“](../images/5-create-a-storage-queue-1.png)

1. Klicken Sie im Bildschirm **Willkommen bei Azure Cloud Shell** auf **PowerShell (Linux)**.
1. Wenn der Bildschirm **Sie haben keinen Speicher bereitgestellt** angezeigt wird, klicken Sie auf **Speicher erstellen**.
1. Wenn die `PS Azure`-Eingabeaufforderung angezeigt wird, geben Sie den folgenden Befehl ein, um das Speicherkonto aufzurufen. Ersetzen Sie `<storageaccountname>` durch den eindeutigen Namen Ihres Speicherkontos, und drücken Sie dann die EINGABETASTE:

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um den Kontext des Speicherkontos abzurufen:

    ```powershell
    $context = $storageaccount.Context
    ```

1. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um eine neue Warteschlange zu erstellen:

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a>Hinzufügen einer Nachricht zu einer Warteschlange

Da Sie nun eine Warteschlange im Speicherkonto erstellt haben, können Sie ihr eine Nachricht hinzufügen.

1. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um eine neue Nachricht zu erstellen:

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um die neue Nachricht der neuen Warteschlange hinzuzufügen:

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

1. Klicken Sie im Azure-Portal im Navigationsbereich auf der linken Seite auf **Alle Ressourcen**.
1. Klicken Sie in der Liste der Ressourcen auf das Speicherkonto, das Sie zuvor erstellt haben.
1. Klicken Sie im Speicherkontoblatt auf **Storage-Explorer (Vorschau)**.
1. Klicken Sie im Storage-Explorer unter **WARTESCHLANGEN** auf **musicsharingmessages**. Der Storage-Explorer zeigt die Nachricht an, die Sie gerade hinzugefügt haben.

## <a name="retrieve-and-remove-the-message"></a>Abrufen und Entfernen der Nachricht

Zielkomponenten für eine Nachricht in einer Speicherwarteschlange müssen die Nachricht abrufen, die sich am Anfang der Warteschlange befindet. Anschließend muss die Zielkomponente die Nachricht verarbeiten und aus der Warteschlange löschen, damit andere Komponenten diese nicht abrufen.

1. Geben Sie den folgenden Befehl in Cloud Shell ein, und drücken Sie dann die EINGABETASTE, um die Nachricht am Anfang der Warteschlange abzurufen:

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um die Nachricht anzuzeigen:

    ```powershell
    $retrievedMessage.AsString
    ```

1. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um alle Eigenschaften der Nachricht anzuzeigen:

    ```powershell
    $retrievedMessage
    ```

1. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um die Nachricht aus der Warteschlange zu entfernen:

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. Navigieren Sie im Azure-Portal zum Blatt „Speicherkonto“, um die Warteschlangenanzeige zu aktualisieren. Klicken Sie auf **Übersicht**, und klicken Sie dann auf **Storage-Explorer**.
1. Klicken Sie unter **WARTESCHLANGEN** auf **musicsharingmessages**. Der Storage-Explorer zeigt an, dass die Warteschlange leer ist, da Sie die einzige Nachricht entfernt haben.

## <a name="cleanup"></a>Bereinigen

Geben Sie den folgenden Befehl in Cloud Shell ein, um alle im Rahmen dieser Übung erstellten Ressourcen zu entfernen: 
```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```


## <a name="summary"></a>Zusammenfassung

Sie haben ein Speicherkonto in Ihrem Azure-Abonnement erstellt und darin eine neue Warteschlange. Außerdem haben Sie PowerShell verwendet, um die Aktionen von verteilten Anwendungskomponenten zu simulieren, indem Sie der Warteschlange eine Nachricht hinzugefügt und diese anschließend abgerufen und entfernt haben.

Warteschlangen für Speicherkonten sind eine gute Lösung, wenn Nachrichten zwischen den Komponenten einer verteilten Anwendung übergeben werden sollen. Verwenden Sie keine Speicherwarteschlangen, wenn Sie Ereignisse veröffentlichen möchten.