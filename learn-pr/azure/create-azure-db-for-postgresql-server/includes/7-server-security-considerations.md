Angenommen, Sie arbeiten mit einer lokalen PostgreSQL-Datenbank. Sie verwalten sämtliche Sicherheitsaspekte und haben alle Zugriffe auf Ihre Server mit den Standardfirewallregeln auf PostgreSQL-Serverebene gesperrt. Sie möchten nun sicherstellen, dass Sie die gleichen Firewallregeln auf Serverebene in Azure konfigurieren können.

## <a name="server-security-considerations-and-connection-methods"></a>Überlegungen zur Sicherheit von Servern und Verbindungsmethoden

Sie haben verschiedene Möglichkeiten, den Zugriff auf Ihren Azure Database for PostgreSQL-Server und Ihre Datenbanken einzuschränken. Der Netzwerkzugriff kann auf Netzwerk-, Server- oder Datenbankebene eingeschränkt werden. Sie können auch eine der folgenden Optionen verwenden:

- Benutzerkonten zum Einschränken des Datenbankzugriffs
- Virtuelle Netzwerke zum Einschränken des Netzwerkzugriffs
- Firewallregeln zum Einschränken des Serverzugriffs

### <a name="authentication-and-authorization"></a>Authentifizierung und Autorisierung

Der Azure Database for PostgreSQL-Server unterstützt die native PostgreSQL-Authentifizierung. Mit den Anmeldeinformationen des Serveradministrators können Sie eine Verbindung mit dem Server herstellen und diesen authentifizieren. Sie erstellen auch Benutzerkonten zum Herstellen einer Verbindung mit bestimmten Datenbanken, um den Zugriff einzuschränken.

### <a name="what-is-a-virtual-network"></a>Was ist ein virtuelles Netzwerk?

Ein virtuelles Netzwerk ist ein logisch isoliertes Netzwerk in Azure, das im Azure-Netzwerk erstellt wird. Sie können mithilfe eines virtuellen Netzwerks steuern, welche Azure-Ressourcen eine Verbindung mit anderen Ressourcen herstellen können.

Stellen Sie sich vor, Sie betreiben eine Webanwendung, die eine Verbindung mit einer Datenbank herstellt. Sie verwenden Subnetze, um verschiedene Teile des Netzwerks zu isolieren. Ein Subnetz ist ein Teil eines Netzwerks, der auf einem IP-Adressbereich basiert.

Um diese Subnetze zu konfigurieren, erstellen Sie ein virtuelles Netzwerk, das Sie anschließend in Subnetze unterteilen. Die Webanwendung wird in einem Subnetz, die Datenbank in einem anderen betrieben. Jedes Subnetz verfügt über eigene Regeln für die Kommunikation mit dem jeweils anderen Netzwerk. Diese Regeln bieten Ihnen die Möglichkeit, den Zugriff der Datenbank auf die Webanwendung zu beschränken.

Das Erstellen eines virtuellen Netzwerks würde den Rahmen dieses Moduls sprengen. Wenn Sie weitere Informationen benötigen, informieren Sie sich über andere Lernmodule zum Thema virtuelle Netzwerke.

### <a name="what-is-a-firewall"></a>Was ist eine Firewall?

Die Firewall ist ein Dienst, der den Zugriff auf einen Server basierend auf der Ursprungs-IP-Adresse der jeweiligen Anforderung gewährt. Sie erstellen Firewallregeln, die IP-Adressbereiche festlegen. Nur Clients mit diesen zugewiesenen IP-Adressen dürfen auf den Server zugreifen. Firewallregeln weisen im Allgemeinen auch spezifische Informationen zu Netzwerkprotokollen und Ports auf. Beispielsweise lauscht ein PostgreSQL-Server standardmäßig an Port 5432 auf TCP-Anforderungen.

### <a name="azure-database-for-postgresql-server-firewall"></a>Azure Database for PostgreSQL-Serverfirewall

Die Azure Database for PostgreSQL-Serverfirewall verhindert jeglichen Zugriff auf Ihren Datenbankserver, bis Sie angeben, welche Computer zugriffsberechtigt sind. Die Firewallkonfiguration ermöglicht die Angabe eines Bereichs von IP-Adressen, die eine Verbindung mit dem Server herstellen dürfen. Der Server verwendet stets die standardmäßigen PostgreSQL-Verbindungsinformationen.

