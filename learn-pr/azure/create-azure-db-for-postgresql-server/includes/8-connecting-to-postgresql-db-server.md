Nehmen wir an, dass Sie eine lokale PostgreSQL-Datenbank nutzen. Sie verwalten alle Sicherheitsaspekte, und Sie haben Vollzugriff auf Ihre Server mit den Standardregeln des PostgreSQL-Firewallregel auf Serverebene gesperrt. Sie verfügen jetzt über ein gutes Verständnis dafür, wie Sie die gleichen Firewallregeln auf Serverebene in Azure konfigurieren.

Sie verfügen nun über die Möglichkeit, die mit einer der vorherigen Azure-Datenbank für PostgreSQL-Server herstellen, die Sie erstellt haben, mithilfe von `psql`.

## <a name="allow-azure-service-access"></a>Zulassen des Zugriffs für Azure-Dienst

Bevor wir beginnen, müssen Sie den Zugriff auf Azure-Dienste zu ermöglichen, wenn Sie PowerShell verwenden möchten und `psql` für die Verbindung mit Ihrem Server. Denken Sie daran, dass Sie den Zugriff auf zwei Arten ermöglichen können.

Die erste Möglichkeit besteht, zu **zulassen des Zugriffs auf Azure-Dienste**. Gewähren des Zugriffs wird eine Firewallregel erstellen, auch wenn die Regel in der Liste der benutzerdefinierten Regeln eingegeben ist nicht, die Sie erstellen.

Die zweite Option besteht darin eine Firewallregel zu erstellen, die Zugriff auf alle IP-Adressen zulässt. Die Regel enthält die IP-Adresse für den Client Ausführen von PowerShell, die Sie zum Ausführen verwenden `psql` aus.

Sie müssen außerdem deaktivieren Sie die **SSL-Verbindung erzwingen** Option.

Wir beginnen.

Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an. Navigieren Sie zu die Server-Ressource, die für die Sie eine Firewallregel erstellen möchten.

Wählen Sie die **Verbindungssicherheit** Option, um das Blatt "verbindungssicherheit" auf der rechten Seite zu öffnen.

![Screenshot des Azure-Portal mit der Verbindung im Sicherheitsabschnitt das Ressourcenblatt des PostgreSQL-Datenbank](../media-draft/7-db-security-settings.png)

Beachten Sie, die Zugriff auf PowerShell-Clients, die ausgeführt werden sollen `psql`.

Sie können entweder:

- Legen Sie **zulassen des Zugriffs auf Azure-Dienste** zu **ON**
- Legen Sie **SSL-Verbindung erzwingen** zu **deaktiviert**
- Klicken Sie auf die **speichern** Schaltfläche, um die Änderungen zu speichern

Oder Sie können eine Firewallregel für den Zugriff auf alle IP-Adressen durch das Hinzufügen einer Firewallregel hinzufügen. Verwenden Sie die folgenden Werte:

- Regelname: `AllowAll`
- Start-IP: `0.0.0.0`
- End-IP: `255.255.255.255`
- Legen Sie **SSL-Verbindung erzwingen** zu **deaktiviert**
- Klicken Sie auf die **speichern** Schaltfläche, um die Änderungen zu speichern

> [!Warning]
> Erstellen diese Firewallregel auf können eine beliebige IP-Adresse im Internet versuchen, mit dem Server herstellen. Obwohl Clients Zugriff auf den Server ohne Benutzername und Kennwort nicht, aktivieren Sie diese Regel mit Vorsicht, und stellen Sie sicher, dass Sie Auswirkungen auf die Sicherheit kennen. In produktionsumgebungen müssen Sie nur den Zugriff auf bestimmte Client-IP-Adressen zulassen.

Verbinden Sie in der Azure Cloud Shell Psql auf Ihren Server mit dem folgenden Befehl ein:

```bash
psql --host=<server-name>.postgres.database.azure.com --username=<admin-user>@<server-name> --dbname=postgres
```

Denken Sie daran, `server-name`, und `admin-user` sind die Werte, die Sie für das Administratorkonto ausgewählt haben, wenn Sie auf den Server erstellt haben. `postgres` ist die Standard-Verwaltungsdatenbank alle PostgreSQL-Server mit erstellt wird. Sie werden für das Kennwort aufgefordert werden, die Sie bereitgestellt werden, wenn Sie auf den Server erstellt haben.

Führen Sie nach erfolgreicher verbindungsherstellung die `\l` Befehl zum Auflisten aller Datenbanken. Dieser Befehl führt zu zwei oder mehr Standarddatenbanken zurückgegeben.

Wenn Sie die Psql-Vorgänge auf dem Server ausgeführt haben, führen Sie den Befehl `\q` beenden `psql`.

Um Cloud Shell zu beenden, führen Sie abschließend den Befehl `exit`.
