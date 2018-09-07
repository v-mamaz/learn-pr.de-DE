In dieser Übung erstellen Sie ein neues Speicherkonto für Ihr Azure-Abonnement. Verwenden Sie anschließend Azure Cloud Shell, um eine neue Warteschlange zu erstellen, eine Meldung hinzuzufügen und dann diese Meldung zu lesen und aus der Warteschlange zu entfernen.

Hierbei handelt es sich um die gleichen Aktionen, die von Komponenten in einer verteilten Anwendung durchgeführt werden. Beispielsweise kann eine mobile App einer Warteschlange eine Meldung hinzufügen, die dann darauf wartet, dass ein Webdienst sie abruft und verarbeitet.

## <a name="create-a-storage-account"></a>Erstellen eines Speicherkontos

Da Azure Storage-Warteschlangen ein Bestandteil von universellen Azure-Speicherkonten ist, müssen Sie zunächst ein Speicherkonto erstellen:

1. Navigieren Sie in einem Browser zum [Azure-Portal](https://portal.azure.com?azure-portal=true), und melden Sie sich mit Ihren regulären Anmeldeinformationen an.

1. Klicken Sie oben links auf **Alle Dienste**.

1. Scrollen Sie nach unten zum Abschnitt **Speicher**, und klicken Sie dann auf **Speicherkonten**.

1. Klicken Sie oben links auf dem Blatt **Speicherkonten** auf **Hinzufügen**.

  ![Screenshot: Blatt „Speicherkonten“ mit Hervorhebung der Option „Hinzufügen“](../media-draft/4-create-a-storage-account-1.png)

1. Geben Sie in das daraufhin angezeigte Dialogfeld die folgenden Informationen ein. Alle Optionen verfügen über ein `(i)`-Symbol im Portal, das Sie verwenden können, um mehr Informationen zur Funktionsweise dieser Option abzurufen.

    - Geben Sie in das Textfeld **Name** einen eindeutigen Namen für das Speicherkonto ein.
    - Stellen Sie unter **Bereitstellungsmodell** sicher, dass **Resource Manager** ausgewählt ist.
    - Wählen Sie in der Dropdownliste **Kontoart** die Option **StorageV2 (universell, Version 2)** aus.
    - Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.
    - Wählen Sie in der Dropdownliste **Replikation** den Wert **Lokal redundanter Speicher** aus.
    - Wählen Sie unter **Leistung** die Option **Standard** aus.
    - Klicken Sie unter **Zugriffsebene** auf die Option **Kalt**.
    - Klicken Sie unter **Sichere Übertragung erforderlich** auf die Option **Deaktiviert**.
    - Wählen Sie unter **Abonnement** Ihr Abonnement aus.
    - Klicken Sie unter **Ressourcengruppe** auf die Option **Neu erstellen**. Geben Sie **MusicSharingResourceGroup** in das Textfeld ein.
    - Klicken Sie unter **Virtuelle Netzwerke** auf die Option **Deaktiviert**. 

    ![Screenshot: Dialogfeld „Speicherkonto erstellen“](../media-draft/4-create-a-storage-account-2.png)

1. Klicken Sie auf **Erstellen**. Dann erstellt Azure eine neue Ressourcengruppe und ein neues Speicherkonto, das diesem zugeordnet ist.

    ![Screenshot: Dialogfeld „Speicherkonto erstellen“ mit Hervorhebung der Option „Erstellen“](../media-draft/4-create-a-storage-account-3.png)

## <a name="create-a-queue"></a>Erstellen einer Warteschlange

Nun ist das Speicherkonto erstellt, und Sie können eine neue Warteschlange hinzufügen. Sie müssen die Warteschlange mit PowerShell-Befehlen erstellen:

1. Klicken Sie in der oberen rechten Ecke des Portals auf den **Cloud Shell**-Link `(>_)`.

    ![Screenshot: Azure-Portal mit Hervorhebung des Symbols „Cloud Shell“](../media-draft/4-create-a-storage-queue-1.png)

1. Klicken Sie im Bildschirm **Welcome to Azure Cloud Shell** (Willkommen bei Azure Cloud Shell) auf **PowerShell (Linux)**.

1. Klicken Sie auf dem Bildschirm **You have no storage mounted** (Sie haben keinen Speicher bereitgestellt) auf **Speicher erstellen**.

1. Wenn die `PS Azure`-Eingabeaufforderung angezeigt wird, das Speicherkonto aufzurufen, geben Sie den folgenden Befehl ein. Ersetzen Sie den `<storageaccountname>` durch den eindeutigen Namen des Speicherkontos, das Sie zuvor erstellt haben, und drücken Sie auf **Enter**. Das entstandene Objekt soll einer Variablen mit dem Namen `$storageaccount` zugewiesen werden.

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. Als nächstes wird der _Kontext_ des Speicherkontos benötigt. Dabei handelt es sich um eine Eigenschaft das zurückgegebenen Objekts. Dieses soll einer anderen Variablen mit dem Namen `$context` zugewiesen werden.

    ```powershell
    $context = $storageaccount.Context
    ```

1. Danach kann die Warteschlange erstellt werden. Verwenden Sie den `New-AzureStorageQueue`-Befehl, und weisen Sie ihn einer `$messageQueue`-Variablen zu.
    - Übergeben Sie einen `-Name`-Parameter mit dem Wert `musicsharingmessages`.
    - Übergeben Sie einen `-Context`-Parameter mit dem Wert, den Sie im Schritt zuvor abgerufen haben.

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a>Hinzufügen einer Meldung zu einer Warteschlange

Da Sie nun eine Warteschlange im Speicherkonto erstellt haben, können Sie ihr eine Meldung hinzufügen.

1. Verwenden Sie die `New-Object`-Methode, um eine .NET-`CloudQueueMessage` mit einem zeichenfolgenbasierten Argument zu erstellen:

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. Übergeben Sie die erstellte `CloudQueueMessage` an die `AddMessageAsync`-Methode in Ihrer `$messageQueue`-Warteschlange, um die neue Meldung an die neue Warteschlange zu übergeben.

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

## <a name="verify-the-message-was-queued"></a>Überprüfen, ob die Meldung in die Warteschlange aufgenommen wurde

Sie können den **Storage-Explorer** verwenden, um mit der Warteschlange zu arbeiten. Zwei Variationen sind verfügbar:

- Eine plattformübergreifende Desktop-App für Linux, macOS und Windows, die Sie herunterladen können
- Eine Webvorschauversion für das Azure-Portal. Im Folgenden wird die Webversion verwendet, aber Sie können auch die Desktopversion installieren. Die Anweisungen sind ähnlich.

1. Klicken Sie im Azure-Portal in der Navigation auf der linken Seite auf **Alle Ressourcen**.

1. Klicken Sie in der Liste der Ressourcen auf das Speicherkonto, das Sie zuvor erstellt haben.

1. Klicken Sie im Speicherkontoblatt auf **Storage-Explorer (Vorschau)**.

1. Klicken Sie im Storage-Explorer unter **WARTESCHLANGEN** auf **musicsharingmessages**. Der Storage-Explorer sollte die Meldung anzeigen, die Sie gerade hinzugefügt haben.

## <a name="retrieve-and-remove-the-message"></a>Abrufen und Entfernen der Meldung

Zielkomponenten für eine Meldung in einer Speicherwarteschlange müssen die Meldung abrufen, die sich am Anfang der Warteschlange befindet. Anschließend muss die Zielkomponente die Meldung verarbeiten und aus der Warteschlange löschen, damit andere Komponenten diese nicht abrufen.

1. Sie können die erste in PowerShell verfügbare Meldung mithilfe der `GetMessageAsync`-Methode in der Warteschlange abrufen. Es handelt sich dabei um eine asynchrone .NET-Methode. Da dies an dieser Stelle zu lange dauern würde, können Sie einfach die `Result`-Eigenschaft verwenden, um den Rückgabewert abzurufen. Dadurch wird ein Objekt zurückgegeben, das für die Meldung steht, die einem Parameter zugewiesen werden kann.

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. Diese Meldung wird in Text dargestellt, wenn Sie `AsString` aufrufen. Dadurch wird der Wert auf der Konsole zurückgegeben.

    ```powershell
    $retrievedMessage.AsString
    ```

1. Stattdessen können Sie auch alle Eigenschaften der Meldung anzeigen, indem Sie nur den Variablennamen eingeben und die **EINGABETASTE** drücken.

    ```powershell
    $retrievedMessage
    ```

1. `GetMessageAsync` entfernt die Meldung *nicht*, sondern gibt sie nur zurück. Dadurch kann der Prozess fortgesetzt werden. Wenn Sie diese Meldung aus der Warteschlange entfernen möchten, können Sie die `DeleteMessageAsync`-Methode für die Warteschlange verwenden. Dafür muss die Meldung übergeben werden, die entfernt werden soll.

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. Wenn Sie prüfen möchten, ob die Meldung entfernt wurde, aktualisieren Sie die Warteschlangenanzeige im Azure-Portal, indem Sie zum Blatt „Speicherkonto“ navigieren und auf **Übersicht > Storage-Explorer** klicken. Klicken Sie unter **WARTESCHLANGEN** auf **musicsharingmessages**. Der Storage-Explorer sollte jetzt anzeigen, dass die Warteschlange leer ist, da Sie die einzige Meldung entfernt haben.


## <a name="summary"></a>Zusammenfassung
Warteschlangen für Speicherkonten sind eine gute Lösung, wenn _Meldungen_ zwischen den Komponenten einer verteilten Anwendung übergeben werden sollen. Sie eignen sich besonders, wenn Sie sicherstellen wollen, dass die Meldungen in der Reihenfolge zugestellt werden, in der Sie sie senden. Allerdings wird bei der Verwendung von Warteschlangen vorausgesetzt, dass Sender und Empfänger das Format der Daten kennen, die übergeben werden. Es besteht automatisch ein Datenvertrag, durch den die beiden miteinander kommunizierenden Dienste aneinander gekoppelt sind.

Nicht alle Architekturen müssen formatierte Datenblöcke übergeben. Einige Architekturen benötigen nur einfache Meldungen, die gesendet werden sollen, ohne zu wissen, wie die Meldung verarbeitet wird. In solchen Szenarios eignen sich Warteschlangen nicht. Daher sollten Sie sich in der nächsten Einheit über eine Meldungsstrategie informieren, die sich besser für diesen Kommunikationsstil eignet.