Angenommen, wir möchten einen einfachen Bookmark Lookup-Dienst erstellen. Der Dienst ist anfänglich schreibgeschützt. Wenn ein Benutzer nach einem Eintrag suchen möchte, sendet er eine Anforderung mit der ID des Eintrags, und wir geben die URL zurück. Die folgende Abbildung verdeutlicht den Datenfluss.

![Flussdiagramm zur Suche nach einem Lesezeichen in unserem Cosmos DB-Back-End](../media-draft/find-bookmark-flow-small.png)

Wenn ein Benutzer uns eine Anforderung mit entsprechendem Text sendet, versuchen wir, einen Eintrag in unserer Back-End-Datenbank zu finden, der diesen Text als Schlüssel oder ID enthält. Wir geben ein Ergebnis zurück, das angibt, ob wir den Eintrag gefunden haben.

Irgendwo müssen wir Daten speichern. In diesem Flussdiagramm wird als Datenspeicher Azure Cosmos DB verwendet. Aber wie stellen wir eine Verbindung mit dieser Datenbank über eine Funktion her und lesen Daten? In der Welt der Funktionen konfigurieren wir eine *Eingabebindung* für diesen Auftrag.  Es ist einfach, eine Bindung über das Azure-Portal zu konfigurieren. Wie wir in Kürze sehen werden, müssen Sie keinen Code für Aufgaben wie das Öffnen einer Speicherverbindung schreiben. Die Azure Functions-Laufzeit und -Bindung nehmen Ihnen diese Aufgaben ab.

> [!IMPORTANT]
> Wir werden auf einige Ressourcen (Datenbank, Funktion, Bindungen, Code) verweisen, die wir hier in unserer nächsten Übungseinheit erstellen. Bitte bewahren Sie diese Ressourcen zumindest bis zum Abschluss dieses Kurses auf.

Wie im vorherigen Modul werden wir alle Aufgaben im Azure-Portal erledigen.

## <a name="create-an-azure-cosmos-db"></a>Erstellen einer Azure Cosmos DB 

