Nehmen wir an, dass Sie eine lokale PostgreSQL-Datenbank verwenden. Sie verwalten alle Sicherheitsaspekte, und Sie haben Vollzugriff auf Ihre Server mit den Standardregeln des PostgreSQL-Firewallregel auf Serverebene gesperrt. Nun möchten Sie sicherstellen, dass Sie die gleiche Weise konfigurieren können auf Serverebene Firewall-Regeln in Azure.

## <a name="server-security-considerations-and-connection-methods"></a>Überlegungen zur Sicherheit der Server und Verbindungsmethoden

Sie haben eine Reihe von Optionen, um den Zugriff auf Ihren Azure Database for PostgreSQL-Server und Datenbanken zu beschränken. Zugriff auf das Netzwerk kann auf ein Netzwerk, Server oder Datenbankebene eingeschränkt werden. Sie können eine der folgenden Optionen verwenden:

- Benutzerkonten zum Einschränken des Datenbankzugriffs
- Virtuelle Netzwerke mit Zugriff auf das Netzwerk einschränken
- Firewall-Regeln für den Serverzugriff

### <a name="authentication-and-authorization"></a>Authentifizierung und Autorisierung

Azure Database for PostgreSQL-Server unterstützt native PostgreSQL-Authentifizierung. Sie können eine Verbindung herstellen und authentifizieren Sie sich bei dem Server mit den Anmeldeinformationen für Serveradministrator. Sie erstellen auch Benutzern die Verbindung für bestimmte Datenbanken, um den Zugriff einzuschränken.

### <a name="what-is-a-virtual-network"></a>Was ist ein virtuelles Netzwerk?

Ein virtuelles Netzwerk ist eines logisch isolierten Netzwerks, das im Azure-Netzwerk erstellt wird. Sie können ein virtuelles Netzwerk verwenden, um zu steuern, welche Azure-Ressourcen auf andere Ressourcen verbinden können.

Stellen Sie sich vor, dass Sie eine Webanwendung ausführen, die einer Datenbank herstellt. Sie werden Subnetze verwenden, um verschiedene Teile des Netzwerks zu isolieren. Ein Subnetz ist ein Teil des Netzwerks, die auf einen Bereich von IP-Adressen basieren.

Um diesen Subnetzen zu konfigurieren, Sie erstellen ein virtuelles Netzwerk und dann das Netzwerk in Subnetze unterteilen. Die Webanwendung wird für ein Subnetz und die Datenbank in einem anderen Subnetz verwendet werden. Jedes Subnetz müssen eigene Regeln für die Kommunikation zu und von anderen Netzwerk. Diese Regeln bieten Ihnen die Möglichkeit, den Zugriff auf die Webanwendung aus der Datenbank zu beschränken.

Erstellen eines virtuellen Netzwerks ist, würde den Rahmen dieses Moduls. Wenn Sie weitere Informationen benötigen, untersuchen Sie andere Learning-Module, die im Zusammenhang mit virtuellen Netzwerken.

### <a name="what-is-a-firewall"></a>Was ist eine Firewall?

Eine Firewall ist ein Dienst, der Server den Zugriff auf Grundlage der ursprünglichen IP-Adresse für jede Anforderung gewährt. Sie erstellen Firewallregeln, die IP-Adressbereiche angeben. Nur Clients, die von diesen IP-Adressen erhält Zugriff auf den Server gewährt wurden. Firewall-Regeln, enthalten im Allgemeinen auch bestimmten Netzwerk-Protokoll und Port. Beispielsweise überwacht ein PostgreSQL-Server wird standardmäßig TCP-Anforderungen über Port 5432.

### <a name="azure-database-for-postgresql-server-firewall"></a>Azure-Datenbank für PostgreSQL-Serverfirewall

Azure Database for PostgreSQL-Serverfirewall verhindert jeglichen Zugriff auf Ihren Datenbankserver, bis Sie angeben, welche Computer zugriffsberechtigt sind. Die Konfiguration der Firewall können Sie einen Bereich von IP-Adressen angeben, die für die Verbindung mit dem Server zulässig sind. Der Server verwendet immer die standardmäßigen PostgreSQL-Verbindungsinformationen.

![Funktionsdiagramm für Azure-firewall](../media-draft/7-firewall-diagram.png)

### <a name="azure-database-for-postgresql-server-ssl-connections"></a>Azure-Datenbank für PostgreSQL-Server SSL-Verbindungen

