In dieser Einheit bewerten Sie eine vorhandene Datenbank mithilfe des Datenmigrations-Assistenten und überprüfen alle Funktionen, die in der lokalen SQL Server-Instanz verwendet und derzeit nicht von Azure SQL-Datenbank unterstützt werden.

## <a name="setup"></a>Einrichtung

1. [Installieren Sie den **Datenmigrations-Assistenten**](https://www.microsoft.com/download/details.aspx?id=53595), wenn Sie dies noch nicht getan haben.

1. Dazu muss eine SQL Server-Instanz ausgeführt werden. Außerdem müssen Sie die Verbindungsdetails zur Hand haben.

<!-- 1. [**** likely replace with an LOD VM *****] TODO: -->

1. Öffnen Sie einen Internetbrowser, und navigieren Sie zu https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.

1. Klicken Sie unter **OLTP downloads** (OLTP-Downloads) auf **AdventureWorks2008R2.bak**, und speichern Sie die Datei auf Ihrem lokalen Computer.

1. Stellen Sie *AdventureWorks 2008R2* in Management Studio auf Ihrer Standardinstanz wieder her.

## <a name="create-an-assessment"></a>Erstellen einer Bewertung

1. Starten Sie **Microsoft-Datenmigrations-Assistent**.

1. Klicken Sie im linken Navigationsbereich der App auf __+__, um ein neues Datenmigrations-Assistent-Projekt zu erstellen.

1. Geben Sie die folgenden Optionen an:

    - **Projekttyp:** Wählen Sie *Bewertung* aus.
    - **Projektname:** Geben Sie einen Namen für Ihr Projekt ein, z.B. „FahrradDB-Bewertung“.
    - **Typ des Quellservers:** Wählen Sie *SQL Server* aus.
    - **Typ des Zielservers:** Wählen Sie *Azure SQL-Datenbank*.

1. Klicken Sie auf **Erstellen**.
    ![Screenshot der beschriebenen Konfiguration in Datenmigrations-Assistent für Ihre AdventureWorks-SQL Server-Daten](../media-draft/3-create-assessment.png)

1. Wählen Sie den Typ des Bewertungsberichts aus, und überprüfen Sie Folgendes:
    - Datenbankkompatibilität überprüfen
    - Check feature parity (Featureparität prüfen)

1. Klicken Sie auf **Weiter**.

## <a name="add-databases-to-assess"></a>Auswählen zu bewertender Datenbanken

1. Klicken Sie auf **Quellen hinzufügen**, um das Verbindungsmenü zu öffnen.

1. Gehen Sie wie folgt vor:

    - Geben Sie den Namen Ihrer vorhandenen SQL Server-Instanz ein.
    - Wählen Sie den **Authentifizierungstyp** aus.
    - Geben Sie die Verbindungseigenschaften für Ihren Server ein.

1. Klicken Sie auf **Verbinden**.

1. Wählen Sie unter **Quellen hinzufügen** die Datenbanken aus, die bewertet werden sollen. Wählen Sie für diese Übung **AdventureWorks2008R2** aus.

1. Klicken Sie auf **Hinzufügen**.
    > [!NOTE]
    > Verwenden Sie zum Hinzufügen von Datenbanken aus mehreren SQL Server-Instanzen die Schaltfläche **Quellen hinzufügen**. Wenn Sie mehrere Datenbanken entfernen möchten, drücken Sie UMSCHALT+STRG, um die zu entfernenden Datenbanken auszuwählen, und klicken Sie dann auf **Quellen entfernen**.

1. Klicken Sie auf **Bewertung starten**.

## <a name="view-results"></a>Anzeigen der Ergebnisse

Wenn mehrere Datenbanken vorhanden sind, werden die Ergebnisse der einzelnen Datenbanken angezeigt, sobald diese verfügbar sind. Sie müssen nicht warten, bis alle Datenbankbewertungen abgeschlossen wurden.

1. Nachdem die Bewertung für **AdventureWorks** abgeschlossen wurde, klicken Sie auf **Compatibility issues** (Kompatibilitätsprobleme) und **Featureempfehlungen**, um die Ergebnisse anzuzeigen.

    - Die Kategorie „SQL Server-Featureparität“ enthält Features, die möglicherweise nicht vollständig unterstützt werden, und Schritte, um diese Probleme zu beheben. Migrationen werden jedoch aufgrund von Problemen mit der Featureparität nicht beendet.
    - Die Kategorie „Kompatibilitätsprobleme“ enthält Features, die eine Migration beenden würden, und Schritte, um diese Probleme zu beheben.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie eine lokal installierte SQL Server-Datenbank bewertet, um zu überprüfen, ob Features nicht verfügbar wären, wenn Sie die Datenbank zu Azure SQL-Datenbank migrieren.