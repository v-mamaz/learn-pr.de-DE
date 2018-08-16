In diesem Modul können Sie eine einfache Webanwendung bereitstellen, in dem eine HTML-basierte Benutzeroberfläche dargestellt. Ein serverloses Back-End kann es sich um die Anwendung zum Hochladen von Bildern und erhalten automatisch Untertitel Beschreibung.

![Ausgeführte Web-app](../images/0-app-screenshot-finished.png)

Das folgende Diagramm zeigt die Azure-Dienste, die von der Anwendung verwendet:

1. BLOB Storage dient die statische Webinhalte (HTML, CSS und JS) und speichert Bilder.
2. Azure Functions verwaltet Bilduploads, Ändern der Größe und Speicher für Metadaten.
3. COSMOS DB speichert Metadaten zu Bildern.
4. Logik-Apps ruft Image Beschriftungen aus Computer Vision-API ab.
5. Azure Active Directory verwaltet die Benutzerauthentifizierung.

![Diagramm der Lösungsarchitektur](../images/0-architecture.jpg)

In dieser Einheit, erfahren Sie, wie Sie:
> [!div class="checklist"]
> * Konfigurieren Sie Azure Blob Storage zum Hosten einer statischen Website und hochgeladene Bilder.
> * Hochladen von Bildern in Azure Blob Storage mit Azure Functions.
> * Ändern der Bildgröße mithilfe von Azure Functions.
> * Store Bildmetadaten in Azure Cosmos DB.
> * Verwenden Sie Cognitive Services-maschinelles sehen-API, um das Image Untertitel automatisch generieren.
> * Verwenden Sie Azure Active Directory, um die Web-app zu sichern, indem Sie die Authentifizierung von Benutzern.

Azure Blob Storage ist ein kostengünstig und hochgradig skalierbaren Dienst, der zum Hosten von statischer Dateien verwendet werden kann. In diesem Tutorial verwenden Sie diese zum Verarbeiten von statischem Inhalt (z. B. HTML, JavaScript, CSS) für die Web-app, die Sie erstellen.

## <a name="create-a-storage-account"></a>Erstellen eines Speicherkontos

Ein Speicherkonto ist eine Azure-Ressource, die Ihnen ermöglicht, Tabellen, Warteschlangen, Dateien, Blobs (Objekte) und VM-Datenträger zu speichern.

1. Melden Sie sich der Cloud Shell (Bash), durch Auswählen der **EINGABETASTE fokusmodus** Schaltfläche. Diese Schaltfläche ist auf der rechten oberen Ecke oder den unteren Rand der Seite, je nachdem, wie breit Ihres Browserfensters ist. Fokusmodus Dockt eine Cloud Shell-Fensters auf der rechten Seite im Browserfenster, an, damit Sie problemlos Befehle ausführen können, die in diesem Tutorial gezeigt werden.

1. In Azure ist eine Ressourcengruppe ein Container, der verwandte Azure-Ressourcen zur besseren Verwaltung enthält. Erstellen Sie eine neue Ressourcengruppe mit dem Namen **ersten serverlosen app**.

    ```azurecli
    az group create -n first-serverless-app -l westcentralus
    ```

1. Der statische Inhalt (HTML, CSS und JavaScript-Dateien) für dieses Tutorial wird in Blob Storage gehostet. BLOB-Speicher ist ein Speicherkonto erforderlich. Erstellen Sie ein Speicherkonto (universell V2) in der Ressourcengruppe ein. Ersetzen Sie dies `<storage account name>` durch einen eindeutigen Namen.

    ```azurecli
    az storage account create -n <storage account name> -g first-serverless-app --kind StorageV2 -l westcentralus --https-only true --sku Standard_LRS
    ```

1. Über die Suchleiste am oberen Rand der [Azure-Portal](https://portal.azure.com), suchen Sie das Speicherkonto, das Sie gerade erstellt haben, und öffnen Sie sie.

1. Wählen Sie auf der linken Navigationsleiste **statische Website (Vorschau)** einen Container für das Hosten statischer Websites konfigurieren.
    - Wählen Sie **aktiviert** statische Website zu aktivieren.
    - Geben Sie *"Index.HTML"* als der Name des indexdokuments. Das Feld bereits hat *"Index.HTML"* in einer grauen Schriftart aber nur Beispieltext, müssen diesen Wert in das Feld eingeben.
    - Klicken Sie auf **Speichern**.
    
    ![Geben Sie die Einstellungen für statische website](../images/1-storage-static-website.png)

1. Speichern Sie die **primären Endpunkt** an einer beliebigen Stelle Sie können bequem kopieren aus beim Durcharbeiten des Tutorials. Dies ist die URL der Webanwendung.

## <a name="upload-the-web-application"></a>Laden Sie die Webanwendung hoch.

1. Die Quelldateien für die Anwendung, die Sie in diesem Tutorial erstellen befinden sich in einem [GitHub-Repository](https://github.com/Azure-Samples/functions-first-serverless-web-application). Stellen Sie sicher, dass Sie in Ihrem Basisverzeichnis in Cloud Shell und dieses Repository klonen.

    ```azurecli
    cd ~
    git clone https://github.com/Azure-Samples/functions-first-serverless-web-application
    ```

    Das Repository geklont `/home/<username>/functions-first-serverless-web-application`.

1. Die Client-Side-Web-Anwendung befindet sich in der **Www** Ordner und mit dem Vue.js JavaScript-Framework basiert. Ändern Sie in den Ordner, und führen Sie Npm-Befehle zum Installieren der Anwendung Abhängigkeiten und Erstellen der Anwendung. Die letzte von diesen Befehlen dauert mehrere Minuten in Anspruch.

    ```azurecli
    cd ~/functions-first-serverless-web-application/www
    npm install
    npm run generate
    ```

    Die Anwendung wird generiert, der **Dist** Ordner.

1. Wechseln Sie zum aktuelle Verzeichnis **Dist** und die Anwendung zum Hochladen der **$web** Blob-Container.

    ```azurecli
    cd dist
    az storage blob upload-batch -s . -d \$web --account-name <storage account name>
    ```

1. Öffnen Sie die Speicher statische Websites primären Endpunkt-URL in einem Webbrowser, um die Anwendung anzuzeigen.

    ![Erste serverlose Web-app-Startseite](../images/1-app-screenshot-new.png)


## <a name="summary"></a>Zusammenfassung

In dieser Einheit, die Sie erstellt einer Ressourcengruppe namens **ersten serverlosen app** , enthält ein Speicherkonto. Ein blobcontainer namens **$web** in Storage-Konto speichert die statische Inhalte für Ihre Webanwendung und stellt den Inhalt öffentlich zur Verfügung. Als Nächstes erfahren Sie, wie Sie mit einer serverlosen Funktion zum Hochladen von Bildern in Blob Storage von der Webanwendung.