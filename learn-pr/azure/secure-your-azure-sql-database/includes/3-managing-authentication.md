Nehmen wir an, dass Sie eine Website und ein Angreifer, die sich bereits Zugriff auf Ihre Datenbank ausführen. Der Angreifer erlangt Zugriff auf ein Konto Dbo im Angriff und jeder Vorgang in der Datenbank ausführen. Ein Dbo-Konto kann Zugriff auf und Bearbeiten von Informationen wie z. B. Metadaten und führen Sie alle Ebenen des Zugriffs.

Wenn der Angreifer nur Zugriff auf ein normales Benutzerkonto erlangt, kann dann nur Tabellen, Sichten, gespeicherte Prozeduren und anderen Objekten definiert, die für dieses Benutzerkonto Zugriff auf. Z. B. wenn eine Website, die Zugriff auf eine Datenbank aufgrund eines SQL Injection-Angriffs kompromittiert wurde, würde der Angreifer beschränkt werden in was sie tun könnten.

Für den Fall, dass eine sicherheitsverletzung der Fall ist, unterstützt er um die Auswirkungen der sicherheitsverletzung zu verringern. Sehen wir uns zum Einschränken des Zugriffs auf die SQL Azure-Datenbank auf der Benutzerebene an.

## <a name="reduce-the-attack-surface-of-the-database"></a>Reduzieren der Angriffsfläche der Datenbank

Um die Auswirkungen jeder sicherheitsverletzung zu reduzieren, schränken Sie die Oberfläche des Angriffs. Wenn Sie eine Verbindung herstellen mit Ihrer Datenbank, die mit einem Konto Dbo oder Administrator, und ein Angreifer Zugriff auf die Datenbank erhält, hat der Angreifer Zugriff auf alle Vorgänge für die Datenbank ausführen. Zugriff kann gehören, Abfragen der Datenbankmetadaten, bestimmen, welche Daten verfügbar und/oder sensible ist und Ausnutzen dieser Informationen.

Sie vermeiden dieses Sicherheitsrisiko durch Erstellen von Datenbankbenutzern, die über eingeschränkte Berechtigungen haben. Wir verwenden den Begriff mit minimalprivilegien hier, wie die Benutzer nur Zugriff auf die Tabellen, Sichten, gespeicherte Prozeduren und anderen Entitäten, die für die Arbeit benötigt haben sollen.

## <a name="create-a-database-user"></a>Erstellen eines Datenbankbenutzers

Um einen Benutzer mit eingeschränkten Rechten zu erstellen, Sie erstellen einen Datenbankbenutzer und klicken Sie dann die Datenbank, Benutzer zuordnen. SQL Server-Benutzer erstellen, und geben Sie die Benutzerberechtigungen in der Datenbank.

> [!Note]
> Es gibt 13 (13) Typen von Benutzern in SQL Server. Wenn Sie eine andere Art von Datenbankbenutzer erstellen müssen, verwenden Sie den entsprechenden Link, um zu ermitteln, die richtige Syntax. Finden Sie unter [Erstellen eines Datenbankbenutzers](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-database-user?view=sql-server-2017).

Bevorzugte Methode ist, um den Benutzer auf Datenbankebene zu erstellen. Dieser Schritt wird verhindert, dass Benutzerberechtigungen innerhalb der Grenzen der Datenbank, die Sie schützen möchten.

1. Wählen Sie zuerst die Datenbank ein.
2. Erstellen Sie dann den Benutzer über die folgende Abfrage aus:

   ```sql
   CREATE USER MyWebAppUser WITH PASSWORD = '<YourSuperStrongPassword>';
   ```

   Die vorherige Abfrage wird der Benutzer erstellt *MyWebUser*. Standardmäßig wird der Benutzer nicht nicht auf alle Tabellen, Sichten oder gespeicherte Prozeduren zugreifen.

3. Nun erstellen Sie entsprechende Berechtigungen für den Benutzer, indem sie Rollen wie z. B. Db_datareader und Db_datawriter hinzugefügt.

   Die Rolle "Db_datareader" ermöglicht den Benutzerzugriff auf alle Benutzertabellen und Sichten in der Datenbank. Ebenso wird die Rolle "Db_datawriter" ermöglichen den Benutzerzugriff auf das Lesen, schreiben, aktualisieren, und Löschen von Zeilen in der Datenbank.

   ```sql
   ALTER ROLE db_datareader ADD MEMBER MyWebAppUser;
   ALTER ROLE db_datawriter ADD MEMBER MyWebAppUser;
   ```

Sie können den Benutzerzugriff auf andere Elemente innerhalb der Datenbank mithilfe des DENY-Operators verweigern. Hier sind Sie dem Benutzer MyWebAppUser die Möglichkeit, auswählen von Daten aus der Customers-Tabelle verweigern.

```sql
DENY SELECT ON Customers TO MyWebAppUser;
```

Sie können auch die GRANT-Berechtigung explizit gewähren einem Benutzer oder Rolle verwenden.

```sql
GRANT SELECT ON Customers TO MyWebAppUser;
```

Sie werden weiterhin die Vorgänge in der Datenbank zu optimieren, um den Benutzer auf die Ebene des Zugriffs erforderlich zu erhalten. Anstelle eines Benutzers können Sie eine Rolle mit den mindestens erforderlichen Berechtigungen erstellen, und klicken Sie dann den Benutzer zur Rolle hinzufügen.

Wenn Sie mehrere Benutzer, die die gleichen Berechtigungen verfügen verfügen, können Sie diese Benutzer als Teil der Rolle erstellen. Der Benutzer hat nur Zugriff auf Dinge, die sie benötigen, nachdem alle Zugriffsberechtigungen erteilt oder verweigert wurden.
Wenn ein Angreifer Zugriff auf die Datenbank durch den neu erstellten Benutzer erhält, werden sie nur finden Sie unter und führen Sie die gleichen Daten und Vorgänge, die der Benutzer kann. Sperren des Benutzerzugriffs erheblich verringert die Oberfläche der Angriff auf die Datenbank.
