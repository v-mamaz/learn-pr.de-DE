Nehmen wir an, dass Sie derzeit über eine lokale relationale PostgreSQL-Datenbank mithilfe von flexiblen-Datentypen und Unterstützung von Geodaten nutzen. Möchte Ihr Unternehmen ist am erweitern, der erfordert, dass der Datenbank skalieren. Als Alternative zur in zusätzliche Hardware investieren sind Sie damit beauftragt, ein Angebot für eine optimale Cloud-gehosteten Datenbank zu suchen. Sie haben sich entschieden, einer Azure-Datenbank für PostgreSQL-Server.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>Was ist ein Azure-Datenbank für PostgreSQL-Server?

Die PostgreSQL-Server ist ein zentraler Verwaltungspunkt für eine oder mehrere Datenbanken. Der PostgreSQL-Dienst in Azure ist eine verwaltete Ressource, die bietet leistungsgarantien und stellt Zugriff sowie Funktionen auf Serverebene.

Ein **, Azure Database for PostgreSQL** Server ist das übergeordnete Element _Ressource_ für eine Datenbank. Ein _Ressource_ ist ein verwaltbares Element, das über Azure verfügbar ist. Diese Ressource zu erstellen, können Sie die Server-Instanz zu konfigurieren.

### <a name="what-is-an-azure-database-for-postgresql-server-resource"></a>Was ist eine Azure Database for PostgreSQL-Server-Ressource?

Azure Database for PostgreSQL-Server-Ressource ist ein Container mit hoher Lebensdauer Auswirkungen auf die für Ihren Server und Datenbanken. Wenn die Server-Ressource gelöscht wird, werden alle Datenbanken ebenfalls gelöscht. Bedenken Sie, dass alle Ressourcen, die zum übergeordneten Element gehören in der gleichen Region gehostet werden.

Der Server-Ressourcenname wird verwendet, um den Servernamen für den Endpunkt zu definieren. Wenn der Ressourcenname ist z. B. **Mypgsqlserver**, und klicken Sie dann den Namen des Servers wird **mypgsqlserver.postgres.database.azure.com**.

Die Server-Ressource bietet außerdem die __Verbindungsbereich__ für Management-Richtlinien, die auf die Datenbank angewendet. Zum Beispiel: Login, Firewall, Benutzer, Rollen und Konfiguration.

Genau wie die Open-Source-Version von PostgreSQL wird der Server ist in mehreren Versionen verfügbar und lässt die Installation von Erweiterungen. Sie müssen die, die zu installierende Serverversion auswählen.

> [!NOTE]
> Erweiterungen können mehrere SQL-Objekte zusammen bündeln, in einem einzigen Paket, das geladen oder mit einem einzigen Befehl entfernt werden kann. Ein Beispiel für eine Erweiterung ist `chkpass`, die stellt einen Datentyp für automatisch verschlüsselte Kennwörter bereit.

## <a name="pricing-tiers"></a>Tarife

Azure Database for PostgreSQL bietet, dass Sie mit der Option zum Auswählen aus drei Tarifen, die basierend auf Parametern wie computeleistung und Speicher.

### <a name="basic-tier"></a>Basic-Tarif

Die **grundlegende** Tarif eignet sich ideal für Workloads, die wenig COMPUTE- und e/a-Leistung erfordern. In diesem Tarif haben Sie Zugriff auf die folgende Hardware:

- Compute Gen 4 CPUs auf Intel E5-2673 v3 (Haswell) 2,4-GHz-Prozessoren verfügbar als 1 oder 2 v-Kern-Konfiguration basieren
- Berechnen Sie, dass die CPUs der Generation 5 auf Intel E5-2673 v4 (Broadwell) 2,3-GHz-Prozessoren verfügbar sind als 1 oder 2 v-Kern-Konfiguration basieren
- Speicher von bis zu 1 TB
- Lokal redundant-backup

Sie werden eine bestimmten Preis-Tier-Einstellung verwenden, um Unterstützung für ein bestimmtes Szenario zu veranschaulichen, wenn Sie einen Beispiel-Server später erstellen. Bedenken Sie, dass für Produktionsserver sollten Sie einen Tarif entsprechend Ihrer Umgebung auswählen.

