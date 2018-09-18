Im Azure-Portal können Sie PostgreSQL-Datenbankserver verwalten und skalieren. Sie treffen die Entscheidung, einen Azure Database for PostgreSQL-Server zu erstellen, um Daten zur Leistung der Aufgabenausführung zu speichern. Aufgrund des Verlaufs der Erfassung von Datenvolumes wissen Sie, dass für Ihren Serverspeicher mindestens 10 GB benötigt werden. Für Ihre Verarbeitungsanforderungen ist die Unterstützung von Compute Gen 5 mit einem V-Kern erforderlich. Außerdem verfügen Sie über die Information, dass Sicherungen bei Ihnen normalerweise 25 Tage lang gespeichert werden.

> [!TIP]
> Alle Übungen in Microsoft Learn sind kostenlos. Wenn Sie jedoch eigenständig weitere Funktionen nutzen möchten, benötigen Sie ein Azure-Abonnement. Wenn Sie noch nicht über ein Abonnement verfügen, können Sie in wenigen Minuten ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen.

Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an. Das Menü zum Erstellen und Verwalten von Azure-Ressourcen wird links angezeigt. Den verbleibenden Bildschirmbereich nimmt das Dashboard ein.

## <a name="create-an-azure-database-for-postgresql-server"></a>Erstellen eines Azure Database for PostgreSQL-Servers

Nach dem Anmelden wird das Standarddashboard angezeigt. Sie haben zwei Möglichkeiten, um einen Azure Database for PostgreSQL-Server zu erstellen. Im Dashboard können Sie wie folgt vorgehen:

- Wählen Sie die Option **Alle Dienste**, und suchen Sie dann nach der Option **Azure Database for PostgreSQL-Server**. Auf diesem Bildschirm werden alle konfigurierten Server angezeigt, die sich bereits unter Ihrem Konto befinden. Wählen Sie **Hinzufügen**, um zum Blatt für die Erstellung des neuen Servers zu gelangen.

oder

- Wählen Sie die Option **Ressource erstellen**, um die Optionen für Azure Marketplace-Ressourcen anzuzeigen. Wählen Sie die Option „Datenbanken“ und dann **Azure Database for PostgreSQL**.

### <a name="configure-the-server"></a>Konfigurieren des Servers

Das Blatt für die Erstellung des PostgreSQL-Servers wird angezeigt (etwa wie in der folgenden Abbildung).

![Blatt für die Erstellung des PostgreSQL-Servers im Azure-Portal](../media-draft/4-create-blade.png)

> [!NOTE]
> Beim Erstellen des PostgreSQL-Servers müssen Sie sich einige Details merken bzw. notieren. Dies können beispielsweise der Benutzername und das Kennwort für den Zugriff auf den Server sein. Sie verwenden diese Informationen später, um eine Verbindung mit Ihrem Server herzustellen.

1. Wählen Sie einen eindeutigen Namen für den Server aus. Beachten Sie, dass der Name nur aus Kleinbuchstaben, Zahlen und Bindestrichen bestehen darf.

1. Wählen Sie ein Abonnement aus. Vergewissern Sie sich, dass dieses Feld auf das gewünschte Abonnement festgelegt ist.

1. Sie haben jetzt die Möglichkeit, eine vorhandene Ressource zu erstellen oder wiederzuverwenden. Wählen Sie zum Erstellen einer neuen Ressource das Optionsfeld **Neu erstellen**, und geben Sie einen Namen für die neue Ressourcengruppe ein. Sie verwenden diese Gruppe für den restlichen Teil dieses Moduls. Geben Sie der Ressource einen aussagekräftigen Namen, um das spätere Löschen zu vereinfachen.

1. Wählen Sie die Quelle Ihres neuen Servers aus. Für diese Übung behalten Sie die Option _Leer_ bei. Beachten Sie, dass Sie die Option in _Sicherung_ ändern können, wenn Sie eine vorhandene Serversicherung wiederherstellen möchten.

1. Wählen Sie einen Anmeldenamen aus, der als Administratoranmeldung für den neuen Server verwendet wird. Der Administratoranmeldename darf nicht „azure_superuser“, „azure_pg_admin“, „admin“, „administrator“, „root“, „guest“ oder „public“ lauten. Er kann auch nicht mit „pg_“ beginnen. Prägen Sie sich den Namen für die spätere Verwendung ein bzw. notieren Sie ihn.

1. Wählen Sie ein Kennwort für den obigen Anmeldenamen für Administratoren. Beachten Sie, dass das Kennwort Zeichen aus drei der folgenden Kategorien enthalten muss: englische Großbuchstaben, englische Kleinbuchstaben, Zahlen (0 - 9) und nicht alphanumerische Zeichen (!, $, #, % usw.). Prägen Sie sich das Kennwort für die spätere Verwendung ein bzw. notieren Sie es.

1. Geben Sie das Kennwort zur Bestätigung erneut ein.

1. Wählen Sie einen Standort für Ihren Server aus. Hierbei ist es ratsam, einen Standort zu wählen, der Ihnen am nächsten liegt.

1. Sie wählen jetzt die Version für Ihren Server aus. Wählen Sie die aktuelle Version von PostgreSQL aus.

1. Wählen Sie als zweitletzten Schritt die Option **Tarif**.

    Beachten Sie, dass Sie Ihren Server mit spezifischen Speicher- und Computeoptionen konfigurieren müssen.

    - 10 GB Datenträgerspeicher
    - Unterstützung für Compute Generation 5
    - Aufbewahrungszeitraum von 25 Tagen

    Klicken Sie auf **Tarif**, um auf das Blatt „Tarif“ zuzugreifen, und nehmen Sie die folgenden Änderungen vor: ![Schaltfläche „Tarif“](../media-draft/4-azure-db-pricing-tier-button.png)

    - Wählen Sie die Registerkarte für die Option **Basic**.
    - Wählen Sie die Option **Gen 5 Computation Generation**.
    - Wählen Sie über den Schieberegler **V-Kern** die Option für „1 V-Kern“. Verfolgen Sie, wie sich die Änderungen über den Schieberegler auf die **Preisübersicht** auswirken.
    - Wählen Sie über den Schieberegler **Speicher** eine Größe von „10 GB“ aus. Falls Sie Probleme beim Einstellen des genauen Werts von 10 GB haben, können Sie auf der Tastatur die NACH-LINKS- und NACH-RECHTS-TASTE verwenden, um den Wert genau einzustellen.
    - Wählen Sie über den Schieberegler **Aufbewahrungszeit für Sicherung** einen Zeitraum von 25 Tagen aus.

    ![Tarif](../media-draft/4-azure-db-pricing-tier.png)
    - Klicken Sie auf **OK**, wenn Sie mit Ihrer Auswahl zufrieden sind, um die ausgewählten Optionen zu übernehmen und die Tarifoptionen zu schließen.

1. Jetzt müssen Sie nur noch die eingegebenen Werte überprüfen und auf **Erstellen** klicken. Die Erstellung kann mehrere Minuten dauern. Sie können oben im Azure-Portal das Symbol für Benachrichtigungen (Glocke) wählen, um den Status zu überwachen.

Für Sie steht jetzt ein PostgreSQL-Server zur Verfügung. In der nächsten Einheit wird beschrieben, wie Sie den gleichen Server mit der Azure-Befehlszeilenschnittstelle erstellen.
