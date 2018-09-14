Angenommen Sie, wir möchten, zum Erstellen eines einfachen Bookmark Lookup-Diensts. Der Dienst ist Readonly anfänglich aus. Wenn ein Benutzer einen Eintrag zu finden möchte, senden Sie eine Anforderung mit der ID des Eintrags, und wir die URL zurück. Das folgende Diagramm verdeutlicht den Flow.

![Flussdiagramm der Suche nach einem Lesezeichen in unsere Cosmos DB Back-end](../media-draft/find-bookmark-flow-small.png)

Wenn ein Benutzer uns eine Anforderung mit dem Text sendet, versuchen wir, einen Eintrag in der Back-End-Datenbank zu suchen, diesen Text als Schlüssel oder -ID enthält Wir haben, der angibt, ob wir den Eintrag oder nicht gefunden Ergebnis zurück.

Wir müssen Daten zu speichern. In diesem Flussdiagramm wird Datenspeicher wie Azure Cosmos DB angezeigt. Aber wie wir von einer Funktion mit dieser Datenbank verbinden und Lesen von Daten? In der Welt von Funktionen konfigurieren wir eine *eingabebindung* für diesen Auftrag.  Es ist einfach, eine Bindung über das Azure-Portal konfiguriert. Wie wir in Kürze sehen werden, müssen Sie Code für Aufgaben wie das Öffnen einer speicherverbindung schreiben. Die Azure Functions-Laufzeit und die Bindung sorgt diese Aufgaben für Sie.

> [!IMPORTANT]
> Wir werden auf einige Ressourcen ("Datenbank", "Funktion", "Bindungen", "Code") verweisen, die wir hier in unserer nächsten testumgebung erstellen. Bewahren Sie diese Ressourcen zu mindestens bis Sie diesen Kurs abgeschlossen haben.

Wie bei der vorherigen Modul der Fall war, werden wir alles, was im Azure-Portal tun.

## <a name="create-an-azure-cosmos-db"></a>Erstellen Sie ein Azure Cosmos DB 

### <a name="create-a-database-account"></a>Erstellen eines Datenbankkontos

Einem Datenbankkonto ist ein Container für eine oder mehrere Datenbanken verwalten. Bevor wir eine Datenbank erstellen können, müssen wir ein Datenbankkonto erstellen.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

2. Wählen Sie die **erstellen Sie eine Ressource** Schaltfläche finden Sie auf der linken oberen Ecke des Azure-Portal, klicken Sie dann auf **Datenbanken** > **Azure Cosmos DB**.

3. Geben Sie auf der Seite **Neues Konto** die Einstellungen für das neue Azure Cosmos DB-Konto ein.

    Einstellung|Wert|BESCHREIBUNG
    ---|---|---
    ID|*Ein eindeutiger Name*|Geben Sie einen eindeutigen Namen ein, der das Azure Cosmos DB-Konto identifiziert. Da *documents.azure.com* an die ID angefügt wird, die Sie bereitstellen, um Ihren URI zu erstellen, sollten Sie eine eindeutige, aber identifizierbare ID verwenden.<br><br>Die ID darf nur Kleinbuchstaben, Zahlen und einen Bindestrich (-) enthalten, und sie muss zwischen 3 und 50 Zeichen lang sein.
    API|SQL|Die API bestimmt den Typ des zu erstellenden Kontos. Azure Cosmos DB stellt fünf APIs entsprechend den Anforderungen Ihrer Anwendung zur Verfügung: SQL (Dokumentendatenbank), Gremlin (Diagrammdatenbank), MongoDB (Dokumentendatenbank), Azure Table und Cassandra, jede ist derzeit ein separates Konto erforderlich. <br><br>Wählen Sie **SQL**. Zu diesem Zeitpunkt funktionieren der Azure Cosmos DB-Trigger, eingabebindungen und ausgabebindungen nur mit SQL-API und Graph-API-Konten. 
    Abonnement|*Ihr Abonnement*|Wählen Sie das Azure-Abonnement, das Sie für dieses Azure Cosmos DB-Konto verwenden möchten, aus.
    Ressourcengruppe|Vorhandenen verwenden<br><br>*Wählen Sie dann <rgn>[Ressourcengruppennamen Sandkasten]</rgn>, die Ressourcengruppe, die wir in einer früheren Einheit für dieses Modul die Ressourcen erstellt.*| Wählen wir **vorhandene**, da wir alle für dieses Modul in der gleichen Ressourcengruppe erstellte Ressourcen gruppieren möchten.
    Standort|Automatisch ausgefüllten einmal **vorhandene** festgelegt ist. | Wählen Sie den geografischen Standort aus, an dem Ihr Azure Cosmos DB-Konto gehostet werden soll. Verwenden Sie einen Standort, der Ihren Benutzern am nächsten liegt, um ihnen einen schnellen Zugriff auf die Daten zu gewähren. In diesem Lab wird der Speicherort für uns als Speicherort für die vorhandene Ressourcengruppe festgelegt vorab bestimmt.

