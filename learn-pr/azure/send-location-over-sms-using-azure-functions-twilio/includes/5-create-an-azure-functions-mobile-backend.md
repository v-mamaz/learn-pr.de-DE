An diesem Punkt ruft die App den Benutzerstandort ab und ist bereit, an eine Azure-Funktion gesendet zu werden. In dieser Einheit erstellen Sie die Azure-Funktion.

## <a name="create-an-azure-functions-project"></a>Erstellen eines Azure Functions-Projekts

1. Fügen Sie der Projektmappe `ImHere` ein neues Projekt hinzu, indem Sie mit der rechten Maustaste auf die Projektmappe klicken und *Hinzufügen > Neues Projekt* auswählen.

1. Wählen Sie in der Struktur links *Visual C# > Cloud* aus, und klicken Sie dann im Arbeitsbereich in der Mitte auf *Azure Functions*.

1. Geben Sie dem Projekt den Namen „ImHere.Functions“, und klicken Sie dann auf **OK**.

    ![Dialogfeld „Neues Projekt hinzufügen“](../media-drafts/5-add-new-functions-project.png)

1. Behalten Sie im Konfigurationsdialogfeld **Neues Projekt** die Functions-Version *Azure Functions v1 (.NET Framework)* bei. Wählen Sie *HTTP-Trigger* aus, behalten Sie für das Speicherkonto die Einstellung *Speicheremulator* bei, und legen Sie die Zugriffsrechte auf *Anonym* fest. Klicken Sie dann auf **OK**.

    ![Dialogfeld zur Azure Functions-Projektkonfiguration](../media-drafts/5-configure-trigger.png)

Das neue Projekt wird erstellt und enthält die Standardfunktion `Function1`.

> Diese Funktion wurde mit anonymem Zugriff erstellt. Nach der Veröffentlichung in Azure kann diese Funktion von jedem Benutzer aufgerufen werden, der die zugehörige URL kennt. In der Praxis würden Sie die Funktion über eine Authentifizierung schützen, beispielsweise über die [Azure App Service-Authentifizierung](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) oder über [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c).

## <a name="create-the-function"></a>Erstellen der Funktion

Das Azure Functions-Projekt wird mit einer einzigen HTTP-Triggerfunktion namens `Function1` erstellt. Die Funktion selbst wird als statische `Run`-Methode in der Klasse `Function1` implementiert.

1. Benennen Sie die Datei im Projektmappen-Explorer von „Function1.cs“ in „SendLocation.cs“ um. Klicken Sie auf `Function1`Ja **, wenn Sie zur Umbenennung aller Verweise auf das Codeelement**  aufgefordert werden.

1. Benennen Sie den Funktionsnamen im Attribut in „SendLocation“ um.

    ```cs
    [FunctionName("SendLocation")]
    ```

1. Löschen Sie den Inhalt der Funktion bis auf die erste Zeile, mit der eine Informationsmeldung an die Protokollierung ausgegeben wird.

    ```cs
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                       TraceWriter log)
    {
        log.Info("C# HTTP trigger function processed a request.");
    }
    ```

## <a name="create-a-class-to-share-data-between-the-mobile-app-and-function"></a>Erstellen einer Klasse zur Freigabe von Daten zwischen der mobilen App und der Funktion

Wenn Daten an die Azure-Funktion gesendet werden, werden Sie als JSON gesendet. Die mobile App serialisiert die Daten in JSON, und die Funktion führt eine Deserialisierung aus JSON durch. Um für konsistente Daten zwischen der mobilen App und der Funktion zu sorgen, erstellen Sie ein neues Projekt, das eine Klasse zum Speichern der Daten zu Standort und Telefonnummern enthält. Anschließend wird durch die App und die Funktion auf dieses Projekt verwiesen.

1. Erstellen Sie ein neues Projekt unterhalb der Projektmappe `ImHere`, indem Sie mit der rechten Maustaste auf die Projektmappe klicken und *Hinzufügen > Neues Projekt* auswählen.

1. Wählen Sie in der Struktur links *Visual C# > .NET Standard* aus, und klicken Sie dann im Arbeitsbereich in der Mitte auf *Klassenbibliothek (.NET Standard)*.

1. Geben Sie dem Projekt den Namen „ImHere.Data“, und klicken Sie dann auf **OK**.

    ![Dialogfeld „Neues Projekt hinzufügen“](../media-drafts/5-add-new-net-standard-project.png)

1. Löschen Sie die automatisch generierte Datei „Class1.cs“.

