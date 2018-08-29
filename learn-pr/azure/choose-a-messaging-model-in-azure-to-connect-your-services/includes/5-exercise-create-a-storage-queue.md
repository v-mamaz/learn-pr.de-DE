In dieser Übung erstellen Sie ein neues Speicherkonto in Ihrem Azure-Abonnement. Sie werden dann Azure Cloud Shell verwenden, um eine neue Warteschlange zu erstellen, eine Nachricht hinzuzufügen und dann diese Nachricht zu lesen und aus der Warteschlange zu entfernen.

Hierbei handelt es sich um die gleichen Aktionen, die von Komponenten in einer verteilten Anwendung durchgeführt werden. Beispielsweise kann eine mobile App einer Warteschlange eine Nachricht hinzufügen, die dann darauf wartet, dass ein Webdienst sie abruft und verarbeitet.

## <a name="create-a-storage-account"></a>Erstellen eines Speicherkontos

Speicherwarteschlangen gehören in Azure zu den Speicherkonten für allgemeine Zwecke. Sie müssen zunächst ein Speicherkonto erstellen:

1. Navigieren Sie in einem Browser zum [Azure-Portal](http://portal.azure.com), und melden Sie sich mit Ihren üblichen Anmeldeinformationen an.
1. Klicken Sie oben links auf **Alle Dienste**.
1. Scrollen Sie nach unten zum Abschnitt **Speicher**, und klicken Sie dann auf **Speicherkonten**.
1. Klicken Sie oben links auf dem Blatt **Speicherkonten** auf **Hinzufügen**.

    ![Erstellen eines Speicherkontos](../images/5-create-a-storage-account-1.png)

1. Geben Sie im Textfeld **Name** einen eindeutigen Namen für das Speicherkonto ein.
1. Stellen Sie unter **Bereitstellungsmodell** sicher, dass **Resource Manager** ausgewählt ist.
1. Wählen Sie in der Dropdownliste **Kontoart** die Option **StorageV2 (universell, Version 2)** aus.
1. Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.
1. Wählen Sie in der Dropdownliste **Replikation** den Wert **Lokal redundanter Speicher** aus.
1. Wählen Sie unter **Leistung** die Option **Standard** aus.
1. Wählen Sie unter **Zugriffsebene** die Option **Kalt** aus.
1. Wählen Sie unter **Sichere Übertragung erforderlich** die Option **Deaktiviert** aus.
1. Wählen Sie unter **Abonnement** Ihr Abonnement aus.

    ![Erstellen eines Speicherkontos](../images/5-create-a-storage-account-2.png)

1. Wählen Sie unter **Ressourcengruppe** die Option **Neu erstellen** aus, und klicken Sie dann im Textfeld auf den Typ **MusicSharingResourceGroup**.
1. Wählen Sie unter **Virtuelle Netzwerke** die Option **Deaktiviert** aus, und klicken Sie dann auf **Erstellen**.

    ![Erstellen eines Speicherkontos](../images/5-create-a-storage-account-3.png)

Azure erstellt das neue Speicherkonto und die neue Ressourcengruppe.

## <a name="create-a-queue"></a>Erstellen einer Warteschlange

Nun ist das Speicherkonto erstellt, und Sie können eine neue Warteschlange hinzufügen. Sie müssen die Warteschlange mit PowerShell-Befehlen erstellen:

1. Klicken Sie in der oberen rechten Ecke des Portals auf den Link **Cloud Shell**.

    ![Starten von Cloud Shell](../images/5-create-a-storage-queue-1.png)

1. Klicken Sie im Bildschirm **Willkommen bei Azure Cloud Shell** auf **PowerShell (Linux)**.
1. Klicken Sie auf dem Bildschirm **Sie haben keinen Speicher bereitgestellt** auf **Speicher erstellen**.
1. Wenn die `PS Azure`-Eingabeaufforderung angezeigt wird, geben Sie – um das Speicherkonto zu erhalten – den folgenden Befehl ein, wobei Sie `<storageaccountname>` durch den eindeutigen Namen Ihres Speicherkontos ersetzen, und drücken Sie dann die EINGABETASTE:

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. Um den Kontext des Speicherkontos zu erhalten, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

    ```powershell
    $context = $storageaccount.Context
    ```

1. Um eine neue Warteschlange zu erstellen, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a>Hinzufügen einer Nachricht zur Warteschlange

Da Sie nun eine Warteschlange im Speicherkonto erstellt haben, können Sie ihr eine Nachricht hinzufügen.

1. Um eine neue Nachricht zu erstellen, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. Um der Warteschlange eine neue Nachricht hinzuzufügen, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

1. Klicken Sie im Azure-Portal in der Navigation auf der linken Seite auf **Alle Ressourcen**.
1. Klicken Sie in der Liste der Ressourcen auf das Speicherkonto, das Sie früher erstellt haben.
1. Klicken Sie im Speicherkontoblatt auf **Storage-Explorer (Vorschau)**.
1. Klicken Sie im Storage-Explorer unter **WARTESCHLANGEN** auf **musicsharingmessages**. Der Storage-Explorer zeigt die Nachricht an, die Sie gerade hinzugefügt haben.

## <a name="retrieve-and-remove-the-message"></a>Abrufen und Entfernen der Nachricht

Eine Zielkomponente für eine Nachricht in einer Speicherwarteschlange muss die Nachricht am Anfang der Warteschlange abrufen, verarbeiten und dann aus der Warteschlange löschen, damit andere Komponenten sie nicht abrufen:

1. Um die Nachricht am Anfang der Warteschlange abzurufen, geben Sie den folgenden Befehl in Azure Cloud Shell ein, und drücken Sie dann die EINGABETASTE:

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. Um die Nachricht anzuzeigen, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

    ```powershell
    $retrievedMessage.AsString
    ```

1. Um alle Eigenschaften der Nachricht anzuzeigen, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

    ```powershell
    $retrievedMessage
    ```

1. Um die Nachricht aus der Warteschlange zu entfernen, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. Um die Warteschlangenanzeige zu aktualisieren, klicken Sie im Azure-Portal auf dem Speicherkontoblatt auf **Übersicht** und dann auf **Storage-Explorer**.
1. Klicken Sie unter **WARTESCHLANGEN** auf **musicsharingmessages**. Der Storage-Explorer zeigt an, dass die Warteschlange leer ist, da Sie die einzige Nachricht entfernt haben.

## <a name="cleanup"></a>Cleanup

Geben Sie zum Entfernen aller in dieser Übung erstellten Ressourcen den folgenden Befehl in Azure Cloud Shell ein. 
```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```


## <a name="summary"></a>Zusammenfassung

Hier haben Sie ein Speicherkonto in Ihrem Azure-Abonnement erstellt und darin eine neue Warteschlange. Sie haben PowerShell auch verwendet, um die Aktionen der verteilten Anwendungskomponenten durch Hinzufügen einer Nachricht zur Warteschlange und anschließendes Abrufen und Entfernen zu simulieren.

Azure-Speicherkonto-Warteschlangen sind eine gute Lösung, wenn Nachrichten zwischen den Komponenten einer verteilten Anwendung übergeben werden sollen. Wählen Sie Speicherwarteschlangen nicht aus, wenn Sie Ereignisse veröffentlichen möchten.