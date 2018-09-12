In Ihrer Datenbank befinden sich mehrere Dokumente, die gleichzeitig aktualisiert werden müssen. In dieser Lektion wird erläutert, wie Sie gespeicherte Prozeduren über eine .NET-Konsolenanwendung erstellen, registrieren und ausführen.

## <a name="create-a-stored-procedure-in-your-app"></a>Erstellen einer gespeicherten Prozedur in Ihrer App

In dieser gespeicherten Prozedur wird mithilfe der OrderId (Bestell-ID), die eine Liste aller Auftragspositionen enthält, die Gesamtbestellsumme berechnet. Diese ergibt sich aus der Summe der Auftragspositionen abzüglich aller Gutschriften des Kunden, wobei sämtliche Gutscheincodes berücksichtigt werden.

1. Erweitern Sie auf der Registerkarte „Azure“ in Visual Studio Code das **Learning-Modul (SQL)** > **Benutzer** > **WebCustomers**, und klicken Sie dann mit der rechten Maustaste auf **Gespeicherte Prozeduren** und anschließend auf **Gespeicherte Prozedur erstellen**.

1. Geben Sie im Textfeld am oberen Rand des Bildschirms *UpdateOrderTotal* ein, und drücken Sie die EINGABETASTE, um der gespeicherten Prozedur einen Namen zu geben.

1. Erweitern Sie **Gespeicherte Prozeduren**, und klicken Sie auf **UpdateOrderTotal**.

1. Standardmäßig wird eine gespeicherte Prozedur bereitgestellt, die das erste Element abruft.

1. Fügen Sie zum Ausführen dieser gespeicherten Prozedur in Ihrer Anwendung der Datei „Program.cs“ den folgenden Code hinzu.

    ```csharp
    public async Task RunStoredProcedure(string databaseName, string collectionName, User user)
    {
        try
        {
            await client.ExecuteStoredProcedureAsync<string>(UriFactory.CreateStoredProcedureUri(databaseName, collectionName, "sample"), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            Console.WriteLine("Stored procedure complete");
        }
        catch (DocumentClientException de)
        {
            throw;
        }
    }
    ```
    <!--TODO: Update sproc to take order total and check for available dividend, and use of summer coupon code, and provide updated total-->

1. Kopieren Sie nun den folgenden Code, und fügen Sie diesen am Ende der **BasicOperations**-Methode ein.

    ```
    await this.RunStoredProcedure("Users", "WebCustomers", yanhe);
    ```

1. Führen Sie im integrierten Terminal den folgenden Befehl aus, um das Beispiel mit der gespeicherte Prozedur auszuführen.

    ```
    dotnet run
    ```
    Auf der Konsole wird die Meldung ausgegeben, dass die gespeicherte Prozedur abgeschlossen wurde.

## <a name="clean-up"></a>Bereinigen
<!---TODO: Update for sandbox?--->

Wenn Sie weiterhin an den Modulen in diesem Lernpfad arbeiten möchten, können Sie den Bereinigungsvorgang überspringen. Andernfalls müssen Sie mithilfe der folgenden Schritte den Bereinigungsvorgang für Ihre Ressourcen ausführen, da Ihnen sonst die Nutzung des Diensts in Rechnung gestellt wird.

1. Klicken Sie im Azure-Portal ganz links auf **Ressourcengruppen** und anschließend auf die erstellte Ressourcengruppe.  

    Sollte das linke Menü reduziert sein, klicken Sie auf ![Schaltfläche „Erweitern“](../media/5-javascript-programming/expand.png) , um es zu erweitern.

   ![Metriken im Azure-Portal](../media/5-javascript-programming/delete-resources-select.png)

1. Wählen Sie in dem neuen Fenster die Ressourcengruppe aus, und klicken Sie auf **Ressourcengruppe löschen**.

   ![Metriken im Azure-Portal](../media/5-javascript-programming/delete-resources.png)

1. Geben Sie im neuen Fenster den Namen der zu löschenden Ressourcengruppe ein, und klicken Sie dann auf **Löschen**.

## <a name="summary"></a>Zusammenfassung

In diesem Modul haben Sie eine .NET Core-Konsolenanwendung erstellt, mit der Benutzerdatensätze erstellt, aktualisiert und gelöscht werden. Außerdem werden mithilfe von SQL und LINQ Benutzerdatensätze abgefragt. Durch die Konsolenanwendung wird eine gespeicherte Prozedur ausgeführt, um Elemente in der Datenbank abzufragen.