1. Erstellen Sie eine neue Klasse im `ImHere.Data`-Projekt namens `PostData`, indem Sie mit der rechten Maustaste auf das Projekt und anschließend auf *Hinzufügen > Klasse* klicken. Geben Sie der neuen Klasse den Namen „PostData“, und klicken Sie auf **OK**.

1. Fügen Sie `double`-Eigenschaften für Längen- und Breitengrad sowie eine `string[]`-Eigenschaft für die Telefonnummern hinzu, die als Sendeziel verwendet werden.

    ```cs
    public class PostData
    {
        public double Latitude { get; set; }
        public double Longitude { get; set; }
        public string[] ToNumbers { get; set; }
    }
    ```

1. Fügen Sie den Projekten `ImHere.Functions` und `ImHere` einen Verweis auf dieses Projekt hinzu, indem Sie mit der rechten Maustaste auf das Projekt und anschließend auf *Hinzufügen > Verweis* klicken. Wählen Sie in der Struktur links *Projekte* aus, und aktivieren Sie dann das Feld neben *ImHere.Data*.

    ![Konfigurieren von Projektverweisen](../media-drafts/5-configure-project-references.png)

## <a name="read-the-data-sent-to-the-function"></a>Lesen der an die Funktion gesendeten Daten

In der Azure-Funktion enthält der `req`-Parameter die gesendete HTTP-Anforderung, und die Daten in dieser Anforderung sind ein als JSON serialisiertes `PostData`-Objekt.

1. Öffnen Sie die Klasse `SendLocation` im `ImHere.Functions`-Projekt.

1. Lesen Sie den Inhalt der HTTP-Anforderung in ein `PostData`-Objekt aus, und fügen Sie eine using-Direktive für den `ImHere.Data`-Namespace hinzu.

    ```cs
    PostData data = await req.Content.ReadAsAsync<PostData>();
    ```

1. Erstellen Sie unter Verwendung des Längen- und Breitengrads aus `PostData` eine Google Maps-URL.

   ```cs
   string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
   ```

1. Protokollieren Sie die URL.

    ```cs
    log.Info($"URL created - {url}");
    ```

1. Geben Sie einen Statuscode 200 zurück, um anzuzeigen, dass die Funktion fehlerfrei ausgeführt wurde.

    ```cs
    return req.CreateResponse(HttpStatusCode.OK);
    ```

Die vollständige Funktion wird unten gezeigt.

```cs
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                                Route = null)]HttpRequestMessage req,
                                                    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    PostData data = await req.Content.ReadAsAsync<PostData>();
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.Info($"URL created - {url}");
    return req.CreateResponse(HttpStatusCode.OK);
}
```

## <a name="run-the-azure-function-locally"></a>Lokales Ausführen der Azure-Funktion

Funktionen können mit einem lokalen Speicherkonto und einer lokalen Azure Functions-Runtime lokal ausgeführt werden. Mithilfe dieser lokalen Runtime können Sie Ihre Funktion testen, bevor Sie sie in Azure bereitstellen.

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt `ImHere.Functions`, und wählen Sie *Als Startprojekt festlegen* aus.

1. Wählen Sie im Menü *Debuggen* die Option *Ohne Debuggen starten* aus. Die lokale Azure Functions-Runtime wird in einem Konsolenfenster gestartet und startet Ihre Funktion. Hierbei wird auf einem verfügbaren Port auf `localhost` gelauscht.

    ![Lokal ausgeführte Azure-Funktion](../media-drafts/5-function-running-locally.png)

1. Notieren Sie den Port, auf dem die Funktion lauscht. Sie benötigen diese Angabe in der nächsten Einheit, um die mobile App zu testen. In der Abbildung unten lauscht die Funktion auf Port **7071**.

    ```sh
    Listening on http://localhost:7071/
    ```

1. Führen Sie die Funktion weiterhin aus, damit Sie in der nächsten Einheit die mobile App testen können.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie ein Azure Functions-Projekt in Visual Studio erstellt wird, und Sie haben ein freigegebenes Objekt mit einem Datenobjekt für die gemeinsame Verwendung durch die mobile App und die Funktion hinzugefügt. Außerdem haben Sie erfahren, wie Sie eine grundlegende Implementierung der Funktion erstellen, um die übergebenen Daten zu deserialisieren. Ferner haben Sie erfahren, wie eine Azure-Funktion lokal ausgeführt wird. In der nächsten Einheit rufen Sie die Azure-Funktion aus der mobilen App auf.