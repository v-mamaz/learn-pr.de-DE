Bevor Sie eine Verbindung der Datenbank mit Ihrer App herstellen, sollten Sie überprüfen, ob Sie eine Verbindung zu ihr herstellen, ihr eine einfache Tabelle hinzufügen und mit Beispieldaten arbeiten können.

Wir verwalten die Infrastruktur, Softwareupdates und Patches für Ihre Azure SQL-Datenbank. Darüber hinaus können Sie Ihre Azure SQL-Datenbank wie jede andere SQL Server-Installation behandeln. Sie können z.B. Visual Studio, SQL Server Management Studio, SQL Server Operations Studio oder andere Tools zum Verwalten von Azure SQL-Datenbank verwenden.

Wie Sie auf die Datenbank zugreifen und die Verbindung zwischen ihr und Ihrer App herstellen, bleibt Ihnen überlassen. Aber um ein wenig Erfahrung in der Arbeit mit Ihrer Datenbank zu sammeln, stellen Sie hier direkt aus dem Portal eine Verbindung mit ihr her, erstellen eine Tabelle und führen einige grundlegende CRUD-Vorgänge aus. Sie lernen Folgendes:

- Was Cloud Shell ist und wie Sie über das Portal darauf zugreifen.
- Wie Sie über Azure CLI auf Informationen zu Ihrer Datenbank zugreifen, einschließlich der Verbindungszeichenfolgen.
- Wie Sie mittels `sqlcmd` eine Verbindung mit Ihrer Datenbank herstellen.
- Wie Sie die Datenbank mit einer grundlegenden Tabelle und einigen Beispieldaten initialisieren.

## <a name="what-is-azure-cloud-shell"></a>Was ist Azure Cloud Shell?

Azure Cloud Shell ist eine browserbasierte Shell zum Verwalten und Entwickeln von Azure-Ressourcen. Stellen Sie sich Cloud Shell als eine interaktive Konsole vor, die in der Cloud ausgeführt wird.

Hinter den Kulissen wird Cloud Shell unter Linux ausgeführt. Aber abhängig davon, ob Sie eine Linux- oder Windows-Umgebung bevorzugen, haben Sie zwei Oberflächen zur Auswahl: Bash und PowerShell.