Melden Sie sich unter [https://portal.azure.com](https://portal.azure.com?azure-portal=true) mit Ihrem Azure-Konto am Azure-Portal an.

### <a name="create-a-database-account"></a>Erstellen eines Datenbankkontos

Ein Datenbankkonto ist ein Container für die Verwaltung mindestens einer Datenbank. Bevor wir eine Datenbank erstellen können, müssen wir ein Datenbankkonto erstellen.

1. Wählen Sie die Schaltfläche **Ressource erstellen** in der oberen linken Ecke des Azure-Portals und dann **Datenbanken** > **Azure Cosmos DB** aus.

2. Geben Sie auf der Seite **Neues Konto** die Einstellungen für das neue Azure Cosmos DB-Konto ein.
 
    Einstellung|Wert|BESCHREIBUNG
    ---|---|---
    ID|*Ein eindeutiger Name*|Geben Sie einen eindeutigen Namen ein, der das Azure Cosmos DB-Konto identifiziert. Da *documents.azure.com* an die ID angefügt wird, die Sie bereitstellen, um Ihren URI zu erstellen, sollten Sie eine eindeutige, aber identifizierbare ID verwenden.<br><br>Die ID darf nur Kleinbuchstaben, Zahlen und einen Bindestrich (-) enthalten, und sie muss zwischen 3 und 50 Zeichen lang sein.
    API|SQL|Die API bestimmt den Typ des zu erstellenden Kontos. Azure Cosmos DB stellt fünf APIs bereit, die Sie für Ihre Anwendung auswählen können: SQL (Dokumentdatenbank), Gremlin (Diagrammdatenbank), MongoDB (Dokumentdatenbank), Azure Table und Cassandra. Für jede API ist zurzeit ein separates Konto erforderlich. <br><br>Wählen Sie **SQL** aus. Zurzeit funktionieren der Azure Cosmos DB-Trigger, Eingabebindungen und Ausgabebindungen ausschließlich mit SQL- und Graph-API-Konten. 
    Abonnement|*Ihr Abonnement*|Wählen Sie das Azure-Abonnement aus, das Sie für dieses Azure Cosmos DB-Konto verwenden möchten.
    Ressourcengruppe|Vorhandene verwenden<br><br>*Geben Sie dann [!INCLUDE [resource-group-name](./rg-name.md)] ein, die Ressourcengruppe, die wir in einer früheren Einheit für die Ressourcen dieses Moduls erstellt haben.*| Wir wählen **Vorhandene verwenden** aus, weil wir alle für dieses Modul erstellten Ressourcen unter derselben Ressourcengruppe zusammenfassen möchten.
    Standort|Wird automatisch ausgefüllt, sobald **Vorhandene verwenden** festgelegt wurde. | Wählen Sie den geografischen Standort aus, an dem Ihr Azure Cosmos DB-Konto gehostet werden soll. Verwenden Sie einen Standort, der Ihren Benutzern am nächsten liegt, um ihnen einen schnellen Zugriff auf die Daten zu gewähren. In dieser Übungseinheit wird der Standort für uns als der für die vorhandene Ressourcengruppe festgelegte Standort vorgegeben.
    
Belassen Sie für alle anderen Felder auf dem Blatt **Neues Konto** die Standardwerte, da wir sie in diesem Modul verwenden.  Dazu gehören **Georedundanz aktivieren**, **Multimaster aktivieren** und **Virtuelle Netzwerke**.

3. Wählen Sie **Erstellen** aus, um das Datenbankkonto bereitzustellen.

4. Die Bereitstellung kann einige Zeit in Anspruch nehmen. Warten Sie also auf eine Meldung vom Typ **Die Bereitstellung war erfolgreich** ähnlich der folgenden Meldung, bevor Sie fortfahren.

<!-- TODO figure out how to center these image -->

![Benachrichtigung, dass die Datenbankkontobereitstellung erfolgreich war](../media-draft/db-deploy-success.PNG)

5. Herzlichen Glückwunsch! Sie haben Ihr Datenbankkonto erstellt und bereitgestellt.

6. Wählen Sie **Zu Ressource wechseln** aus, um im Portal zum Datenbankkonto zu navigieren. Wir werden als nächstes der Datenbank eine Sammlung hinzufügen.

### <a name="add-a-collection"></a>Hinzufügen einer Sammlung

In Cosmos DB enthält ein *Container* beliebige vom Benutzer generierte Entitäten. In einer Datenbank, die die SQL-API (eine dokumentorientierte API) unterstützt, ist ein Container eine *Sammlung*. In einer Sammlung speichern wir Dokumente. Wahrscheinlich wird alles klarer, wenn wir eine Sammlung erstellen und einige Dokumente hinzufügen.

Wir verwenden das Tool Daten-Explorer im Azure-Portal, um eine Datenbank und eine Sammlung zu erstellen.

1. Klicken Sie auf **Daten-Explorer** > **Neue Sammlung**.

2. Geben Sie unter **Sammlung hinzufügen** die Einstellungen für die neue Sammlung ein.

    >[!TIP]
    >Der Bereich **Sammlung hinzufügen** wird ganz rechts angezeigt. Möglicherweise müssen Sie nach rechts scrollen, damit Sie ihn sehen.

    Einstellung|Empfohlener Wert|Beschreibung
    ---|---|---
    Datenbank-ID|[!INCLUDE [cosmos-db-name](./cosmos-db-name.md)]| Datenbanknamen müssen zwischen 1 und 255 Zeichen lang sein und dürfen weder /, \\, #, ? noch nachgestellte Leerzeichen enthalten.<br><br>Sie können hier einen beliebigen Namen eingeben, aber wir schlagen [!INCLUDE [cosmos-db-name](./cosmos-db-name.md)] als Namen für die neue Datenbank vor, und auf diesen Namen beziehen wir uns in dieser Einheit. |
    Sammlungs-ID|[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)]|Geben Sie [!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)] als Namen für die neue Sammlung ein. Für Sammlungs-IDs gelten dieselben Zeichenanforderungen wie für Datenbanknamen.
    Speicherkapazität| Fest (10 GB)|Verwenden Sie den Standardwert **Fest (10 GB)**. Dieser Wert gibt die Speicherkapazität der Datenbank an.
    Durchsatz|400 RU|Ändern Sie den Durchsatz in 400 Anforderungseinheiten pro Sekunde (RU/s). Die Speicherkapazität muss auf **Fest (10 GB)** festgelegt werden, um den Durchsatz auf 400 RU/s festzulegen. Sie können den Durchsatz später zentral hochskalieren, wenn Sie Wartezeiten verringern möchten.
    
