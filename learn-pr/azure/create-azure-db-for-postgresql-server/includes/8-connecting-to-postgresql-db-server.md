Angenommen, Sie arbeiten mit einer lokalen PostgreSQL-Datenbank. Sie verwalten sämtliche Sicherheitsaspekte und haben den gesamten Zugriff auf Ihre Server mit den standardmäßigen Firewallregeln auf PostgreSQL-Serverebene gesperrt. Sie wissen, wie Sie die gleichen Firewallregeln auf Serverebene in Azure konfigurieren.

Nun haben Sie die Möglichkeit, mithilfe von `psql` eine Verbindung mit einem der zuvor erstellten Azure Database for PostgreSQL-Server herzustellen.

## <a name="allow-azure-service-access"></a>Zulassen des Zugriffs für Azure-Dienste

Vorbereitung: Sie müssen den Zugriff auf Azure-Dienste zulassen, wenn Sie mithilfe von PowerShell und `psql` eine Verbindung mit Ihrem Server herstellen möchten. Zur Erinnerung: Zugriff kann auf zwei Arten zugelassen werden.

Die erste Möglichkeit besteht darin, **Zugriff auf Azure-Dienste erlauben** zu aktivieren. Wenn Sie den Zugriff zulassen, wird eine Firewallregel erstellt. Diese wird jedoch nicht in die Liste mit den benutzerdefinierten Regeln aufgenommen, die Sie erstellen.

Die zweite Möglichkeit besteht darin, eine Firewallregel zu erstellen, die den Zugriff auf alle IP-Adressen zulässt. Die Regel enthält die IP-Adresse für den Client, auf dem PowerShell ausgeführt wird und von dem aus Sie `psql` ausführen.

Darüber hinaus müssen Sie **SSL-Verbindung erzwingen** deaktivieren.

Legen wir los.

Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an. Navigieren Sie zu der Serverressource, für die Sie eine Firewallregel erstellen möchten.

Wählen Sie die Option **Verbindungssicherheit** aus, um auf der rechten Seite das entsprechende Blatt zu öffnen.

![Sicherheitseinstellungen für die PostgreSQL-Datenbank](../media-draft/7-db-security-settings.png)

Zur Erinnerung: Sie möchten den Zugriff auf PowerShell-Clients zulassen, auf denen `psql` ausgeführt wird.

Verwenden Sie eines der folgenden Verfahren:

- Legen Sie **Zugriff auf Azure-Dienste erlauben** auf **EIN** fest.
- Legen Sie **SSL-Verbindung erzwingen** auf **DEAKTIVIERT** fest.
- Klicken Sie auf die Schaltfläche **Speichern**, um die Änderungen zu speichern.

Oder: Fügen Sie eine Firewallregel hinzu, um den Zugriff auf alle IP-Adressen zuzulassen. Verwenden Sie folgende Werte:

- Regelname: `AllowAll`
- Start-IP: `0.0.0.0`
- End-IP: `255.255.255.255`
- Legen Sie **SSL-Verbindung erzwingen** auf **DEAKTIVIERT** fest.
- Klicken Sie auf die Schaltfläche **Speichern**, um die Änderungen zu speichern.

> [!Warning]
> Wenn Sie diese Firewallregel erstellen, kann über jede IP-Adresse im Internet versucht werden, eine Verbindung mit Ihrem Server herzustellen. Ohne Benutzername und Kennwort können Clients zwar nicht auf den Server zugreifen, aktivieren Sie diese Regel aber dennoch mit Bedacht und nur, wenn Sie verstehen, was das für die Sicherheit bedeutet. In Produktionsumgebungen lassen Sie den Zugriff nur für bestimmte Client-IP-Adressen zu.

Für die nächsten Schritte benötigen wir eine Azure Cloud Shell-Sitzung. In diesem Lab wird `bash` als Befehlszeilenumgebung verwendet.

- Öffnen Sie Cloud Shell über das Azure-Portal. Klicken Sie im [Azure-Portal](https://portal.azure.com?azure-portal=true) auf die Schaltfläche „Cloud Shell öffnen“:

  ![Cloud Shell-Schaltfläche](../media-draft/cloud-shell-button.png)

- Sollten Sie über mehrere Abonnements verfügen, vergewissern Sie sich, dass Sie das richtige Abonnement verwenden, wenn Sie dazu aufgefordert werden. Sie können auch den folgenden Befehl ausführen, um das aktive Abonnement festzulegen. Vergessen Sie nicht, die Nullen durch Ihre Abonnement-ID zu ersetzen.

   ```bash
   az account set --subscription 00000000-0000-0000-0000-000000000000
   ```

- Verbinden Sie psql mithilfe des folgenden Befehls mit Ihrem Server:

  ```bash
  psql --host=<server-name>.postgres.database.azure.com --username=<admin-user>@<server-name> --dbname=postgres
  ```

   `server-name` und `admin-user` sind die Werte, die Sie beim Erstellen des Servers für Ihr Administratorkonto ausgewählt haben. `postgres` ist die standardmäßige Verwaltungsdatenbank, mit der jeder PostgreSQL-Server erstellt wird. Sie werden zur Eingabe des Kennworts aufgefordert, das Sie beim Erstellen des Servers angegeben haben.

- Führen Sie nach erfolgreicher Verbindungsherstellung den Befehl `\l` aus, um alle Datenbanken aufzulisten.

   Daraufhin werden mindestens zwei Standarddatenbanken zurückgegeben.

- Wenn Sie auf Ihrem Server keine weiteren psql-Vorgänge mehr ausführen möchten, führen Sie den Befehl `\q` aus, um `psql` zu beenden.

- Führen Sie abschließend den Befehl `exit` aus, um Cloud Shell zu beenden.