### <a name="general-purpose-tier"></a>Allgemeiner Zweck-Ebene

Die **allgemeiner** Tarif eignet sich ideal für die meisten geschäftlichen Workloads, die ausgeglichene COMPUTE- und Speicherkapazitäten mit skalierbarem e/a-Durchsatz erfordern. In diesem Tarif haben Sie Zugriff auf die folgende Hardware:

- Compute Gen 4 CPUs basieren auf Intel E5-2673 v3 (Haswell) 2,4-GHz-Prozessoren verfügbar in 2, 4, 8, 18, 32 v-Kern-Konfigurationen
- Berechnen Sie die CPUs der Generation 5 basieren auf Intel E5-2673 v4 (Broadwell) 2,3-GHz-Prozessoren verfügbar sind, in 2, 4, 8, 18, 32 v-Kern-Konfigurationen
- Speicher von bis zu 4 TB
- Lokal redundant-backup
- Geografisch redundanten Sicherung

### <a name="memory-optimized-tier"></a>Speicherstufe-optimiert

Die **Speicheroptimierte** Tarif eignet sich ideal für Hochleistungs datenbankworkloads, die in-Memory-Leistung für schnellere transaktionsverarbeitung und Erhöhung der Parallelität erfordern. In diesem Tarif haben Sie Zugriff auf die folgende Hardware:

- Berechnen Sie die CPUs der Generation 5 basieren auf Intel E5-2673 v4 (Broadwell) 2,3-GHz-Prozessoren verfügbar sind, in 2, 4, 8, 16 v-Kern-Konfigurationen
- Speicher von bis zu 4 TB
- Lokal redundant-backup
- Geografisch redundanten Sicherung

## <a name="steps-to-create-an-azure-database-for-postgresql-server"></a>Schritte zum Erstellen eines Azure Database for PostgreSQL-server

Sie erstellen in der Regel über einen Azure Database for PostgreSQL-Server mithilfe von Azure-Portal. Wir sehen uns die Schritte, die Sie ausführen müssen.

Zunächst müssen Sie zum Azure-Portal anmelden, und klicken Sie dann werde **erstellen Sie eine Ressource**.

Wählen Sie **Datenbanken** und **, Azure Database for PostgreSQL**. Können Sie auch die **Suche** Funktionalität dieser Kategorie zu finden.

Zeigt das Portal eine PostgreSQL-Server-Konfigurationsbildschirm, so genannte ein Blatt, und Sie Ihre Auswahl treffen.

![Screenshot des Azure-Portal mit dem Blatt "erstellen" für eine neue Datenbank für PostgreSQL](../media-draft/4-create-blade.png)

Sie müssen, geben Sie einen Wert für alle Elemente auf dem Blatt, lassen Sie uns einen Blick auf die einzelnen.

### <a name="server-name"></a>Servername

Weiter oben wurde erwähnt, dass Sie eine Server-Ressource erstellen. Der Servername ist das Element, das diese Ressource angibt. Daher müssen Sie einen eindeutigen Namen für den Server auswählen. Den Namen des Servers muss nur Kleinbuchstaben und haben kann, Zahlen und Bindestriche enthalten.

Angenommen, Sie den Namen des Servers möchten _Nachverfolgen von Adventure Works_. Sie würden dann festlegen, um den Namen als `adventure-works-tracking`. Wenn Sie versuchen, einen Server mit einem Namen zu erstellen, die bereits vorhanden ist, erhalten Sie entsprechende Fehler.

### <a name="subscription"></a>Abonnement

Das Feld "Abonnement" wird für die Abrechnung verwendet. Sie müssen ein bestimmtes Abonnement auswählen, für den Fall, dass Sie über mehrere Abonnements zur Verfügung haben.

### <a name="resource-group"></a>Ressourcengruppe