3. Klicken Sie auf **OK**. Im Daten-Explorer werden die neue Datenbank und die neue Sammlung angezeigt. Nun verfügen wir also über eine Datenbank. In der Datenbank haben wir eine Sammlung definiert. Im nächsten Schritt fügen wir einige Daten hinzu, die auch als Dokumente bezeichnet werden.

### <a name="add-test-data"></a>Hinzufügen von Testdaten

Wir haben eine Sammlung namens [!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)] in unserer Datenbank definiert, was also möchten wir in der Sammlung speichern? Nun, die Idee ist, eine URL und eine ID in jedem Dokument zu speichern, also eine Liste von Webseitenlesezeichen. 

Sie fügen nun mithilfe des Daten-Explorers der neuen Sammlung Daten hinzu.

1. Im Daten-Explorer wird die neue Datenbank im Bereich „Sammlungen“ angezeigt. Erweitern Sie die Datenbank [!INCLUDE [cosmos-db-name](./cosmos-db-name.md)] und die Sammlung [!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)], und klicken Sie auf **Dokumente** und anschließend auf **Neues Dokument**.
  
2. Fügen Sie der Sammlung nun ein Dokument mit der folgenden Struktur hinzu. Jedes Dokument ist eine schemalose JSON-Datei.

     ```json
     {
         "id": "docs",
         "URL": "https://docs.microsoft.com/azure"
     }
     ```

3. Nachdem Sie die JSON-Datei auf der Registerkarte **Dokumente** hinzugefügt haben, klicken Sie auf **Speichern**.

Wenn das Dokument gespeichert wird, beachten Sie, dass mehr Eigenschaften vorhanden sind als die, die wir hinzugefügt haben. Sie beginnen alle mit einem Unterstrich (_rid, _self, _etag, _attachments, _ts). Hierbei handelt es sich um Eigenschaften, die vom System zur Verwaltung des Dokuments generiert werden. In der folgenden Tabelle wird kurz erläutert, worum es sich dabei handelt.


|Eigenschaft  |Beschreibung  |
|---------|---------|
|_rid     |     Die Ressourcen-ID (_rid) ist ein eindeutiger Bezeichner, der auch gemäß dem Ressourcenstapel für das Ressourcenmodell hierarchisch ist. Sie wird intern für die Platzierung und Navigation der Dokumentressource verwendet.    |
|_self     |   Der eindeutig adressierbare URI für die Ressource.      |
|_etag     |   Für die Steuerung der optimistischen Parallelität erforderlich.     |
|_attachments     |  Der adressierbaren Pfad für die Anlagenressource.       |
|_ts     |    Der Zeitstempel der letzten Aktualisierung dieser Ressource.    |
 

4. Fügen Sie der Sammlung weitere Dokumente hinzu. Verwenden Sie für jedes der folgenden Elemente den Befehl **Neues Dokument**, um die jeweiligen Einträge zu erstellen. Vergessen Sie nicht, auf ##Speichern** zu klicken, um die Hinzufügungen zu erfassen.

|id  |value  |
|---------|---------|
|Portal     |  https://portal.azure.com       |
|learn     |   https://docs.microsoft.com/learn |
|marketplace     |    https://azuremarketplace.microsoft.com/marketplace/apps  |
|blog | https://azure.microsoft.com/blog |

Wenn Sie fertig sind, sollte Ihre Sammlung wie im folgenden Screenshot dargestellt aussehen.