Lassen Sie alle anderen Felder in der **neues Konto** Blatt bei Werten, da wir sie in diesem Modul verwenden.  Dazu gehören **georedundanz aktivieren**, **Multi-Master aktivieren**, **virtuelle Netzwerke**.

4. Wählen Sie **erstellen** bereitstellen und das Datenbankkonto bereitstellen.

5. Bereitstellung kann einige Zeit dauern. Warten Sie also eine **Bereitstellung erfolgreich** Meldung ähnlich der folgenden Meldung aus, bevor Sie fortfahren.

<!-- TODO figure out how to center these image -->

![Benachrichtigung, die nach der Bereitstellung der Datenbank-Konto](../media-draft/db-deploy-success.PNG)

6. Herzlichen Glückwunsch! Sie haben erstellt und Ihrem Datenbankkonto bereitgestellt.

7. Wählen Sie **zu Ressource wechseln** , zu der Datenbankkonto im Verwaltungsportal zu navigieren. Wir werden eine Sammlung mit der Datenbank als Nächstes hinzufügen.

### <a name="add-a-collection"></a>Hinzufügen einer Sammlung

In Cosmos DB eine *Container* enthält Entitäten für den beliebige vom Benutzer generierte. In einer Datenbank eine dokumentorientierte-API die unterstützt SQL-API, die ein Container ist ein *Auflistung*. In einer Sammlung speichern wir von Dokumenten. Hoffentlich werden alle klarer, sobald wir eine Sammlung erstellen, und fügen Sie einige Dokumente hinzu.

Erstellen wir mithilfe des Daten-Explorer-Tools im Azure-Portal eine Datenbank und Sammlung.

1. Klicken Sie auf **Daten-Explorer** > **Neue Sammlung**.

2. In der **Sammlung hinzufügen**, geben Sie die Einstellungen für die neue Sammlung.

    >[!TIP]
    >Der Bereich **Sammlung hinzufügen** wird ganz rechts angezeigt. Möglicherweise müssen Sie nach rechts scrollen, damit Sie ihn sehen.

    Einstellung|Empfohlener Wert|Beschreibung
    ---|---|---
    Datenbank-ID|[!INCLUDE [cosmos-db-name](./cosmos-db-name.md)]| Datenbanknamen müssen zwischen 1 und 255 Zeichen lang sein und dürfen weder /, \\, #, ? noch nachgestellte Leerzeichen enthalten.<br><br>Sie können, geben hier beliebig, aber es wird empfohlen [!INCLUDE [cosmos-db-name](./cosmos-db-name.md)] als Namen für die neue Datenbank, und ist, was wir in dieser Einheit verweisen müssen. |
    Sammlungs-ID|[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)]|Geben Sie [!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)] als Namen für die neue Sammlung. Sammlungs-IDs gelten dieselben zeichenanforderungen wie für Datenbanknamen.
    Speicherkapazität| Fixed (10 GB)|Übernehmen Sie den Standardwert **Fest (10 GB)**. Dieser Wert gibt die Speicherkapazität der Datenbank an.
    Throughput|400 RU|Ändern Sie den Durchsatz in 400 Anforderungseinheiten pro Sekunde (RU/s). Die Speicherkapazität muss auf **Fest (10 GB)** festgelegt werden, um den Durchsatz auf 400 RU/s einzustellen. Sie können den Durchsatz später zentral hochskalieren, wenn Sie Wartezeiten reduzieren möchten.
    
