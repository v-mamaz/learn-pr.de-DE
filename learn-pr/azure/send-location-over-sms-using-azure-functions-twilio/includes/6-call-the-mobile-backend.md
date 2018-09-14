Die mobile App wird ausgeführt, und die erste Version der Azure-Funktion wurde erstellt. In dieser Einheit rufen Sie die Azure-Funktion in der mobilen App auf und übergeben den Standort des Benutzers und die Liste der Telefonnummern, an die der Benutzer SMS-Nachrichten senden möchte.

## <a name="calling-the-azure-function-from-the-mobile-app"></a>Aufrufen der Azure-Funktion in der mobilen App

1. Öffnen Sie `MainViewModel`.

1. Fügen Sie in dieser Klasse ein privates `HttpClient`-Feld namens `client` hinzu. Sie müssen einen Verweis auf den `System.Net.Http`-Namespace hinzufügen.

    ```cs
    HttpClient client = new HttpClient();
    ```

1. Fügen Sie ein konstantes Feld für die Basis-URL der Funktion hinzu. Legen Sie für dieses Feld die Adresse fest, die die lokale Azure Functions-Runtime abhört. Nachdem die Funktion in Azure bereitgestellt wurde, kann diese Konstante in die Azure-URL geändert werden.

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

1. Erstellen Sie in der `SendLocation`-Methode, nachdem der Standort gefunden wurde, eine neue Instanz von `PostData`, indem Sie den Standort und die Liste mit den vom Benutzer eingegebenen Telefonnummern verwenden. Sie müssen eine using-Anweisung für den `ImHere.Data`-Namespace hinzufügen.

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > Dabei wird davon ausgegangen, dass die Telefonnummern im richtigen Format eingegeben wurden (also eine Telefonnummer pro Zeile im `Editor`-Steuerelement). In einer App mit Produktionsqualität würde mithilfe einer Überprüfung sichergestellt werden, dass eine oder mehrere Telefonnummern im richtigen Format eingegeben wurden.

1. Zum Serialisieren von `PostData` als JSON verwenden Sie am einfachsten das NuGet-Paket „Newtonsoft.JSON“. Fügen Sie dieses NuGet-Paket dem `ImHere`-Projekt auf die gleiche Weise zu wie das Xamarin.Essentials-Paket in einer vorherigen Einheit.

1. Serialisieren Sie `PostData` zu `string` mithilfe einer statischen `JsonConvert`-Klasse. Sie müssen eine using-Anweisung für den `Newtonsoft.Json`-Namespace hinzufügen. Codieren Sie diese Zeichenfolge in eine `StringContent`-Klasse, sodass diese der Azure-Funktion als JSON übergeben werden kann.

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

1. Senden Sie diese Daten an die Funktion, und erhalten Sie das Ergebnis zurück.

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   Über `/api/<function name>` wird auf Azure-Funktionen zugegriffen. Wenn es sich bei dem Port, der von der lokalen Functions-Runtime ausgewählt wird, beispielsweise um Port 7071 handelt, wird die `SendLocation`-Funktion unter `http://localhost:7071/api/SendLocation` zur Verfügung gestellt.

1. Abhängig vom Ergebnis wird auf der Benutzeroberfläche eine Meldung angezeigt.

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

Der vollständige Code für die neuen Felder und die `SendLocation`-Methode wird unten angegeben.

```cs
HttpClient client = new HttpClient();
const string baseUrl = "http://localhost:7071";

async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";

        PostData postData = new PostData
        {
            Latitude = location.Latitude,
            Longitude = location.Longitude,
            ToNumbers = PhoneNumbers.Split('\n')
        };

        string data = JsonConvert.SerializeObject(postData);
        StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
        HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                            content);

        if (result.IsSuccessStatusCode)
            Message = "Location sent successfully";
        else
            Message = $"Error - {result.ReasonPhrase}";
    }
}
```

## <a name="testing-it-out"></a>Testen Sie es

1. Stellen Sie sicher, dass die Azure-Funktion noch lokal ausgeführt wird und der Port der `SendLocation`-Methode entspricht.

1. Legen Sie die UWP-App als Start-App fest, und führen Sie diese aus. Klicken Sie auf die Schaltfläche **Standort senden**. Im Konsolenfenster der Functions-Runtime, welches die aufgerufene Funktion angezeigt, wird die Ausgabe und die Protokollierung mit der generierten URL angezeigt.

    ![Ausgabe der aufgerufenen Funktion](../media/6-function-called.png)

1. Um die URL-Generierung zu testen, fügen Sie sie von der Konsole in einem Browser ein. Ihr aktueller Standort sollte angezeigt werden.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Sie in der mobilen App eine Azure-Funktion aufrufen. Dieser Aufruf gibt den Standort des Benutzers und die Telefonnummern weiter, die als JSON eingegeben wurden. In der nächsten Einheit müssen Sie die Azure-Funktion an Twilio binden, um den Standort als SMS-Nachricht zu senden.