![Eine Abbildung, die zeigt, wie die Azure Database for PostgreSQL-Serverfirewall die IP-Adresse aller eingehenden Anforderungen überprüft. Nur Anforderungen, die aus einem vordefinierten gültigen IP-Adressbereich stammen, werden an die Datenbank weitergeleitet.](../media/7-firewall-diagram.png)

### <a name="azure-database-for-postgresql-server-ssl-connections"></a>SSL-Verbindungen für Azure Database for PostgreSQL-Server

Azure Database for PostgreSQL stellt Verbindungen zwischen Clientanwendungen und dem PostgreSQL-Dienst vorzugsweise über Secure Sockets Layer (SSL) her. Das Erzwingen von SSL-Verbindungen zwischen dem Datenbankserver und Ihren Clientanwendungen trägt zum Schutz vor Man-in-the-Middle- und ähnlichen Angriffen bei, indem die Daten zwischen Server und Client verschlüsselt wird. Die Aktivierung von SSL erfordert den Austausch von Schlüsseln und eine strenge Authentifizierung zwischen Client und Server, damit die Verbindung funktioniert. Details zur Verwendung von SSL werden in dieses Lernmodul nicht behandelt. Wenn Sie weitere Informationen benötigen, informieren Sie sich in anderen Lernmodulen zum Thema SSL.

## <a name="configure-connection-security"></a>Konfigurieren der Verbindungssicherheit

Werfen wir einen Blick auf die Entscheidungen und Schritte bei der Konfiguration einer Firewall für den Azure Database for PostgreSQL-Server. Sie erfahren auch, wie Sie eine Verbindung mit dem Server herstellen, den Sie zuvor erstellt haben.