Azure-Datenbank für PostgreSQL bevorzugt, dass Ihre Clientanwendungen mit der PostgreSQL-Dienst mithilfe von Secure Sockets Layer (SSL) verbinden. Erzwingen von SSL-Verbindungen zwischen Ihren Datenbankserver und Clientanwendungen trägt zum Schutz gegen "Man in the Middle" und ähnliche Angriffe durch das Verschlüsseln der Daten zwischen Server und Client. Aktivieren von SSL erfordert den Austausch von Schlüsseln und strenge Authentifizierung zwischen Client und Server für die Verbindung funktioniert. Informationen zur Verwendung von SSL sprengen den Rahmen dieses lernmodul ab. Wenn Sie weitere Informationen benötigen, untersuchen Sie andere Learning-Module, die im Zusammenhang mit SSL.

## <a name="configure-connection-security"></a>Konfigurieren der Sicherheit der Clientverbindung

Sehen wir uns die Entscheidungen und die Schritte, die Sie vornehmen, um einen Azure Database for PostgreSQL-Server-Firewall zu konfigurieren. Sie sehen auch die Verbindung mit dem Server, die Sie zuvor erstellt haben.

Öffnen Sie zunächst die [Azure-Portal](https://portal.azure.com?azure-portal=true) und navigieren Sie zu die Server-Ressource, die für die Sie eine Firewallregel erstellen möchten.

Wählen Sie dann die **Verbindungssicherheit** Option, um das Blatt "verbindungssicherheit" auf der rechten Seite zu öffnen.

![Screenshot des Azure-Portal mit der Verbindung im Sicherheitsabschnitt das Ressourcenblatt des PostgreSQL-Datenbank](../media-draft/7-db-security-settings.png)

Auf diesem Bildschirm müssen Sie mehrere Optionen. Ihre Möglichkeiten:

- Fügen Sie die IP-Adresse, mit denen Sie Zugriff auf das Portal als einen Eintrag für die Firewall durch Klicken auf die **Client-IP hinzufügen** Schaltfläche.
- Zugriff auf Azure-Dienste zulassen. Standardmäßig werden alle Azure-Dienste **nicht** haben Zugriff auf dem PostgreSQL-Server.
- Fügen Sie Firewall-Regeln, indem Sie die IP-Adressbereiche eingeben.
- Erzwingen von SSL-Verbindungen. Diese Option erzwingt, dass der Client die Verbindung mit dem Server mit einem SSL-Zertifikat.

Denken Sie immer daran, auf die **speichern** Symbol oberhalb der Felder für die die aktualisierte Konfiguration zu speichern, nachdem Sie Änderungen vorgenommen haben.

### <a name="allow-access-to-azure-services"></a>Zugriff auf Azure-Dienste erlauben

Um Azure Cloud Shell zum Zugreifen auf oder konfigurieren Sie den Server zu verwenden, müssen Sie Sie aktivieren **ermöglichen den Zugriff auf Azure-Diensten**. Dieser Schritt wird eine Firewallregel hinzuzufügen, die Server-Konfiguration, um den Zugriff über Cloud Shell zu ermöglichen. Diese Regel nicht als eine der benutzerdefinierten Regeln angezeigt, die Sie hinzufügen.

Sie müssen auch deaktivieren **SSL-Verbindung erzwingen**. PowerShell kann nicht mit dem Server verbinden, wenn SSL für Clientverbindungen erforderlich ist.

Beide Optionen führt zu einer Fehlermeldung, die wurde in der Befehlszeile angezeigt, wenn nicht ordnungsgemäß konfiguriert.

Z. B. wenn der Zugriff kann nicht auf Azure-Dienste und Erzwingen von SSL-Verbindungen ist aktiviert und Sie in etwa diesen Fehler sehen, wenn die Firewall den Zugriff blockiert:

> Psql: FATAL: kein pg_hba.conf-Eintrag für Host "123.45.67.89," Benutzer "Adminuser", Datenbank "Postgres", SSL für SCHWERWIEGEND: SSL-Verbindung ist erforderlich. Please specify SSL options and retry.

### <a name="create-a-firewall-rule-using-the-portal"></a>Erstellen einer Firewallregel mithilfe des Portals

Nehmen wir an, dass eine Firewallregel erstellen, die Zugriff über alle IP-Adresse ermöglicht werden soll.

> [!WARNING]
> Erstellen diese Firewallregel auf können eine beliebige IP-Adresse im Internet versuchen, mit dem Server herstellen. Auch wenn bei Clients keine werden Zugriff auf den Server ohne Benutzername und Kennwort, aktivieren Sie diese Regel mit Vorsicht und stellen Sie sicher, dass Sie Auswirkungen auf die Sicherheit kennen.

Sie erstellen eine neue Firewallregel, indem Sie die folgenden Daten in die gekennzeichneten Felder einzugeben:

- Regelname: `AllowAll`
- Start-IP: `0.0.0.0`
- End-IP: `255.255.255.255`

Um eine Firewallregel zu entfernen, müssen Sie die Auslassungspunkte (...) am Ende der Regel klicken, die Sie löschen möchten. Klicken Sie auf die **löschen** Schaltfläche, um die Regel zu löschen.

Klicken Sie auf die **speichern** Symbol oberhalb der Felder für die um das Löschen der Regel zu übernehmen.

### <a name="create-a-firewall-rule-using-the-azure-cli"></a>Erstellen einer Firewallregel mithilfe der Azure CLI

Sie verwenden die Azure-Befehlszeilenschnittstelle, um die Firewallregeln hinzufügen, auf Ihrem Server mit der `az postgres server firewall-rule create` Befehl mithilfe von Azure Cloud Shell.

Nehmen wir an, dass die gleichen Regeln wie oben beschrieben erstellt werden soll. Verwenden Sie den folgenden Befehl ein:

  ```azurecli
  az postgres server firewall-rule create --resource-group <resource_group_name> --server <server-name> --name AllowAll --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
  ```

Entfernen von Firewallregeln vom Server mit dem Befehl `az postgres server firewall-rule delete`.

Nehmen wir an, dass die Firewall zu löschen, die Sie erstellt werden sollen. Anschließend verwenden Sie den folgenden Befehl aus:

  ```azurecli
  az postgres server firewall-rule delete --name AllowAll --resource-group <resource_group_name> --server-name <server-name>
  ```

## <a name="connecting-to-your-server"></a>Herstellen einer Verbindung mit Ihrem server

Wie alle modernen Datenbank erfordert PostgreSQL regelmäßigen serververwaltung, um die optimale Leistung zu erzielen. Sie haben eine Reihe von Optionen zum Verbinden und Verwalten Ihrer Azure Database for PostgreSQL-Server. Wir verwenden `psql` für die Verbindung mit dem Server.

### <a name="what-is-psql"></a>Was ist Psql?

Wird aufgerufen, das Befehlszeilentool `psql` PostgreSQL-Instanz verteilt interaktiven Terminal für die Arbeit mit der PostgreSQL-Server und Datenbanken. `psql` funktioniert mit Azure-Datenbank für PostgreSQL genauso wie bei jeder anderen PostgreSQL-Implementierung und ist im Lieferumfang von Azure Cloud Shell. Die `psql` Tool können Sie zum Verwalten von Datenbanken sowie die Struktur-Abfragen für diese Datenbanken auszuführen.

Mithilfe von `psql` erfordert eine Verbindung mit einer PostgreSQL-Server. Stehen zahlreiche Befehlszeilenparameter für die Verwendung bei der Arbeit mit `psql`.

- `--host` – Der Host, den Sie eine Verbindung herstellen möchten.
- `--username` – Der Name/Benutzername für die Verbindung.
- `--dbname` – Der Name der Datenbank für die Verbindung.

> [!Note]
> Sie werden in der Regel eine Verbindung mit der `postgres` -Verwaltungsdatenbank, wenn Sie die Serverkonfiguration für den Zugriff und die Datenbank zu verwalten.

Hier ist der vollständige Befehl ein:

  ```bash
  psql --host=<server-name>.postgres.database.azure.com --username=<admin-user>@<server-name> --dbname=<database>
  ```

Nach dem Sie verbunden sind, wird eine Eingabeaufforderung angezeigt, und Sie können Befehle auf Ihrem Server und Datenbanken.

Sie haben nun die Schritte gesehen, mit denen Sie Azure-Datenbank für PostgreSQL-Sicherheitseinstellungen konfigurieren. In der nächsten Einheit konfigurieren Sie Azure-Datenbank für PostgreSQL-Sicherheitseinstellungen. Sie müssen auch den Server mithilfe von Cloud Shell eine Verbindung herstellen.
