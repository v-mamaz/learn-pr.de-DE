Ihr Transportunternehmen möchte sich von anderen Unternehmen abheben, jedoch ohne umfangreiche Investitionen. Sie müssen die Datenbank optimal einrichten, um den besten Service bereitzustellen und dabei die Kosten unter Kontrolle zu halten.

Hier lernen Sie Folgendes:

- Welche Aspekte Sie beim Erstellen einer Azure SQL-Datenbank berücksichtigen müssen, einschließlich:
  - Wie ein logischer Server als administrativer Container für Ihre Datenbanken fungiert.
  - Die Unterschiede zwischen Kaufmodellen.
  - Wie Pools für elastische Datenbanken Ihnen ermöglichen, die Verarbeitungsleistung zwischen Datenbanken zu verteilen.
  - Wie Sortierungsregeln sich auf das Vergleichen und Sortieren von Daten auswirken.
- Wie Azure SQL-Datenbank im Portal aufgerufen wird.
- Wie Firewallregeln hinzugefügt werden, damit nur vertrauenswürdige Quellen auf Ihre Datenbank zugreifen können.

Wir werfen kurz einen Blick auf einige Dinge, die Sie bei der Erstellung einer Instanz von Azure SQL-Datenbank berücksichtigen müssen.

## <a name="one-server-many-databases"></a>Ein Server, viele Datenbanken

Wenn Sie Ihre erste Azure SQL-Datenbank erstellen, erstellen Sie auch einen _logischen Azure SQL-Server_. Stellen Sie sich einen logischen Server als administrativen Container für Ihre Datenbanken vor. Sie können Anmeldungen, Firewallregeln und Sicherheitsrichtlinien über den logischen Server steuern. Sie können diese Richtlinien auch für jede Datenbank auf dem logischen Server überschreiben.

Im Moment benötigen Sie nur eine einzige Datenbank. Mit einem logischen Server können Sie jedoch später weitere Datenbanken hinzufügen und die Leistung aller Ihrer Datenbanken optimieren.

## <a name="choose-performance-dtus-versus-vcores"></a>Wählen Sie die Leistung: DTUs oder V-Kerne

Azure SQL-Datenbank bietet zwei Kaufmodelle: DTU und V-Kern.

### <a name="what-are-dtus"></a>Was sind DTUs?

DTU steht für Database Transaction Unit (Datenbanktransaktionseinheit) und ist ein kombiniertes Maß aus Compute-, Speicher- und E/A-Ressourcen. Stellen Sie sich das DTU-Modell als einfache, vorkonfigurierte Kaufoption vor.

Die Idee der eDTUs, elastischer Datenbanktransaktionseinheiten, basiert darauf, dass Ihr logischer Server mehrere Datenbanken enthalten kann. Mit dieser Option können Sie einen Preis auswählen, aber zulassen, dass jede Datenbank im Pool abhängig von der aktuellen Auslastung weniger oder mehr Ressourcen nutzen kann.

### <a name="what-are-vcores"></a>Was sind V-Kerne?

V-Kerne erlauben Ihnen größere Kontrolle darüber, welche Compute- und Speicherressourcen Sie erstellen und bezahlen.

Während das DTU-Modell feste Kombinationen aus Compute-, Speicher- und E/A-Ressourcen bietet, ermöglicht das V-Kern-Modell Ihnen die unabhängige Konfiguration von Ressourcen. Mit dem V-Kern-Modell können Sie z.B. Speicherkapazität erhöhen, jedoch die vorhandene Menge an Computeleistung und E/A-Durchsatz beibehalten.

Ihr Transport- und Logistikprototyp benötigt nur eine einzige Azure SQL-Datenbank-Instanz. Sie entscheiden sich für die DTU-Option, da sie eine gute Balance zwischen Compute-, Speicher- und E/A-Leistung bietet und für den Anfang kostengünstiger ist.

## <a name="what-are-sql-elastic-pools"></a>Was sind Pools für elastische SQL-Datenbanken?