3. Klicken Sie auf **OK**. Im Daten-Explorer zeigt die neue Datenbank und Sammlung. Jetzt haben wir also eine Datenbank. In der Datenbank haben wir eine Sammlung definiert. Als Nächstes fügen wir einige Daten, die auch als Dokumente bezeichnet.

### <a name="add-test-data"></a>Hinzufügen von Testdaten

Wir haben eine Sammlung definiert, in unserer Datenbank mit dem Namen [!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)], also was wir beabsichtigten in der Sammlung speichern? Die Idee ist, eine URL und die ID jedes Dokuments, wie eine Liste der Webseite Lesezeichen speichern. 

Wir fügen die Daten auf die neue Sammlung mit dem Daten-Explorer.

1. Im Daten-Explorer wird die neue Datenbank im Bereich „Sammlungen“ angezeigt. Erweitern Sie die [!INCLUDE [cosmos-db-name](./cosmos-db-name.md)] Datenbank, erweitern Sie die [!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)] Sammlung, klicken Sie auf **Dokumente**, und klicken Sie dann auf **neues Dokument**.
  
2. Fügen Sie nun der Sammlung ein Dokument mit folgender Struktur hinzu. Jedes Dokument ist die schemalose JSON-Datei.

     ```json
     {
         "id": "docs",
         "URL": "https://docs.microsoft.com/azure"
     }
     ```

3. Nachdem Sie den JSON-Code auf der Registerkarte **Dokumente** hinzugefügt haben, klicken Sie auf **Speichern**.

Wenn das Dokument gespeichert wird, beachten Sie, dass es mehr Eigenschaften als diejenigen, die hinzugefügt wurden. Sie fangen alle mit einem Unterstrich ("_rid", "_self", "_etag", "_attachments", "_ts"). Hierbei handelt es sich um Eigenschaften, die vom System zur Verwaltung des Dokuments generiert. Die folgende Tabelle erklärt kurz an, was sind.

|Eigenschaft  |Beschreibung  |
|---------|---------|
|_rid     |     Die Ressourcen-ID (_rid) ist ein eindeutiger Bezeichner, der auch gemäß dem ressourcenstapel für das Ressourcenmodell hierarchisch ist. Sie wird intern für die Platzierung und Navigation der dokumentressource verwendet.    |
|_self     |   Den eindeutig adressierbaren URI für die Ressource.      |
|_etag     |   Für die Steuerung optimistischer Parallelität erforderlich.     |
|_attachments     |  Den adressierbaren Pfad der anlagenressource.       |
|_ts     |    Der Zeitstempel der letzten Aktualisierung dieser Ressource.    |
 
4. Fügen Sie ein paar weitere Dokumente in die Auflistung ein. Verwenden Sie für jeden der folgenden, die **neues Dokument** Befehl erneut aus, um einen Eintrag für jede zu erstellen. Vergessen Sie nicht auf klicken, ## Save ** um die Erweiterungen zu erfassen.

|id  |value  |
|---------|---------|
|Portal     |  https://portal.azure.com       |
|Erfahren Sie mehr     |   https://docs.microsoft.com/learn |
|Marketplace     |    https://azuremarketplace.microsoft.com/marketplace/apps  |
|blog | https://azure.microsoft.com/blog |

Wenn Sie damit fertig sind, sollte Ihre Sammlung wie im folgenden Screenshot aussehen.

