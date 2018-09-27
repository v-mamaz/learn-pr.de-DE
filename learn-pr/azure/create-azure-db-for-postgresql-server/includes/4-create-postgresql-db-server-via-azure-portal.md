Im Azure-Portal können Sie PostgreSQL-Datenbankserver verwalten und skalieren. Sie treffen die Entscheidung, einen Azure Database for PostgreSQL-Server zu erstellen, um Daten zur Leistung der Aufgabenausführung zu speichern. Aufgrund des Verlaufs der Erfassung von Datenvolumes wissen Sie, dass für Ihren Serverspeicher mindestens 10 GB benötigt werden. Für Ihre Verarbeitungsanforderungen ist die Unterstützung von Compute Gen 5 mit einem V-Kern erforderlich. Außerdem verfügen Sie über die Information, dass Sicherungen bei Ihnen normalerweise 25 Tage lang gespeichert werden.

[!include[](../../../includes/azure-sandbox-activate.md)]

Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.

Das Menü zum Erstellen und Verwalten von Azure-Ressourcen wird links angezeigt. Den verbleibenden Bildschirmbereich nimmt das Dashboard ein.

## <a name="create-an-azure-database-for-postgresql-server"></a>Erstellen eines Azure Database for PostgreSQL-Servers

Nachdem Sie sich angemeldet haben, wird das Standarddashboard angezeigt. Sie haben zwei Möglichkeiten, um einen Azure Database for PostgreSQL-Server zu erstellen. Im Dashboard können Sie wie folgt vorgehen:

- Wählen Sie die Option **Alle Dienste** aus, und suchen Sie dann nach **Azure Database for PostgreSQL-Server**. Auf diesem Bildschirm werden alle konfigurierten Server angezeigt, die sich bereits unter Ihrem Konto befinden. Wählen Sie **Hinzufügen**, um zum Blatt für die Erstellung des neuen Servers zu gelangen.

**oder**

- Wählen Sie die Option **Ressource erstellen**, um die Optionen für Azure Marketplace-Ressourcen anzuzeigen. Wählen Sie die Option **Datenbanken** und dann **Azure Database for PostgreSQL** aus.

### <a name="configure-the-server"></a>Konfigurieren des Servers

Das Blatt für die Erstellung des PostgreSQL-Servers wird angezeigt (etwa wie in der folgenden Abbildung).

![Screenshot des Azure-Portals mit einem Erstellungsblatt für eine neue PostgreSQL-Datenbank.](../media/4-create-blade.png)

> [!NOTE]
> Beim Erstellen des PostgreSQL-Servers müssen Sie sich einige Details merken. Dies können beispielsweise der Benutzername und das Kennwort für den Zugriff auf den Server sein. Sie verwenden diese Informationen später, um eine Verbindung mit Ihrem Server herzustellen.

1. Wählen Sie einen eindeutigen Namen für den Server aus. Beachten Sie, dass der Name nur aus Kleinbuchstaben, Zahlen und Bindestrichen bestehen darf.

1. Wählen Sie ein Abonnement aus. Vergewissern Sie sich, dass dieses Feld auf das gewünschte Abonnement festgelegt ist.

1. Sie haben jetzt die Möglichkeit, eine vorhandene Ressourcengruppe zu erstellen oder wiederzuverwenden. Wählen Sie **Vorhandene verwenden** und anschließend <rgn>[Name der Sandboxressourcengruppe]</rgn> in der Dropdownliste aus. Sie verwenden diese Gruppe für den restlichen Teil dieses Moduls.

1. Wählen Sie die Quelle Ihres neuen Servers aus. Für diese Übung lassen Sie die Option _Leer_. Beachten Sie, dass Sie die Option in _Sicherung_ ändern können, wenn Sie eine vorhandene Serversicherung wiederherstellen möchten.

1. Wählen Sie einen Anmeldenamen aus, der als Administratoranmeldung für den neuen Server verwendet wird. Der Administratoranmeldename darf nicht „azure_superuser“, „azure_pg_admin“, „admin“, „administrator“, „root“, „guest“ oder „public“ lauten. Er kann auch nicht mit „pg_“ beginnen. Prägen Sie sich den Namen für die spätere Verwendung ein bzw. notieren Sie ihn.

1. Wählen Sie ein Kennwort für den obigen Anmeldenamen für Administratoren aus. Denken Sie daran, dass das Kennwort Zeichen aus drei der folgenden Kategorien enthalten muss:
   - Englische Großbuchstaben
   - Englische Kleinbuchstaben
   - Ziffern (0 bis 9)
   - Nicht alphanumerische Zeichen (!, $, #, % usw.)

1. Geben Sie das Kennwort zur Bestätigung erneut ein.

1. Wählen Sie einen Standort für Ihren Server aus. Hierbei sollten Sie den Standort, der Ihnen am nächsten liegt, in der folgenden Liste auswählen.

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]


1. Jetzt wählen Sie die Version für Ihren Server aus. Wählen Sie die aktuelle Version von PostgreSQL aus.

1. Wählen Sie als zweitletzten Schritt die Option **Tarif**.

    Beachten Sie, dass Sie Ihren Server mit spezifischen Speicher- und Computeoptionen konfigurieren müssen:

    - 10GB Datenträgerspeicher
    - Unterstützung für Compute Generation 5
    - Aufbewahrungszeitraum von 25 Tagen

    Klicken Sie auf **Tarif**, um auf das Blatt „Tarif“ zuzugreifen, und nehmen Sie die folgenden Änderungen vor:

    - Wählen Sie die Registerkarte für die Option **Basic** aus.
    - Wählen Sie die Option **Gen 5 Computation Generation**.
    - Wählen Sie über den Schieberegler **V-Kern** die Option für „1 V-Kern“. Verfolgen Sie, wie sich die Änderungen über den Schieberegler auf die **Preisübersicht** auswirken.
    - Wählen Sie über den Schieberegler **Speicher** eine Größe von „10GB“ aus. Falls Sie Probleme beim Einstellen des genauen Werts von 10GB haben, können Sie auf der Tastatur die NACH-LINKS- und NACH-RECHTS-TASTE verwenden, um den Wert genau einzustellen.
    - Wählen Sie über den Schieberegler **Aufbewahrungszeit für Sicherung** einen Zeitraum von 25 Tagen aus.
    - Behalten Sie die Einstellung **Lokal redundant** der Sicherungsredudanzoptionen bei.

    ![Screenshot des Azure-Portals mit dem Datenbanktarifblatt für eine neue PostgreSQL-Datenbank.](../media/4-azure-db-pricing-tier.png)

1. Beachten Sie die Preisübersicht auf der rechten Seite. Sie bietet eine Kostenaufschlüsselung für den Server zusammen mit einer Schätzung der monatlichen Kosten.

1. Klicken Sie auf **OK**, wenn Sie mit Ihrer Auswahl zufrieden sind, um die ausgewählten Optionen zu übernehmen und die Tarifoptionen zu schließen.

1. Jetzt müssen Sie nur noch die eingegebenen Werte überprüfen und auf **Erstellen** klicken. Die Erstellung kann mehrere Minuten dauern. Sie können oben im Azure-Portal das Symbol für Benachrichtigungen (Glocke) wählen, um den Status zu überwachen.

Für Sie steht jetzt ein PostgreSQL-Server zur Verfügung. In der nächsten Einheit wird beschrieben, wie Sie den gleichen Server mit der Azure-Befehlszeilenschnittstelle erstellen.
