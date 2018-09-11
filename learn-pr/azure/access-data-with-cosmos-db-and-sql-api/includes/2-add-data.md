Das Hinzufügen von Daten zu Ihrer Azure Cosmos DB-Datenbank sollte kein Problem sein. Sie öffnen das Azure-Portal, navigieren zu Ihrer Datenbank und verwenden den **Daten-Explorer**, um der Datenbank JSON-Dokumente hinzuzufügen. Es gibt zwar auch komplexere Möglichkeiten, um Daten hinzuzufügen, wir beginnen aber mit dieser Methode, da sich der Daten-Explorer sehr gut dazu eignet, sich mit den internen Abläufen und Funktionen von Azure Cosmos DB vertraut zu machen.

## <a name="what-is-the-data-explorer"></a>Was ist der Daten-Explorer?
Der Daten-Explorer von Azure Cosmos DB ist ein Tool im Azure-Portal, mit dem Sie in Azure Cosmos DB gespeicherte Daten verwalten können. Es stellt eine Benutzeroberfläche zum Anzeigen von und Navigieren durch Datensammlungen sowie zum Bearbeiten von Dokumenten in der Datenbank bereit.

## <a name="add-data-using-the-data-explorer"></a>Hinzufügen von Daten mit dem Daten-Explorer

1. Wenn Sie zuvor das vorherige Modul absolviert haben, klicken Sie im Fenster des Azure-Portals auf **Daten-Explorer** und anschließend auf **Vollbildmodus öffnen**.

    Melden Sie sich andernfalls beim [Azure-Portal](https://portal.azure.com/) an, und klicken Sie auf **Alle Dienste** > **Datenbanken** > **Azure Cosmos DB**. Wählen Sie anschließend Ihr Konto aus, klicken Sie auf **Daten-Explorer**, und klicken Sie anschließend auf **Vollbildmodus öffnen**
 
   ![Erstellen neuer Dokumente im Daten-Explorer im Azure-Portal](../media-draft/2-add-data/azure-cosmosdb-data-explorer-full-screen.png)

2. Klicken Sie im Feld **Vollbildmodus öffnen** auf **Öffnen**.

    Im Webbrowser wird der neue Daten-Explorer im Vollbildmodus angezeigt. Dadurch haben Sie mehr Platz und verfügen über eine dedizierte Umgebung für die Arbeit mit Ihrer Datenbank.

3. Klicken Sie auf **Neues Dokument**, um ein neues JSON-Dokument zu erstellen.

   ![Erstellen neuer Dokumente im Daten-Explorer im Azure-Portal](../media-draft/2-add-data/azure-cosmosdb-data-explorer-new-document.png)

4. Nun können Sie ein Dokument in der folgenden Struktur zur Sammlung hinzufügen. Kopieren Sie dafür einfach den folgenden Code, und fügen Sie diesen auf der Registerkarte **Dokumente** ein.

     ```
    {
        "id": "1",
        "productId": "33218896",
        "category": "Women's Clothing",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt",
        "shipping": {
            "weight": 1,
            "dimensions": {
            "width": 6,
            "height": 8,
            "depth": 1
           }
        }
     ```

5. Nachdem Sie den JSON-Code auf der Registerkarte **Dokumente** hinzugefügt haben, klicken Sie auf **Speichern**.

    ![Kopieren Sie JSON-Daten, und klicken Sie im Azure-Portal im Daten-Explorer auf „Speichern“.](../media-draft/2-add-data/azure-cosmosdb-data-explorer-save-document.png)

6. Erstellen und speichern Sie ein weiteres Dokument, indem Sie das folgende JSON-Objekt in den Daten-Explorer kopieren und auf **Speichern** klicken.

     ```
    {
        "id": "2",
        "productId": "33218897",
        "category": "Women's Outerwear",
        "manufacturer": "Contoso",
        "description": "Black wool pea-coat",
        "shipping": {
            "weight": 2,
            "dimensions": {
            "width": 8,
            "height": 11,
            "depth": 3
           }
        }
    }
     ```

7. Vergewissern Sie sich, dass die Dokumente gespeichert wurden, indem Sie im linken Menü auf **Dokumente** klicken. 

    Die beiden Dokumente werden im Daten-Explorer auf der Registerkarte **Dokumente** angezeigt.

## <a name="summary"></a>Zusammenfassung

In diesem Modul haben Sie Ihrer Datenbank mithilfe des Daten-Explorers zwei Dokumente hinzugefügt, die jeweils ein Produkt in Ihrem Produktkatalog darstellen. Der Daten-Explorer eignet sich sehr gut, um Dokumente zu erstellen, Dokumente zu ändern und sich mit Azure Cosmos DB vertraut zu machen.  
