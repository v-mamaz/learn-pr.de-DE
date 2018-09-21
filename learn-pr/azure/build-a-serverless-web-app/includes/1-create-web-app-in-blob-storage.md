Im Rahmen dieses Moduls stellen Sie eine einfache Web-App bereit, die über eine HTML-basierte Benutzeroberfläche verfügt. Mit einem serverlosen Back-End kann die Anwendung Bilder hochladen und automatisch beschreibende Bildtitel generieren.

![Ausführen der Web-App](../media/0-app-screenshot-finished.png)

Im folgenden Diagramm sind die Azure-Dienste aufgeführt, die von der Anwendung verwendet werden.

![Die Abbildung zeigt, wie verschiedene Azure-Dienste wie Azure Blob Storage, Azure Functions, Cosmos DB, Azure Logic Apps und Azure Active Directory von der Anwendung verwendet werden. ](../media/0-architecture.jpg)

1. Azure Blob Storage stellt statischen Webinhalt (HTML, CSS, JS) bereit und speichert Bilder.
2. Azure Functions verwaltet das Hochladen von Bildern, die Größenänderung und die Speicherung von Metadaten.
3. Azure Cosmos DB speichert Bildmetadaten.
4. Azure Logic Apps ruft Bildtitel von der Maschinelles Sehen-API von Cognitive Services ab.
5. Azure Active Directory wird zum Verwalten der Benutzerauthentifizierung verwendet.

Azure Blob Storage ist ein kostengünstiger und extrem skalierbarer Dienst, der zum Hosten von statischen Dateien verwendet werden kann. In diesem Modul verwenden Sie Blob Storage, um statische Inhalte (z.B. HTML, JavaScript oder CSS) für die Web-App bereitzustellen, die Sie erstellen.

## <a name="create-an-azure-storage-account"></a>Erstellen eines Azure-Speicherkontos

[!include[](../../../includes/azure-sandbox-activate.md)]

Ein Azure Storage-Konto ist eine Azure-Ressource, mit der Sie Tabellen, Warteschlangen, Dateien, Blobs (Objekte) und VM-Datenträger speichern können.

1. Der statische Inhalt (HTML-, CSS- und JavaScript-Dateien) für dieses Modul wird in Blob Storage gehostet. Für Blob Storage ist ein Speicherkonto erforderlich. Erstellen Sie ein Speicherkonto vom Typ „General-purpose v2“(GPv2) in der Ressourcengruppe. Ersetzen Sie `<storage account name>` durch einen eindeutigen Namen.

    ```azurecli
    az storage account create \
        -n <storage account name> \
        -g <rgn>[Sandbox resource group name]</rgn> \
        --kind StorageV2 \
        --https-only true \
        --sku Standard_LRS
    ```
    
1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.

1. Verwenden Sie die Suchleiste oben im Portal, um das Speicherkonto zu finden, das Sie eben erstellt haben. Öffnen Sie das Konto.

1. Klicken Sie im linken Navigationsbereich auf **Statische Website (Vorschau)**, um einen Container für das Hosten von statischen Websites zu konfigurieren.
    - Klicken Sie auf **Aktiviert**, um eine statische Website zu aktivieren.
    - Geben Sie **index.html** als Name des Indexdokuments ein. Im Feld steht *index.html* bereits in grauer Schrift, jedoch ist dies nur ein Beispieltext. Sie müssen trotzdem **index.html** in das Feld eingeben.
    - Klicken Sie auf **Speichern**.
    
    ![Eingeben der Einstellungen für die statische Website](../media/1-storage-static-website.png)

1. Speichern Sie den **primären Endpunkt** an einem Ort, an dem Sie ihn beim Durcharbeiten des Moduls bequem kopieren können. Dieser Endpunkt ist die URL Ihrer Webanwendung.

## <a name="upload-the-web-application"></a>Hochladen der Webanwendung

1. Die Quelldateien für die Anwendung, die Sie in diesem Modul erstellen, befinden sich in einem [GitHub-Repository](https://github.com/Azure-Samples/functions-first-serverless-web-application). Navigieren Sie in Cloud Shell zu Ihrem Basisverzeichnis, und klonen Sie dieses Repository.

    ```azurecli
    cd ~
    git clone https://github.com/Azure-Samples/functions-first-serverless-web-application
    ```

    Das Repository wird in `/home/<username>/functions-first-serverless-web-application` geklont.

1. Die clientseitige Webanwendung befindet sich im Ordner **www** und wird mit dem JavaScript-Framework „Vue.js“ erstellt. Öffnen Sie den Ordner **www**, und führen Sie **npm**-Befehle aus, um die Anwendungsabhängigkeiten zu installieren und die Anwendung zu erstellen. Es kann mehrere Minuten dauern, bis der letzte dieser Befehle abgeschlossen ist.

    ```azurecli
    cd ~/functions-first-serverless-web-application/www
    npm install
    npm run generate
    ```

    Die Anwendung wird im Ordner **dist** generiert.

1. Legen Sie den **dist**-Ordner als das aktuelle Verzeichnis fest, und laden Sie die Anwendung in den Blobcontainer **$web** hoch.

    ```azurecli
    cd dist
    az storage blob upload-batch -s . -d \$web --account-name <storage account name>
    ```

1. Öffnen Sie die URL des primären Endpunkts der statischen Websites in einem Webbrowser, um die Anwendung anzuzeigen.

    ![Startseite der ersten serverlosen Web-App](../media/1-app-screenshot-new.png)


## <a name="summary"></a>Zusammenfassung

In dieser Lektion haben Sie ein Speicherkonto erstellt. Der statische Inhalt für Ihre Webanwendung wird in einem Blobcontainer namens **$web** im Speicherkonto gespeichert, und der Inhalt wird öffentlich zur Verfügung gestellt. Als Nächstes erfahren Sie, wie Sie eine serverlose Funktion zum Hochladen von Bildern in Blob Storage aus dieser Webanwendung verwenden.