![Screenshot der SQL-API-Benutzeroberfläche im Portal mit der Liste der Einträge, die der Lesezeichenauflistung hinzugefügt wurden.](../media-draft/db-bookmark-coll.PNG)

Wir verfügen nun über einige Einträge in der Lesezeichensammlung. Das Szenario funktioniert wie folgt. Wenn z.B. eine Anforderung mit „Id=docs“ eingeht, suchen wir in der Lesezeichensammlung nach dieser ID und geben die URL https://docs.microsoft.com/azure zurück. Erstellen Sie nun eine Azure-Funktion, die nach Werten in dieser Sammlung sucht.

## <a name="create-our-function"></a>Erstellen der Funktion

1. Navigieren Sie zu der Funktions-App, die Sie in der vorherigen Einheit erstellt haben.

2. Erweitern Sie die Funktions-App, zeigen Sie auf die Funktionssammlung, und wählen Sie dann die Schaltfläche „Hinzufügen“ (**+**) neben **Funktionen** aus. Durch diese Aktion wird der Vorgang der Funktionserstellung gestartet. Die folgende Animation veranschaulicht diese Aktion.

![Animation des Pluszeichens, das angezeigt wird, wenn der Benutzer mit der Maus auf das Menüelement Funktionen zeigt.](../media-draft/func-app-plus-hover-small.gif)

3. Die Seite zeigt den vollständigen Satz von unterstützten Triggern an. Wählen Sie **HTTP-Trigger** aus. Dies ist der erste Eintrag im folgenden Screenshot.

![Screenshot eines Teils der Benutzeroberfläche zur Auswahl der Triggervorlage, wobei der HTTP-Trigger zuerst angezeigt wird (oben links in der Abbildung).](../media-draft/trigger-templates-small.PNG)

4. Füllen Sie das auf der rechten Seite angezeigte Dialogfeld **Neue Funktion** mit den folgenden Werten aus.

|Feld  |Wert  |
|---------|---------|
|Sprache     | **JavaScript**        |
|Name     |   [!INCLUDE [func-name-find](./func-name-find.md)]     |
| Autorisierungsstufe | **Funktion** |

5. Wählen Sie **Erstellen** aus, um unsere Funktion zu erstellen. Die Datei „index.js“ wird im Code-Editor geöffnet und zeigt eine Standardimplementierung der durch HTTP ausgelösten Funktion an.

Sie können überprüfen, was wir bisher erreicht haben, indem Sie unsere neue Funktion wie folgt testen:

1. Klicken Sie in der neuen Funktion rechts oben auf **</> Funktions-URL abrufen**, wählen Sie **Standard (Funktionsschlüssel)** aus, und klicken Sie dann auf **Kopieren**.

2. Fügen Sie die Funktions-URL, die Sie kopiert haben, in die Adressleiste Ihres Browsers ein. Fügen Sie den Wert der Abfragezeichenfolge `&name=<yourname>` am Ende der URL hinzu, und drücken Sie die Taste `Enter` auf Ihrer Tastatur, um die Anforderung auszuführen. Sie sollten eine Antwort ähnlich der folgenden Antwort sehen, die von der Funktion zurückgegeben und in Ihrem Browser angezeigt wird.  

Nachdem unsere Basisfunktion nun funktioniert, sollten wir unsere Aufmerksamkeit auf das Lesen von Daten aus unserer Azure Cosmos DB oder (in unserem Szenario) der Sammlung [!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)] richten.

## <a name="add-a-cosmos-db-input-binding"></a>Hinzufügen einer Cosmos DB-Eingabebindung

Wir möchten Daten aus der Datenbank lesen, die wir erstellt haben. Geben Sie also Eingabebindungen ein. Wie Sie sehen werden, können wir in wenigen Schritten eine Bindung konfigurieren, die mit unserer Datenbank kommunizieren kann.

1. Wählen Sie **Integrieren** im Funktionsmenü auf der linken Seite aus, um die Registerkarte „Integration“ zu öffnen.

Die verwendete Vorlage hat einen HTTP-Trigger und eine HTTP-Ausgabebindung für uns erstellt. Fügen Sie die neue Azure Cosmos DB-Eingabebindung hinzu. 

