Nachdem Sie gelernt haben, welche Arten von Abfragen erstellt werden können, verwenden wir nun den Daten-Explorer im Azure-Portal zum Abrufen und Filtern Ihrer Produktdaten.

Beachten Sie, dass die Abfrage auf der Registerkarte **Dokument** im Fenster Ihres Daten-Explorers standardmäßig auf `SELECT * FROM c` festgelegt ist. Diese Standardabfrage ruft alle Dokumente in der Sammlung ab und zeigt sie an.

![Die Standardabfrage im Daten-Explorer ist SELECT * FROM c.](../media-draft/4-run-queries/azure-cosmosdb-data-explorer-query.png)

## <a name="create-a-new-query"></a>Erstellen einer neuen Abfrage

1. Klicken Sie im Daten-Explorer auf die Registerkarte **Neue SQL-Abfrage**. Beachten Sie, dass `SELECT * from c` die Standardabfrage auf der neuen Registerkarte **Abfrage 1** ist, und klicken Sie dann auf **Abfrage ausführen**. Diese Abfrage gibt alle Ergebnisse in der Datenbank zurück.

    ![Ändern Sie die Standardabfrage, indem Sie ORDER BY c._ts DESC hinzufügen und auf „Filter anwenden“ klicken.](../media-draft/4-run-queries/azure-cosmosdb-data-explorer-edit-query.png)

2. Lassen Sie uns jetzt einige der in der vorherigen Einheit erörterten Abfragen ausführen. Löschen Sie `SELECT * from c` auf der Registerkarte „Abfrage“, kopieren Sie die folgende Abfrage, fügen Sie diese ein, und klicken Sie dann auf **Abfragen ausführen**.

    ```
    SELECT *
    FROM Products p
    WHERE p.id ="1"
    ```

    Die Ergebnisse geben das Produkt zurück, dessen `productId` 1 ist.

    ![Ändern Sie die Standardabfrage, indem Sie ORDER BY c._ts DESC hinzufügen und auf „Filter anwenden“ klicken.](../media-draft/4-run-queries/azure-cosmosdb-data-explorer-query-by-id.png)

3. Löschen Sie die vorherige Abfrage, kopieren Sie die folgende Abfrage, fügen Sie diese ein, und klicken Sie dann auf **Abfrage ausführen**. Diese Abfrage gibt in aufsteigender Reihenfolge und nach dem Preis sortiert den Preis, die Beschreibung und die Produkt-ID für alle Produkte zurück.
 
    ```
    SELECT p.price, p.description, p.productId
    FROM Products p
    ORDER BY p.price ASC
    ```

## <a name="summary"></a>Zusammenfassung

Sie haben nun einige grundlegende Abfragen für Ihre Daten in Azure Cosmos DB abgeschlossen. 