In Ihrer Datenbank befinden sich mehrere Dokumente, die gleichzeitig aktualisiert werden müssen. In dieser Lektion wird erläutert, wie Sie gespeicherte Prozeduren über eine .NET-Konsolenanwendung erstellen, registrieren und ausführen.

## <a name="create-a-stored-procedure-in-your-app"></a>Erstellen einer gespeicherten Prozedur in Ihrer App

In dieser gespeicherten Prozedur wird mithilfe der OrderId (Bestell-ID), die eine Liste aller Auftragspositionen enthält, die Gesamtbestellsumme berechnet. Diese ergibt sich aus der Summe der Auftragspositionen abzüglich aller Gutschriften des Kunden, wobei sämtliche Gutscheincodes berücksichtigt werden.

1. Erweitern Sie in Visual Studio Code auf der Registerkarte **Azure Cosmos DB** Ihr Azure Cosmos DB-Konto, klicken Sie auf **Benutzer** > **WebCustomers**, klicken Sie dann mit der rechten Maustaste auf **Gespeicherte Prozeduren**, und klicken Sie anschließend auf **Gespeicherte Prozedur erstellen**.

1. Geben Sie im Textfeld am oberen Rand des Bildschirms `UpdateOrderTotal` ein, und drücken Sie die EINGABETASTE, um der gespeicherten Prozedur einen Namen zu geben.

1. Erweitern Sie **Gespeicherte Prozeduren** auf der Registerkarte **Azure Cosmos DB**, und klicken Sie auf **UpdateOrderTotal**.

    Standardmäßig wird eine gespeicherte Prozedur bereitgestellt, die das erste Element abruft.

1. Fügen Sie den folgenden Code in die Datei **Program.cs** ein, um diese gespeicherte Standardprozedur über Ihre Anwendung auszuführen.

    ```csharp
    public async Task RunStoredProcedure(string databaseName, string collectionName, User user)
    {
        await client.ExecuteStoredProcedureAsync<string>(UriFactory.CreateStoredProcedureUri(databaseName, collectionName, "UpdateOrderTotal"), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
        Console.WriteLine("Stored procedure complete");
    }
    ```

1. Kopieren Sie nun den folgenden Code, und fügen Sie diesen vor der `await this.DeleteUserDocument("Users", "WebCustomers", yanhe);`-Zeile der **BasicOperations**-Methode ein.

    ```csharp
    await this.RunStoredProcedure("Users", "WebCustomers", yanhe);
    ```

1. Führen Sie im integrierten Terminal den folgenden Befehl aus, um das Beispiel mit der gespeicherten Prozedur auszuführen.

    ```bash
    dotnet run
    ```

Die Konsole zeigt eine Ausgabe an, die angibt, dass die gespeicherte Prozedur abgeschlossen wurde.