![Screenshot der SQL-API-Benutzeroberfläche im Portal mit der Liste der Einträge haben wir unsere Lesezeichen-Auflistung hinzugefügt.](../media-draft/db-bookmark-coll.PNG)

Wir haben nun einige Einträge in der Sammlung von Lesezeichen. In diesem Szenario funktioniert wie folgt. Wenn eine Anforderung mit dem Sie, z. B. eingeht "Id = Docs", wir suchen dieser ID in der Sammlung von Lesezeichen und die URL zurückgegeben https://docs.microsoft.com/azure. Lassen Sie eine Azure-Funktion, die Werte in dieser Auflistung gesucht werden soll.

## <a name="create-our-function"></a>Erstellen Sie unsere-Funktion

1. Navigieren Sie zur Funktions-app, die Sie in der vorherigen Einheit erstellt haben.

2. Erweitern Sie Ihre Funktionen-app dann zeigen Sie auf die Auflistung von Funktionen aus, und aktivieren Sie das Hinzufügen (**+**) neben **Funktionen**. Diese Aktion wird der Prozess der Funktion gestartet. Die folgende Animation veranschaulicht dieses Aktion.

![Die Animation von dem Pluszeichen (+) angezeigt wird, wenn der Benutzer auf das Menüelement Funktionen zeigt.](../media-draft/func-app-plus-hover-small.gif)

3. Die Seite zeigt uns, den vollständigen Satz von unterstützten Triggern. Wählen Sie **HTTP-Trigger**, dies ist der erste Eintrag im folgenden Screenshot.

![Screenshot des Teils der Trigger Vorlagenauswahl-Benutzeroberfläche mit dem TTP-Trigger zuerst angezeigt, in der oberen linken Seite des Bilds.](../media-draft/trigger-templates-small.PNG)

4. Füllen Sie die **neue Funktion** mithilfe der folgenden Werte rechts angezeigten Dialogfeld.

|Feld  |Wert  |
|---------|---------|
|Sprache     | **JavaScript**        |
|Name     |   [!INCLUDE [func-name-find](./func-name-find.md)]     |
| Autorisierungsstufe | **Function** |

5. Wählen Sie **erstellen** unserer Funktion zu erstellen, die der Datei "Index.js" im Code-Editor geöffnet und zeigt eine Standardimplementierung der per HTTP ausgelöste Funktion.

Sie können überprüfen, was wir bisher getan haben, testen Sie unsere neue Funktion wie folgt:

1. Klicken Sie in der neuen Funktion rechts oben auf **</> Funktions-URL abrufen**, wählen Sie **default (Function key)** (Standard (Funktionsschlüssel)) aus, und klicken Sie dann auf **Kopieren**.

2. Fügen Sie die Funktions-URL, die Sie in der Adressleiste des Browsers kopiert haben. Fügen Sie den Wert der Abfragezeichenfolge `&name=<yourname>` am Ende der URL hinzu, und drücken Sie die Taste `Enter` auf Ihrer Tastatur, um die Anforderung auszuführen. Daraufhin sollte eine Ausgabe ähnlich der folgenden Antwort zurückgegeben, die von der Funktion, die in Ihrem Browser angezeigt.  

Nun, da wir unsere Arbeit auf das Notwendigste-Funktion haben, konzentrieren wir uns zum Lesen von Daten aus Azure Cosmos DB- oder in diesem Szenario hat unsere [!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)] Auflistung.

## <a name="add-a-cosmos-db-input-binding"></a>Hinzufügen einer Cosmos DB-eingabebindung

Wir möchten Lesen von Daten aus der Datenbank, die wir erstellt haben, geben daher die eingabebindungen. Wie Sie sehen werden, können wir eine Bindung konfigurieren, die mit unserer Datenbank in wenigen Schritten kommunizieren können.

1. Wählen Sie **integrieren** in der Funktion im Menü auf der linken Seite auf die Registerkarte "Integration" zu öffnen.