Sie verwenden eine Ressourcengruppe aus, um alle Ressourcen im Zusammenhang mit dem Server verwalten. Sie können eine neue Ressourcengruppe erstellen oder wiederverwenden eine vorhandenen Ressourcengruppe.

### <a name="source"></a>Quelle

Können Sie einen Server erstellen entweder von Grund auf neu durch Auswählen der _leere_ Standardoption oder aus einer vorhandenen Sicherung. Die **Backup** Option erhalten Sie die Gelegenheit zum Wiederherstellen einer geosicherung einer vorhandenen Azure-Datenbank für PostgreSQL-Server.

### <a name="server-admin-login-name"></a>Anmeldename des Serveradministrators

Sie erstellen den Server Admin-Benutzer. Wählen Sie einen Benutzernamen ein, der als eine administratoranmeldung für den neuen Server zu verwenden. Der administratoranmeldename darf nicht Azure_superuser, Azure_pg_admin, Admin, Administrator, Root, Guest oder öffentlichen sein. Es kann nicht mit Pg_ gestartet. Denken Sie daran, oder notieren Sie sich diesen Namen für die zukünftige Verwendung.

### <a name="password"></a>Password

Sie wählen Sie ein Kennwort mit den oben genannten Administrator-Anmeldenamen verwenden. Ihr Kennwort muss Zeichen aus drei der folgenden Kategorien enthalten:
- Englische Großbuchstaben
- Englische Kleinbuchstaben
- Zahlen (0 bis 9)
- Nicht-alphanumerische Zeichen (!, $, #, % usw.)

Denken Sie daran, oder notieren Sie sich dieses Kennwort für die zukünftige Verwendung.

### <a name="confirm-password"></a>Kennwort bestätigen

Geben Sie das Kennwort zur Bestätigung erneut ein.

### <a name="location"></a>Standort

Option "Standort" können Sie angeben, in dem der Server physisch erstellt wurde. Wählen Sie den geografischen Standort, der Ihnen am nächsten gelegene. In einem realen Szenario sollte der Speicherort der Speicherort, der die Mehrheit der Benutzer am nächsten liegt.

### <a name="version"></a>Version

Sie können die Version des PostgreSQL mit angeben. Microsoft zielt darauf ab, um die aktuelle Version und die beiden Vorgängerversionen von PostgreSQL zu unterstützen. Wählen Sie dazu eine Version, die Ihrer produktionsumgebung entspricht.

> [!NOTE]
> Weitere Informationen finden Sie unter den folgenden Quellen:
> - [Unterstützte PostgreSQL-Datenbankversionen](https://docs.microsoft.com/azure/postgresql/concepts-supported-versions)
> - [Versionsrichtlinien](https://www.postgresql.org/support/versioning/)

### <a name="pricing-tier"></a>Tarif

Sie müssen einen Tarif auswählen, der Ihr Server Workloads unterstützt. Denken Sie daran, dass Sie drei Tarife zur Auswahl haben. Wie wir gesehen haben, kann jede diese Stufen Sie die COMPUTE- und Speicheroptionen zu konfigurieren. Hier ist ein Beispiel mit der Basic-Tarif ausgewählt, ein Compute Gen 5 und einen Aufbewahrungszeitraum von 25 Tagen.

![Screenshot des Azure-Portal mit der Tarif für eine neue Datenbank für PostgreSQL-Datenbank](../media-draft/4-azure-db-pricing-tier.png)

Jetzt nur noch ist, überprüfen die Werte, die Sie eingegeben haben, stellen Sie möglicherweise zur späteren Verwendung benötigen, und klicken Sie auf Hinweise **erstellen** um den Server zu erstellen.

Bereitstellen des Servers dauert einige Minuten. Sie erhalten eine Benachrichtigung, wenn die Bereitstellung abgeschlossen ist. Von der Benachrichtigung können Sie mit dem neu erstellten Server navigieren.

Sie haben nun die Schritte gesehen, die Sie zum Erstellen eines Azure Database for PostgreSQL-Server ausführen. In der nächsten Einheit müssen Sie die Möglichkeit, Ihre eigenen, Azure Database for PostgreSQL-Server zu erstellen.