Wenn Sie Ihre Azure SQL-Datenbank erstellen, können Sie einen _Pool für elastische SQL-Datenbanken_ erstellen.

Pools für elastische SQL-Datenbanken stehen mit eDTUs in Zusammenhang. Sie ermöglichen Ihnen, einen Satz von Compute- und Speicherressourcen zu kaufen, die von allen Datenbanken im Pool gemeinsam verwendet werden. Jede Datenbank kann innerhalb der von Ihnen festgelegten Grenzen die Ressourcen nutzen, die sie abhängig von der aktuellen Last benötigt.

Für Ihren Prototyp benötigen Sie keinen Pool für elastische SQL-Datenbanken, da Sie nur eine einzige SQL-Datenbank benötigen.

## <a name="what-is-collation"></a>Was ist eine Sortierung?

Sortierung bezieht sich auf die Regeln zum Sortieren und Vergleichen von Daten. Sortierung vereinfacht das Definieren von Sortierregeln, wenn Groß-/Kleinschreibung, Akzente und andere Merkmale der Sprache wichtig sind.

Nun betrachten wir, was die Standardsortierung **SQL_Latin1_General_CP1_CI_AS** bedeutet.

- **Latin1_General** bezieht sich auf die Familie der westeuropäischen Sprachen.
- **CP1** bezieht sich auf Codepage 1252, eine gängige Zeichencodierung des lateinischen Alphabets.
- **CI** bedeutet, dass die Groß-/Kleinschreibung beim Vergleichen nicht beachtet wird. Beispielsweise werden „HELLO“ und „Hello“ im Vergleich als gleich angesehen.
- **CI** bedeutet, dass Akzente beim Vergleichen beachtet werden. Beispielsweise werden „résumé“ und „resume“ im Vergleich nicht als gleich angesehen.

Da Sie keine bestimmten Anforderungen bezüglich der Art haben, in der Daten sortiert und verglichen werden, wählen Sie die Standardsortierung.

## <a name="create-your-azure-sql-database"></a>Erstellen der Azure SQL-Datenbank

Hier richten Sie Ihre Datenbank ein, was das Erstellen des logischen Servers beinhaltet. Sie wählen Einstellungen aus, die Ihre Transportlogistikanwendung unterstützen. In der Praxis würden Sie Einstellungen auswählen, die die Art von App unterstützen, die Sie erstellen.

Im Laufe der Zeit, wenn Sie, die Sie nutzen, benötigen Sie zusätzliche, rechenleistung, halten sich mit den Bedarf, können zwischen dem DTU und dem v-Kern Performance-Modelle passen Sie die Leistungsoptionen oder sogar wechseln.

[!include[](../../../includes/azure-sandbox-activate.md)]

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

1. Klicken Sie im Portal links oben auf **Ressource erstellen**. Wählen Sie **Datenbanken** und dann **SQL-Datenbank** aus.

   ![Screenshot des Azure-Portal mit der Create Blatt einer Ressource mit den ausgewählten Datenbanken-Bereich und die Ressource erstellen, Datenbanken und SQL-Datenbank hervorgehobenen Schaltflächen.](../media-draft/create-db.png)