Die verwendeten Vorlage erstellt eine HTTP-Trigger und eine HTTP-ausgabebindung für uns. Fügen Sie unsere neue Azure Cosmos DB-eingabebindung an. 

2. Wählen Sie **+ neue Eingabe** unter der **Eingaben** Spalte. Es wird eine Liste aller möglichen eingabebindung Typen angezeigt.

3. Klicken Sie auf **Azure Cosmos DB** aus der Liste und klicken Sie dann die **wählen** Schaltfläche. Diese Aktion wird die Azure Cosmos DB-Eingabe-Konfigurationsseite geöffnet.

Als Nächstes müssen wir mit unserer Datenbank eine Verbindung einrichten.

4. Im Feld mit dem Namen **Azure Cosmos DB-Kontoverbindung** klicken Sie auf dieser Seite auf *neue* rechts neben das Feld leer. Diese Aktion öffnet den **Verbindung** Dialogfeld, in dem bereits **Azure Cosmos DB-Konto** und Ihrem Azure-Abonnement ausgewählt haben. Nur noch dazu ist die Auswahl eine Datenbank-Id-Konto.

5. Klicken Sie im Abschnitt **Erstellen eines Datenbankkontos**, mussten Sie einen ID-Wert angeben. Suchen Sie nun diesen Wert in der *Datenbankkonto* Dropdownliste, und klicken Sie dann auf **wählen**.

Eine neue Verbindung mit der Datenbank konfiguriert ist, und sehen Sie in der **Azure Cosmos DB-Kontoverbindung** Feld. Wenn Sie neugierig sind was tatsächlich hinter dieser abstrakten Name ist, klicken Sie einfach *Wert anzeigen* um die Verbindungszeichenfolge anzuzeigen.

Wir möchten ein Lesezeichen mit einer bestimmten ID aus, suchen wir die ID zu verknüpfen, wir auf die Bindung erhalten.

7. In der **Dokument-ID (optional)** Feld `{id}`. Dies bezeichnet man als ein *Bindungsausdruck*. Die Funktion wird durch eine HTTP-Anforderung ausgelöst, die eine Abfragezeichenfolge verwendet, um die zu suchende ID anzugeben. Da IDs in der Sammlung eindeutig sind, gibt die Bindung (nicht gefunden) 0 oder 1 (gefunden) Dokumenten zurück.

8. Füllen Sie sorgfältig die verbleibenden Felder auf dieser Seite mit den Werten in der folgenden Tabelle aus. Zu jedem Zeitpunkt können Sie auf das Informationssymbol rechts von den einzelnen Feldnamen, um weitere Informationen zu den Zweck der einzelnen Felder klicken.

|Einstellung  |Wert  |Beschreibung  |
|---------|---------|---------|
|Dokumentparametername     |  **bookmark**       |  Der Name zum Identifizieren dieser Bindung in Ihrem Code verwendet wird.      |
|Datenbankname     |  [!INCLUDE [cosmos-db-name](./cosmos-db-name.md)]       | Die Datenbank, in dem Daten gelesen werden. Dies ist der Datenbankname, die wir zuvor in dieser Lektion legen.        |
|Sammlungsname     |  [!INCLUDE [cosmos-db-name](./cosmos-coll-name.md)]        | Die Auflistung, aus der wir Daten gelesen werden. Diese Einstellung wurde zuvor in dieser Lektion definiert. |
|SQL-Abfrage (optional)    |   Leer lassen       |   Wir sind nur ein Dokument zu einem Zeitpunkt auf der Grundlage der ID abrufen. Filtern mit dem Dokument-ID-Feld ist also besser als die Verwendung einer SQL-Abfrage in dieser Instanz. Es könnte eine SQL-Abfrage zum Zurückgeben von einem Eintrag erstellen (`SELECT * from b where b.ID = {id}`). Diese Abfrage würde ein Dokument zurückgeben, aber es wäre es in einer Dokumentsammlung zurückgegeben. Unser Code müsste eine Sammlung unnötigerweise zu bearbeiten. Verwenden Sie den SQL-Abfrage-Ansatz, wenn mehrere Dokumente abgerufen werden soll.   |
|Partitionsschlüssel (optional)     |   Leer lassen      |  Wir können hier die Standardeinstellung übernehmen.       |