2. Wählen Sie **+ neue Eingabe** unter der Spalte **Eingaben** aus. Eine Liste aller möglichen Eingabebindungstypen wird angezeigt.

3. Klicken Sie in der Liste auf **Azure Cosmos DB**, und klicken Sie dann die Schaltfläche **Auswählen**. Durch diese Aktion wird die Azure Cosmos DB-Eingabekonfigurationsseite geöffnet.

Im nächsten Schritt müssen Sie eine Verbindung mit unserer Datenbank einrichten.

4. Klicken Sie im Feld mit dem Namen **Azure Cosmos DB-Kontoverbindung** auf dieser Seite rechts neben dem leeren Feld auf *Neu*. Durch diese Aktion wird das Dialogfeld **Verbindung** geöffnet, in dem bereits **Azure Cosmos DB-Konto** und Ihr Azure-Abonnement ausgewählt sind. Sie müssen nur noch eine Datenbankkonto-ID auswählen.

5. Im Abschnitt **Datenbankkonto erstellen** mussten Sie einen ID-Wert angeben. Suchen Sie nun in der Dropdownliste *Datenbankkonto* nach diesem Wert, und klicken Sie dann auf **Auswählen**.

Eine neue Verbindung mit der Datenbank wird konfiguriert und im Feld **Azure Cosmos DB-Kontoverbindung** angezeigt. Wenn Sie neugierig sind, was sich tatsächlich hinter diesem abstrakten Name verbirgt, klicken Sie einfach auf *Wert anzeigen*, um die Verbindungszeichenfolge anzuzeigen.

Wir möchten nach einem Lesezeichen mit einer bestimmten ID suchen. Verknüpfen Sie die erhaltene ID also mit der Bindung.

7. Geben Sie im Feld **Dokument-ID (optional)** die Angabe `{id}` ein. Dies wird als ein *Bindungsausdruck* bezeichnet. Die Funktion wird durch eine HTTP-Anforderung ausgelöst, die eine Abfragezeichenfolge verwendet, um die zu suchende ID anzugeben. Da IDs in der Sammlung eindeutig sind, gibt die Bindung 0 (nicht gefunden) oder 1 (gefunden) Dokument(e) zurück.

8. Füllen Sie die verbleibenden Felder auf dieser Seite sorgfältig mit den Werten in der folgenden Tabelle aus. Sie können jederzeit auf das Informationssymbol rechts neben dem jeweiligen Feldnamen klicken, um weitere Informationen zum Zweck der einzelnen Felder zu erhalten.


|Einstellung  |Wert  |Beschreibung  |
|---------|---------|---------|
|Dokumentparametername     |  **bookmark**       |  Der Name, der zum Identifizieren dieser Bindung in Ihrem Code verwendet wird.      |
|Datenbankname     |  [!INCLUDE [cosmos-db-name](./cosmos-db-name.md)]       | Die Datenbank, aus der die Daten gelesen werden. Dies ist der Datenbankname, den wir zuvor in dieser Lektion festgelegt haben.        |
|Sammlungsname     |  [!INCLUDE [cosmos-db-name](./cosmos-coll-name.md)]        | Die Sammlung, aus der Daten gelesen werden. Diese Einstellung wurde zuvor in dieser Lektion definiert. |
|SQL-Abfrage (optional)    |   Leer lassen       |   Wir rufen jeweils nur ein Dokument basierend auf der ID ab. Daher ist die Filterung anhand des Dokument-ID-Felds in diesem Fall besser als die Verwendung einer SQL-Abfrage. Wir könnten eine SQL-Abfrage für die Rückgabe eines Eintrags (`SELECT * from b where b.ID = {id}`) erstellen. Diese Abfrage würde tatsächlich ein Dokument zurückgeben, aber es würde in einer Dokumentsammlung zurückgegeben. Unser Code müsste eine Sammlung unnötigerweise bearbeiten. Verwenden Sie den SQL-Abfrageansatz, wenn mehrere Dokumente abgerufen werden sollen.   |
|Partitionsschlüssel (optional)     |   Leer lassen      |  Sie können die Standardwerte hier übernehmen.       |