1. Klicken Sie unter **Server** auf **Erforderliche Einstellungen konfigurieren**, füllen Sie das Formular aus, und klicken Sie dann auf **Auswählen**. Hier finden Sie weitere Informationen zum Ausfüllen des Formulars:

    | Einstellung      | Wert |
    | ------------ | ----- |
    | **Servername** | Ein global eindeutiger [Servername](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
    | **Serveradministratoranmeldung** | Ein [Datenbankbezeichner](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers), der als Ihr primärer Administrator-Anmeldename dient. |
    | **Kennwort** | Ein gültiges Kennwort umfasst mindestens acht Zeichen und enthält Zeichen aus drei der folgenden Kategorien: Großbuchstaben, Kleinbuchstaben, Zahlen und nicht alphanumerische Zeichen. |
    | **Standort** | Jeder gültige Standort. |
    > [!IMPORTANT]
    > Notieren Sie Ihren Servernamen, Administrator-Anmeldenamen und Ihr Kennwort zur späteren Verwendung.

1. Klicken Sie auf **Tarif**, um die Dienstebene anzugeben. Wählen Sie die Dienstebene **Basic** aus, und klicken Sie dann auf **Übernehmen**.

1. Verwenden Sie diese Werte, um den Rest des Formulars auszufüllen.

    | Einstellung      | Wert |
    | ------------ | ----- |
    | **Datenbankname** | **Logistik** |
    | **Abonnement** | Ihr Abonnement |
    | **Ressourcengruppe** |  Verwenden Sie die vorhandene Gruppe <rgn>[Sandkasten Resource Group-Name]</rgn> |
    | **Quelle auswählen** | **Leere Datenbank** |
    | **Möchten Sie einen Pool für elastische SQL-Datenbanken verwenden?** | **Jetzt nicht** |
    | **Sortierung** | **SQL_Latin1_General_CP1_CI_AS** |

1. Klicken Sie zum Erstellen der Azure SQL-Datenbank auf **Erstellen**.

1. Klicken Sie in der Symbolleiste auf **Benachrichtigungen**, um den Bereitstellungsprozess zu überwachen.

Wenn der Prozess abgeschlossen ist, klicken Sie auf **An Dashboard anheften**, um Ihren Datenbankserver an das Dashboard anzuheften, sodass Sie später bei Bedarf schnellen Zugriff haben.

   ![Screenshot des Azure-Portal mit dem Menü "Benachrichtigungen", mit der Pin auf die Schaltfläche "Dashboard" über eine aktuelle Bereitstellung Erfolgsmeldung hervorgehoben.](../media-draft/notifications-complete.png)

## <a name="set-the-server-firewall"></a>Festlegen der Serverfirewall

Ihre Azure SQL-Datenbank ist jetzt eingerichtet und in Betrieb. Es gibt viele weitere Optionen zum Konfigurieren, Sichern, Überwachen und zur Problembehandlung für Ihre neue Datenbank.

Sie können auch angeben, welche Systeme über die Firewall auf Ihre Datenbank zugreifen können. Zunächst verhindert die Firewall jeglichen Zugriff auf Ihren Datenbankserver von außerhalb von Azure.

Für den Prototypen müssen Sie nur von Ihrem Laptop aus auf die Datenbank zugreifen. Später können Sie zusätzliche Systeme wie Ihre mobile App auf die Whitelist setzen.

Wir ermöglichen nun Ihrem Entwicklungscomputer, über die Firewall auf die Datenbank zuzugreifen.

1. Wechseln Sie zum Übersichtsblatt der Logistics-Datenbank. Wenn Sie die Datenbank zuvor angeheftet haben, können Sie im Dashboard auf die **Logistics**-Kachel klicken, um dorthin zu gelangen.

1. Klicken Sie auf **Serverfirewall festlegen**.

    ![Screenshot des Azure-Portal mit Blatt "Übersicht" einen SQL-Datenbank mit der Set Server Firewall-Schaltfläche hervorgehoben.](../media-draft/set-server-firewall.png)

1. Klicken Sie auf **Client-IP hinzufügen** und dann auf **Speichern**.

    ![Screenshot des Azure-Portal mit einer SQL-Datenbank-Blatt "Einstellungen" mit hervorgehobener Schaltfläche der hinzufügen-Client-IP-Firewall.](../media-draft/add-client-ip.png)

Im nächsten Teil finden Sie einige praktische Übungen mit der neuen Datenbank und Azure Cloud Shell. Sie werden eine Verbindung mit der Datenbank herstellen, eine Tabelle erstellen, einige Beispieldaten hinzufügen und ein paar SQL-Anweisungen ausführen.