Auf Cloud Shell können Sie von überall zugreifen. Außer vom Portal können Sie auch von [shell.azure.com](https://shell.azure.com/), der mobilen Azure-App oder Visual Studio Code aus auf Cloud Shell zugreifen.

Cloud Shell umfasst beliebte Tools und Text-Editoren. Hier lernen Sie kurz `az`, `jq` und `sqlcmd` kennen, drei Tools, die Sie für unsere aktuelle Aufgabe verwenden.

- `az` wird auch als Azure CLI bezeichnet. Dies ist die Befehlszeilenschnittstelle für die Arbeit mit Azure-Ressourcen. Sie verwenden sie, um Informationen zu Ihrer Datenbank einschließlich der Verbindungszeichenfolge zu erhalten.
- `jq` ist ein Befehlszeilen-JSON-Parser. Sie reichen die Ausgabe von `az`-Befehlen an dieses Tool weiter, um wichtige Felder aus der JSON-Ausgabe zu extrahieren.
- Mit `sqlcmd` können Sie Anweisungen auf einer SQL Server-Instanz ausführen. Mit `sqlcmd` erstellen Sie eine interaktive Sitzung mit Ihrer Azure SQL-Datenbankinstanz.

## <a name="get-information-about-your-azure-sql-database"></a>Abrufen von Informationen zu Ihrer Azure SQL-Datenbankinstanz

Bevor Sie eine Verbindung mit Ihrer Datenbank herstellen, sollten Sie überprüfen, ob sie vorhanden und online ist.

Hierzu öffnen Sie Cloud Shell, und verwenden Sie das `az`-Hilfsprogramm zum Auflisten Ihrer Datenbanken und Anzeigen von Informationen zur **Logistics**-Datenbank einschließlich maximaler Größe und Status.

1. Klicken Sie im Portal im oberen Bereich auf **Cloud Shell**.

1. Die von Ihnen ausgeführten `az`-Befehle erfordern den Namen Ihrer Ressourcengruppe und den Namen Ihres logischen Azure SQL-Servers. Um sich das Eintippen zu ersparen, führen Sie diesen `azure configure`-Befehl aus, um sie als Standardwerte anzugeben.
    Ersetzen Sie `contoso-logistics` durch den Namen Ihres logischen Azure SQL-Servers.

    ```azurecli
    az configure --defaults group=logistics-db-rg sql-server=contoso-logistics
    ```

1. Führen Sie `az sql db list` zum Auflisten aller Datenbanken auf dem logischen Azure SQL-Server aus.

    ```azurecli
    az sql db list
    ```
    Sie sehen einen großen JSON-Block als Ausgabe.

1. Da wir nur die Datenbanknamen benötigen, führen Sie den Befehl ein zweites Mal aus. Reichen Sie die Ausgabe diesmal an `jq` weiter, um nur die Namensfelder auszugeben.
    ```azurecli
    az sql db list | jq '[.[] | {name: .name}]'
    ```
    Sie sehen Folgendes.
    ```console
    [
      {
        "name": "Logistics"
      },
      {
        "name": "master"
      }
    ]
    ```
    **Logistics** ist Ihre Datenbank. Wie SQL Server enthält **master** Servermetadaten wie Anmeldekonten und Systemkonfigurationseinstellungen.

1. Führen Sie diesen `az sql db show`-Befehl aus, um Details zur **Logistics**-Datenbank zu erhalten.

    ```azurecli
    az sql db show --name Logistics
    ```
    Wie bereits zuvor sehen Sie einen großen JSON-Block als Ausgabe.

1. Führen Sie den Befehl ein zweites Mal aus. Reichen Sie die Ausgabe diesmal an `jq` weiter, um die Ausgabe auf den Namen, die maximale Größe und den Status der **Logistics**-Datenbank zu beschränken.

    ```azurecli
    az sql db show --name Logistics | jq '{name: .name, maxSizeBytes: .maxSizeBytes, status: .status}'
    ```
    Sie sehen, dass die Datenbank online ist und ca. 2 GB Daten enthalten kann.
    ```console
    {
      "name": "Logistics",
      "maxSizeBytes": 2147483648,
      "status": "Online"
    }
    ```

## <a name="connect-to-your-database"></a>Herstellen einer Verbindung mit Ihrer Datenbank

Da Sie nun etwas mit Ihrer Datenbank vertraut sind, lassen Sie uns eine Verbindung mit ihr unter Verwendung von `sqlcmd` herstellen, eine Tabelle erstellen, die Informationen über Transportfahrer enthält, und einige grundlegende CRUD-Vorgänge ausführen.

Beachten Sie, dass CRUD für **Create (Erstellen)**, **Read (Lesen)**, **Update (Aktualisieren)** und **Delete (Löschen)** steht. Dies bezieht sich auf Vorgänge, die Sie an Tabellendaten ausführen, und diese vier grundlegenden Vorgänge benötigen Sie für Ihre App. Jetzt ist ein guter Zeitpunkt, um zu überprüfen, ob Sie sie jeweils ausführen können.

1. Führen Sie diesen `az sql db show-connection-string`-Befehl aus, um die Verbindungszeichenfolge zum Herstellen der Verbindung mit der **Logistics**-Datenbank in einem Format abzurufen, das `sqlcmd` verwenden kann.

    ```azurecli
    az sql db show-connection-string --client sqlcmd --name Logistics
    ```
    Die Ausgabe sieht ungefähr so aus.
    ```console
    "sqlcmd -S tcp:contoso-1.database.windows.net,1433 -d Logistics -U <username> -P <password> -N -l 30"
    ```

1. Führen Sie die `sqlcmd`-Anweisung aus dem vorherigen Schritt aus, um eine interaktive Sitzung zu erstellen.
    Entfernen Sie die umgebenden Anführungszeichen, und ersetzen Sie `<username>` und `<password>` durch den Benutzernamen und das Kennwort, die Sie beim Erstellen der Datenbank angegeben haben. Hier sehen Sie ein Beispiel.

    ```console
    sqlcmd -S tcp:contoso-1.database.windows.net,1433 -d Logistics -U martina -P "password1234$" -N -l 30
    ```

    > [!TIP]
    > Setzen Sie Ihr Kennwort in Anführungszeichen, damit „&“ und andere Sonderzeichen nicht als Verarbeitungsanweisungen interpretiert werden.

1. Erstellen Sie von Ihrer `sqlcmd`-Sitzung aus eine Tabelle mit dem Namen `Drivers`.

    ```sql
    CREATE TABLE Drivers (DriverID int, LastName varchar(255), FirstName varchar(255), OriginCity varchar(255) );
    GO
    ```

    Die Tabelle enthält vier Spalten: einen eindeutigen Bezeichner, Nach- und Vorname des Fahrers und den Herkunftsort des Fahrers.

    > [!NOTE]
    > Die hier gezeigte Sprache ist Transact-SQL, auch als T-SQL bezeichnet.

1. Überprüfen Sie, ob die `Drivers`-Tabelle vorhanden ist.

    ```sql
    SELECT name FROM sys.tables;
    GO
    ```

    Sie sehen Folgendes.

    ```console
    name
    --------------------------------------------------------------------------------------------------------------------------------
    Drivers

    (1 rows affected)
    ```

1. Führen Sie diese `INSERT`-T-SQL-Anweisung aus, um der Tabelle eine Beispielzeile hinzuzufügen. Dies ist der **Create**-Vorgang.

    ```sql
    INSERT INTO Drivers (DriverID, LastName, FirstName, OriginCity) VALUES (123, 'Zirne', 'Laura', 'Springfield');
    GO
    ```

    Dies zeigt Ihnen an, dass der Vorgang erfolgreich war.

    ```console
    (1 rows affected)
    ```

1. Führen Sie diese `SELECT`-T-SQL-Anweisungsliste für die `DriverID`-Spalte aller Zeilen in der Tabelle aus. Dies ist der **Read**-Vorgang.

    ```sql
    SELECT DriverID FROM Drivers;
    GO
    ```

    Daraufhin wird ein Ergebnis angezeigt, die `DriverID` für die Zeile, die Sie im vorherigen Schritt erstellt haben.

    ```console
    DriverID
    -----------
            123

    (1 rows affected)
    ```

1. Führen Sie diese `UPDATE`-T-SQL-Anweisung aus, um den Herkunftsort für den Fahrer mit der `DriverID` „123“ von „Springfield“ in „Springfield, OR“ zu ändern. Dies ist der **Update**-Vorgang.

    ```sql
    UPDATE Drivers SET OriginCity='Springfield, AK' WHERE DriverID=123;
    GO
    ```

    Sie sehen Folgendes.

    ```console
    (1 rows affected)
    ```

1. Führen Sie diese `DELETE`-T-SQL-Anweisung aus, um den Datensatz zu löschen. Dies ist der **Delete**-Vorgang.

    ```sql
    DELETE FROM Drivers WHERE DriverID=123;
    GO
    ```

    ```console
    (1 rows affected)
    ```

1. Führen Sie diese `SELECT`-T-SQL-Anweisung aus, um zu überprüfen, ob die `Drivers`-Tabelle leer ist.

    ```sql
    SELECT COUNT(*) FROM Drivers;
    GO
    ```

    Sie sehen, dass die Tabelle keine Zeilen enthält.

    ```console
    -----------
              0

    (1 rows affected)
    ```

## <a name="summary"></a>Zusammenfassung

Da Sie nun wissen, wie Sie mittels Cloud Shell mit Azure SQL-Datenbank arbeiten, können Sie die Verbindungszeichenfolge für Ihr bevorzugtes SQL-Verwaltungstool abrufen &ndash; ganz gleich, ob von SQL Server Management Studio, Visual Studio oder sonst wo aus.

Cloud Shell erleichtert Ihnen den Zugriff auf Ihre Azure-Ressourcen und die Arbeit damit. Da Cloud Shell browserbasiert ist, können Sie mit Windows, macOS oder Linux darauf zugreifen &ndash; im Wesentlichen mit jedem System, in dem ein Webbrowser zur Verfügung steht.

Sie gewannen einige praktische Erfahrungen mit der Ausführung von Azure CLI-Befehlen zum Abrufen von Informationen zu Ihrer SQL Azure-Datenbank. Als Bonus übten Sie Ihre T-SQL-Fertigkeiten.

Jetzt kommen wir zum Ende und sehen, wie wir Ihre Datenbank entfernen können.