9. Klicken Sie auf **Speichern**, um alle Änderungen an dieser Bindungskonfiguration zu speichern. Da wir jetzt unsere Bindung definiert haben, ist es an der Zeit, sie in unserer Funktion zu verwenden.

## <a name="update-function-implementation"></a>Aktualisieren der Funktionsimplementierung

1. Klicken Sie auf unsere Funktion ([!INCLUDE [func-name-find](./func-name-find.md)]), um *index.js* im Code-Editor zu öffnen. Wir haben eine Eingabebindung hinzugefügt, um aus unserer Datenbank zu lesen. Lassen Sie uns also die Logik so aktualisieren, dass diese Bindung verwendet wird.

2. Ersetzen Sie den gesamten Code in „index.js“ durch den Code im folgenden Codeausschnitt.

[!code-javascript[](../code/find-bookmark-single.js)]

Wenn eine HTTP-Anforderung bewirkt, dass unsere Funktion ausgelöst wird, wird der `id`-Abfrageparameter an unsere Cosmos DB Eingabebindung übergeben. Wenn ein Dokument gefunden wird, das dieser ID entspricht, wird der `bookmark`-Parameter auf dieses festgelegt. In diesem Fall erstellen wir eine Antwort mit dem URL-Wert, der im Lesezeichendokument gefunden wurde. Wenn kein Dokument gefunden wurde, das mit diesem Schlüssel übereinstimmt, reagieren wir mit einer Nutzlast und einen Statuscode, der dem Benutzer die schlechte Nachricht mitteilt.

## <a name="try-it-out"></a>Testen

1. Klicken Sie wie üblich rechts oben auf **</> Funktions-URL abrufen**, wählen Sie **Standard (Funktionsschlüssel)** aus, und klicken Sie dann auf **Kopieren**., um die URL der Funktion zu kopieren.

2. Fügen Sie die Funktions-URL, die Sie kopiert haben, in die Adressleiste Ihres Browsers ein. Fügen Sie den Wert der Abfragezeichenfolge `&id=docs` am Ende der URL hinzu, und drücken Sie die Taste `Enter` auf Ihrer Tastatur, um die Anforderung auszuführen. Wenn alles ordnungsgemäß ist, sollte eine Antwort angezeigt werden, die eine URL zu dieser Ressource enthält.

3. Ersetzen Sie `&id=docs` durch `&id=missing`, und beobachten Sie die Antwort.

4. Ersetzen Sie die vorherige Abfragezeichenfolge durch `&id=`, und beobachten Sie die Antwort.

>[!TIP]
>Sie können die Funktion auch mithilfe der Registerkarte **Test** in der Benutzeroberfläche des Funktionsportals testen. Sie können einen Abfrageparameter hinzufügen oder einfach Anforderungstext angeben, um die gleichen Ergebnisse zu erhalten, die in den vorangegangenen Schritten beschrieben wurden.

In dieser Einheit haben wir unsere erste Eingabebindung manuell erstellt, um aus einer Azure Cosmos DB-Datenbank zu lesen. Die Menge an Code, die wir geschrieben haben, um unsere Datenbank zu durchsuchen und Daten zu lesen, war dank Bindungen nur minimal. Der größte Teil unserer Arbeit bestand im deklarativen Konfigurieren der Bindung, und die Plattform hat sich um den Rest gekümmert.  

In der nächsten Einheit fügen wir unserer Lesezeichensammlung durch eine Azure Cosmos DB-Ausgabebindung weitere Daten hinzu.

> [!TIP]
> Diese Einheit ist nicht als Tutorial zu Azure Cosmos DB gedacht. Wenn Sie tiefere Einblicke wünschen, finden Sie hier einige Ressourcen, die Ihnen den Einstieg erleichtern:
>
>* [Einführung in Azure Cosmos DB: SQL-API](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)
>
>* [Technische Übersicht über Azure Cosmos DB](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)
>
>* [Dokumentation für Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/)