Im Rahmen dieses Moduls stellen Sie eine einfache Web-App bereit, die eine HTML-basierte Benutzeroberfläche darstellt. Mit einem serverlosen Back-End kann die Anwendung Bilder hochladen und automatisch Bildtitel abrufen, die diese beschreiben.

![Ausführen der Web-App](../media/0-app-screenshot-finished.png)

Im folgenden Diagramm sind die Azure-Dienste aufgeführt, die von der Anwendung verwendet werden.

1. Azure Blob Storage stellt statischen Webinhalt (HTML, CSS, JS) bereit und speichert Bilder.
2. Azure Functions verwaltet das Hochladen von Bildern, die Größenänderung und die Speicherung von Metadaten.
3. Azure Cosmos DB speichert Bildmetadaten.
4. Azure Logic Apps ruft Bildtitel von der Maschinelles Sehen-API von Cognitive Services ab.
5. Azure Active Directory wird zum Verwalten der Benutzerauthentifizierung verwendet.

![Diagramm der Lösungsarchitektur](../media/0-architecture.jpg)

In dieser Einheit lernen Sie Folgendes:
> [!div class="checklist"]
> * Konfigurieren von Azure Blob Storage zum Hosten einer statischen Website und von hochgeladenen Bildern
> * Hochladen von Bildern in Azure Blob Storage mit Azure Functions
> * Ändern der Größe von Bildern mit Azure Functions
> * Speichern von Bildmetadaten in Azure Cosmos DB
> * Verwenden der Maschinelles Sehen-API von Cognitive Services zum automatischen Generieren von Bildtiteln
> * Nutzen von Azure Active Directory zum Schützen der Web-App durch das Authentifizieren von Benutzern

Azure Blob Storage ist ein kostengünstiger und extrem skalierbarer Dienst, der zum Hosten von statischen Dateien verwendet werden kann. Für dieses Tutorial verwenden Sie den Dienst zum Bereitstellen von statischem Inhalt (z.B. HTML, JavaScript, CSS) für die von Ihnen erstellte Web-App.

## <a name="create-an-azure-storage-account"></a>Erstellen eines Azure-Speicherkontos

Ein Azure-Speicherkonto ist eine Azure-Ressource, mit der Sie Tabellen, Warteschlangen, Dateien, Blobs (Objekte) und VM-Datenträger speichern können.

1. Klicken Sie auf die Schaltfläche **Enter focus mode** (Fokusmodus starten), um Azure Cloud Shell (Bash) zu starten. Diese Schaltfläche befindet sich oben rechts oder unten auf der Seite. Dies hängt davon ab, wie breit Ihr Browserfenster dargestellt wird. Im Fokusmodus wird ein Cloud Shell-Fenster im Browserfenster auf der rechten Seite angedockt, damit Sie im Tutorial angezeigte Befehle leicht ausführen können.

1. In Azure ist eine Ressourcengruppe ein Container, der zusammengehörige Azure-Ressourcen enthält, um die Verwaltung zu vereinfachen. Erstellen Sie eine neue Ressourcengruppe mit dem Namen **first-serverless-app**.

    ```azurecli
    az group create -n first-serverless-app -l westcentralus
    ```

1. Der statische Inhalt (HTML-, CSS- und JavaScript-Dateien) für dieses Tutorial wird in Blob Storage gehostet. Für Blob Storage ist ein Speicherkonto erforderlich. Erstellen Sie ein Speicherkonto (Allgemein V2) in der Ressourcengruppe. Ersetzen Sie `<storage account name>` durch einen eindeutigen Namen.

    ```azurecli
    az storage account create -n <storage account name> -g first-serverless-app --kind StorageV2 -l westcentralus --https-only true --sku Standard_LRS
    ```
    
1. Verwenden Sie die Suchleiste oben im [Azure-Portal](https://portal.azure.com/?azure-portal=true), um das Speicherkonto zu finden, das Sie eben erstellt haben. Öffnen Sie das Konto.

1. Klicken Sie im linken Navigationsbereich auf **Statische Website (Vorschau)**, um einen Container für das Hosten von statischen Websites zu konfigurieren.
    - Klicken Sie auf **Aktiviert**, um eine statische Website zu aktivieren.
    - Geben Sie **index.html** als Name des Indexdokuments ein. Im Feld steht *index.html* bereits in grauer Schrift, jedoch ist dies nur ein Beispieltext. Sie müssen trotzdem **index.html** in das Feld eingeben.
    - Klicken Sie auf **Speichern**.
    
    ![Eingeben der Einstellungen für die statische Website](../media/1-storage-static-website.png)

1. Speichern Sie den **primären Endpunkt** an einem Ort, an dem Sie ihn beim Durcharbeiten des Tutorials bequem kopieren können. Dieser Endpunkt ist die URL Ihrer Web-App.

## <a name="upload-the-web-application"></a>Hochladen der Web-App

1. Die Quelldateien für die Anwendung, die Sie in diesem Tutorial erstellen, befinden sich in einem [GitHub-Repository](https://github.com/Azure-Samples/functions-first-serverless-web-application). Stellen Sie sicher, dass Sie sich in Cloud Shell in Ihrem Basisverzeichnis befinden, und klonen Sie dieses Repository.

    ```azurecli
    cd ~
    git clone https://github.com/Azure-Samples/functions-first-serverless-web-application
    ```

    Das Repository wird in `/home/<username>/functions-first-serverless-web-application` geklont.

1. Die clientseitige Webanwendung befindet sich im Ordner **www** und wird mit dem JavaScript-Framework „Vue.js“ erstellt. Wechseln Sie in den Ordner, und führen Sie **npm**-Befehle aus, um die Anwendungsabhängigkeiten zu installieren und die Anwendung zu erstellen. Es kann mehrere Minuten dauern, bis der letzte dieser Befehle abgeschlossen ist.

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

1. Öffnen Sie die URL des primären Endpunkts für statische Storage-Websites in einem Webbrowser, um die Anwendung anzuzeigen.

    ![Startseite der ersten serverlosen Web-App](../media/1-app-screenshot-new.png)


## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie eine Ressourcengruppe mit dem Namen **first-serverless-app** erstellt, die ein Speicherkonto enthält. Der statische Inhalt für Ihre Web-App wird in einem Blobcontainer namens **$web** im Speicherkonto gespeichert, und der Inhalt wird öffentlich zur Verfügung gestellt. Als Nächstes erfahren Sie, wie Sie eine serverlose Funktion zum Hochladen von Bildern in Blob Storage aus dieser Anwendung verwenden.