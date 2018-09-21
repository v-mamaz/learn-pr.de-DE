Sie können Ihrer Azure Cosmos DB-Datenbank ganz einfach Daten hinzufügen. Öffnen Sie dazu das Azure-Portal, navigieren Sie zu Ihrer Datenbank und verwenden den Daten-Explorer, um der Datenbank JSON-Dokumente hinzuzufügen. Es gibt zwar auch komplexere Möglichkeiten, um Daten hinzuzufügen, wir beginnen aber mit dieser Methode, da sich der Daten-Explorer sehr gut dazu eignet, sich mit den internen Abläufen und Funktionen von Azure Cosmos DB vertraut zu machen.

## <a name="what-is-the-data-explorer"></a>Was ist der Daten-Explorer?
Der Daten-Explorer von Azure Cosmos DB ist ein Tool im Azure-Portal, mit dem Sie in Azure Cosmos DB gespeicherte Daten verwalten können. Über die bereitgestellte Benutzeroberfläche können Sie Datensammlungen anzeigen, durch Datensammlungen navigieren und Dokumente in der Datenbank bearbeiten. Außerdem lassen sich Daten abfragen und gespeicherte Prozeduren erstellen und ausführen.

## <a name="add-data-using-the-data-explorer"></a>Hinzufügen von Daten mit dem Daten-Explorer

1. Melden Sie sich beim [Azure-Portal für die Sandbox](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.

    > [!IMPORTANT]
    > Melden Sie sich beim Azure-Portal und der Sandbox mit demselben Konto an.
    > 
    > Melden Sie sich beim Azure-Portal über den obigen Link an, um sicherzustellen, dass Sie mit der Sandbox verbunden sind, die Zugriff auf ein Concierge-Abonnement ermöglicht.

1. Klicken Sie auf **Alle Dienste** > **Datenbanken** > **Azure Cosmos DB**. Wählen Sie anschließend Ihr Konto aus, und klicken Sie zuerst auf **Daten-Explorer** und anschließend auf **Im Vollbildmodus öffnen**.
 
   ![Erstellen neuer Dokumente im Daten-Explorer im Azure-Portal](../media/3-azure-cosmosdb-data-explorer-full-screen.png)

2. Klicken Sie im Feld **Vollbildmodus öffnen** auf **Öffnen**.

    Im Webbrowser wird der neue Daten-Explorer im Vollbildmodus angezeigt. Dadurch haben Sie mehr Platz und verfügen über eine dedizierte Umgebung für die Arbeit mit Ihrer Datenbank.

3. Um ein neues JSON-Dokument zu erstellen, erweitern Sie im Bereich für die SQL-API **Clothing** (Kleidung), und klicken Sie zuerst auf **Dokumente** und anschließend auf **Neues Dokument**.

   ![Erstellen neuer Dokumente im Daten-Explorer im Azure-Portal](../media/3-azure-cosmosdb-data-explorer-new-document.png)

4. Fügen Sie der Sammlung ein Dokument hinzu, und verwenden Sie dabei die folgende Struktur. Kopieren Sie einfach den folgenden Code, und fügen Sie ihn auf der Registerkarte **Dokumente** ein. Überschreiben Sie hierbei den aktuellen Inhalt:

     ```json
    {
        "id": "1",
        "productId": "33218896",
        "category": "Women's Clothing",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt",
        "price": "14.99",
        "shipping": {
            "weight": 1,
            "dimensions": {
            "width": 6,
            "height": 8,
            "depth": 1
           }
        }
    }
     ```

5. Nachdem Sie den JSON-Code auf der Registerkarte **Dokumente** hinzugefügt haben, klicken Sie auf **Speichern**.

    ![Kopieren Sie JSON-Daten, fügen Sie sie ein, und klicken Sie im Azure-Portal im Daten-Explorer auf „Speichern“.](../media/3-azure-cosmosdb-data-explorer-save-document.png)

6. Erstellen und speichern Sie ein weiteres Dokument, indem Sie erneut auf **Neues Dokument** klicken, das folgende JSON-Objekt kopieren und in den Daten-Explorer einfügen und auf **Speichern** klicken.

     ```json
    {
        "id": "2",
        "productId": "33218897",
        "category": "Women's Outerwear",
        "manufacturer": "Contoso",
        "description": "Black wool pea-coat",
        "price": "49.99",
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

In dieser Einheit haben Sie Ihrer Datenbank mithilfe des Daten-Explorers zwei Dokumente hinzugefügt, die jeweils ein Produkt in Ihrem Produktkatalog darstellen. Der Daten-Explorer eignet sich sehr gut, um Dokumente zu erstellen, Dokumente zu ändern und sich mit Azure Cosmos DB vertraut zu machen.  