9. Klicken Sie auf **speichern** , alle Änderungen an der Konfiguration dieser Bindung zu speichern. Nun, da wir unsere Bindung definiert haben, ist es Zeit für die Verwendung in unserer Funktion an.

## <a name="update-function-implementation"></a>Implementierung der Update-Funktion

1. Klicken Sie auf unserer Funktion [!INCLUDE [func-name-find](./func-name-find.md)], öffnen Sie *"Index.js"* im Code-Editor. Wir haben eine eingabebindung an der Datenbank lesen, aktualisieren wir also die Logik für diese Bindung verwenden, hinzugefügt.

2. Ersetzen Sie alle Code in "Index.js", mit dem Code aus den folgenden Codeausschnitt:

[!code-javascript[](../code/find-bookmark-single.js)]

Wenn eine HTTP-Anforderung bewirkt, unsere Funktion dass auslösen, die `id` Abfrageparameter an unsere Cosmos DB-eingabebindung übergeben wird. Wenn es sich um ein Dokument gefunden, die diese ID entspricht der `bookmark` Parameter, festgelegt. In diesem Fall erstellen wir eine Antwort mit dem URL-Wert, der im Dokument Lesezeichen gefunden. Wenn kein Dokument mit diesem Schlüssel übereinstimmt gefunden wurde, reagieren wir mit einer Nutzlast und einen Statuscode, der dem Benutzer mitteilt, die schlechte Nachricht wann.

## <a name="try-it-out"></a>Ausprobieren

1. Wie üblich, klicken Sie auf **<> / Get Funktions-URL** wählen Sie oben rechts, **Standard (Funktionstaste)**, und klicken Sie dann auf **Kopie** , kopieren Sie die Funktion der URL.

2. Fügen Sie die Funktions-URL, die Sie in der Adressleiste des Browsers kopiert haben. Fügen Sie den Wert der Abfragezeichenfolge `&id=docs` am Ende der URL hinzu, und drücken Sie die Taste `Enter` auf Ihrer Tastatur, um die Anforderung auszuführen. Alle hier auch eine Antwort angezeigt werden soll, die eine URL für diese Ressource enthält.

3. Ersetzen Sie dies `&id=docs` mit `&id=missing` und beobachten Sie die Antwort.

4. Ersetzen Sie die vorherigen Abfragezeichenfolge mit `&id=` und beobachten Sie die Antwort.

>[!TIP]
>Sie können auch testen, die Funktion mithilfe der **testen** Registerkarte in der Benutzeroberfläche des Portals Funktion. Sie können einen Abfrageparameter hinzufügen, oder geben nur einen Anforderungstext, um die gleichen Ergebnisse zu erhalten, wie in den vorangehenden Schritten Te beschrieben.

In dieser Einheit haben wir unsere erste eingabebindung manuell, um aus einer Azure Cosmos DB-Datenbank zu lesen. Die Menge an Code, den wir in unserer Datenbank suchen und Lesen von Daten geschrieben waren minimal, Dank Bindungen. Wir haben die meisten unserer Arbeit mit dem Konfigurieren der Bindung deklarativ und die Plattform sorgte den Rest.  

In der nächsten Einheit fügen wir, dass mehr Daten, die Lesezeichen-Sammlung über ein Azure Cosmosdb-ausgabebindung.

> [!TIP]
> Diese Einheit ist nicht vorgesehen, um ein Tutorial für Azure Cosmos DB werden. Wenn Sie, einen tieferen Einblick möchten, sind hier einige Ressourcen, die Ihnen den Einstieg erleichtern:
>
>* [Einführung in Azure Cosmos DB: SQL-API](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)
>
>* [Eine technische Übersicht über Azure Cosmos DB](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)
>
>* [Dokumentation für Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/)