Melden Sie sich am [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit demselben Konto an, über das Sie die Sandbox aktiviert haben. Navigieren Sie zu der Serverressource, für die Sie eine Firewallregel erstellen möchten.

Wählen Sie anschließend die Option **Verbindungssicherheit** aus, um rechts das Blatt „Verbindungssicherheit“ zu öffnen.

![Screenshot des Azure-Portals mit Abschnitt „Verbindungssicherheit“ auf dem Ressourcenblatt „PostgreSQL-Datenbank“](../media/7-db-security-settings.png)

Auf diesem Bildschirm haben Sie mehrere Möglichkeiten. Sie können:

- Die IP-Adresse, die Sie für den Zugriff auf das Portal verwenden, als Firewalleintrag hinzufügen, indem Sie auf die Schaltfläche **Client-IP-Adresse hinzufügen** klicken.
- Zugriff auf Azure-Dienste erlauben. Standardmäßig haben Azure-Dienste **keinen** Zugriff auf den PostgreSQL-Server.
- Firewallregeln hinzufügen, indem Sie IP-Adressbereiche eingeben.
- SSL-Verbindungen erzwingen. Diese Option zwingt den Client, eine Verbindung mit dem Server mit einem SSL-Zertifikat herzustellen.

Denken Sie immer daran, auf das Symbol **Speichern** über den Eingabefeldern zu klicken, um die aktualisierte Konfiguration zu speichern, nachdem Sie Änderungen vorgenommen haben.

### <a name="allow-access-to-azure-services"></a>Zugriff auf Azure-Dienste erlauben

Um Azure Cloud Shell für den Zugriff oder die Konfiguration Ihres Servers zu verwenden, aktivieren Sie **Zugriff auf Azure-Dienste erlauben**. Mithilfe dieses Schritts wird der Serverkonfiguration eine Firewallregel hinzugefügt, um den Zugriff aus Cloud Shell zu ermöglichen. Diese Regel wird nicht als eine der benutzerdefinierten Regeln angezeigt, die Sie hinzufügen.

Sie müssen auch **SSL-Verbindung erzwingen** deaktivieren. PowerShell kann keine Verbindung mit dem Server herstellen, wenn SSL für Clientverbindungen erforderlich ist.

Beide Optionen führen zu einer Fehlermeldung in der Befehlszeile, wenn sie nicht ordnungsgemäß konfiguriert sind.

Wenn beispielsweise der Zugriff auf Azure-Dienste nicht erlaubt und die Erzwingung von SSL-Verbindungen aktiviert ist, werden Sie eine ähnliche Meldung wie diese sehen, wenn die Firewall den Zugriff blockiert:

```output
psql: FATAL: no pg_hba.conf entry for host "123.45.67.89", user "adminuser", database "postgres", SSL on FATAL:  SSL connection is required. Please specify SSL options and retry.
```

### <a name="create-a-firewall-rule-using-the-portal"></a>Erstellen einer Firewallregel im Portal

Angenommen, Sie möchten eine Firewallregel erstellen, die den Zugriff von jeder IP-Adresse aus ermöglicht.

> [!WARNING]
> Wenn Sie diese Firewallregel erstellen, kann über jede IP-Adresse im Internet versucht werden, eine Verbindung mit Ihrem Server herzustellen. Ohne Benutzername und Kennwort können Clients zwar nicht auf den Server zugreifen. Sie sollten diese Regel aber dennoch nur mit Bedacht aktivieren und sich der Auswirkungen auf die Sicherheit bewusst sein.

Sie erstellen eine neue Firewallregel, indem Sie die folgenden Daten in die markierten Felder eingeben:

- Regelname: `AllowAll`
- Start-IP: `0.0.0.0`
- End-IP: `255.255.255.255`

Um eine Firewallregel zu entfernen, müssen Sie auf die Auslassungspunkte (...) am Ende der Regel klicken, die Sie löschen möchten. Klicken Sie auf die Schaltfläche **Löschen**, um die Regel zu löschen.

Klicken Sie über den Eingabefeldern auf das Symbol **Speichern**, um das Löschen der Regel zu bestätigen.

### <a name="create-a-firewall-rule-using-the-azure-cli"></a>Erstellen einer Firewallregel über die Azure CLI

Sie können die Azure CLI verwenden, um Ihrem Server mithilfe des Befehls `az postgres server firewall-rule create` Firewallregeln hinzuzufügen. Hier ist ein Beispiel, das die oben beschriebene Regel erstellt.

```azurecli
az postgres server firewall-rule create \
  --resource-group <rgn>[Sandbox resource group name]</rgn> \
  --server <server-name> \
  --name AllowAll \
  --start-ip-address 0.0.0.0 \
  --end-ip-address 255.255.255.255
```

Mit dem Befehl `az postgres server firewall-rule delete` heben Sie Firewallregeln für Ihren Server auf. Ein Beispiel:

```azurecli
az postgres server firewall-rule delete \
  --name AllowAll \
  --resource-group <rgn>[Sandbox resource group name]</rgn> \
  --server-name <server-name>
```

## <a name="connecting-to-your-server"></a>Herstellen einer Verbindung mit Ihrem Server

Wie jede moderne Datenbank erfordert auch PostgreSQL eine regelmäßige Serververwaltung, um die bestmögliche Leistung zu erzielen. Sie haben eine Reihe von Optionen, mit Ihrem Azure Database for PostgreSQL-Server eine Verbindung herzustellen und ihn zu verwalten. Zum Herstellen einer Verbindung mit dem Server verwenden Sie `psql`.

### <a name="what-is-psql"></a>Was ist psql?

Das Befehlszeilentool `psql` ist das von PostgreSQL bereitgestellte interaktive Terminal für das Arbeiten mit PostgreSQL-Servern und -Datenbanken. `psql` funktioniert mit Azure Database for PostgreSQL wie mit jeder anderen PostgreSQL-Implementierung und ist in Azure Cloud Shell enthalten. Das Tool `psql` dient zum Verwalten von Datenbanken sowie zum Anwenden von Strukturabfragen auf diese Datenbanken.

`psql` erfordert eine aktive Verbindung mit einem PostgreSQL-Server. Es stehen zahlreiche Befehlszeilenparameter für die Verwendung von `psql` zur Verfügung.

- `--host`: Der Host, mit dem Sie eine Verbindung herstellen möchten.
- `--username`: Der Benutzername/die ID, mit dem bzw. der eine Verbindung hergestellt werden soll.
- `--dbname`: Der Name der Datenbank, mit der eine Verbindung hergestellt werden soll.

> [!TIP]
> Sie stellen normalerweise mit der `postgres`-Verwaltungsdatenbank eine Verbindung her, wenn Sie den Serverzugriff und Datenbankkonfigurationen verwalten.

Hier sehen Sie den vollständigen Befehl:

```bash
psql --host=<server-name>.postgres.database.azure.com
      --username=<admin-user>@<server-name> 
      --dbname=<database>
```

Nach dem Herstellen der Verbindung wird eine Eingabeaufforderung angezeigt, mit der Sie Befehle auf Ihren Server und Ihre Datenbanken anwenden können.

Sie haben nun die Schritte kennengelernt, die Sie zum Konfigurieren von Sicherheitseinstellungen für Azure Database for PostgreSQL ausführen. In der nächsten Einheit konfigurieren Sie Sicherheitseinstellungen für Azure Database for PostgreSQL. Auch die Verbindung mit dem Server stellen Sie über Cloud Shell her.
