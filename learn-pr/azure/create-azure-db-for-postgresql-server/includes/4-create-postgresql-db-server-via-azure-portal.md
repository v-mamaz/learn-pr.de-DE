Das Azure-Portal können Sie verwalten und Skalieren des PostgreSQL-Datenbank-Server. Möchten Sie ein Azure-Datenbank für PostgreSQL-Server zum Speichern von Leistungsdaten Runner zu erstellen. Basierend auf historischen erfasste Datenvolumen, wissen Sie, dass die speicheranforderungen für den Server mit 10 GB festgelegt werden soll. Um Ihre verarbeitungsanforderungen zu unterstützen, müssen Sie 5 Gen-Unterstützung mit 1 virtueller Kern berechnen. Sie wissen auch, dass Sie normalerweise Sicherungen von 25 Tage speichern.

[!include[](../../../includes/azure-sandbox-activate.md)]

Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an. Sie sehen im Azure-Ressourcen erstellen und Verwalten von-Menü auf der linken und das Dashboard, füllen den Rest des Bildschirms.

## <a name="create-an-azure-database-for-postgresql-server"></a>Erstellen einer Azure-Datenbank für PostgreSQL-Server

Nach der Anmeldung, sehen Sie die Standardeinstellung, die Dashboard angezeigt. Sie haben eine Reihe von Optionen, die zum Erstellen eines Azure Database for PostgreSQL-Server zur Verfügung. Im Dashboard ist Folgendes möglich:

- Wählen Sie die **alle Dienste** aus, und suchen Sie nach **, Azure Database for PostgreSQL-Server**. Dieser Bildschirm zeigt alle konfigurierten Server, die bereits in Ihrem Konto enthalten sind. Hier können Sie auswählen **hinzufügen**, dadurch gelangen Sie zum Blatt neuen Server-Erstellung.

oder

- Wählen Sie die **erstellen Sie eine Ressource** Option, die Sie Optionen für Azure Marketplace angezeigt wird. Hier können Sie wählen die **Datenbanken** aus, und wählen Sie **, Azure Database for PostgreSQL**.

### <a name="configure-the-server"></a>Konfigurieren des Servers

Sie sehen nun den PostgreSQL-Server, auf dem Blatt, ähnlich der folgenden Abbildung zu erstellen.

![Screenshot des Azure-Portal mit dem Blatt "erstellen" für eine neue Datenbank für PostgreSQL](../media-draft/4-create-blade.png)

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

> [!NOTE]
> Sie müssen mehr merken oder notieren Sie sich einige Details, wie Sie die PostgreSQL-Server erstellen. Z. B. den Benutzernamen und ein Kennwort zum Zugriff auf den Server. Sie verwenden diese Informationen später eine Verbindung mit Ihrem Server herzustellen.

1. Wählen Sie einen eindeutigen Namen für den Server. Bedenken Sie, dass aus, und klicken Sie dann Name Kleinbuchstaben sein muss und darf Ziffern und Bindestriche enthalten.

1. Wählen Sie ein Abonnement aus. Überprüfen Sie unbedingt, dass dieses Feld auf das Abonnement festgelegt ist, die Sie verwenden möchten.

1. Sie haben jetzt die Option zum Erstellen oder wiederverwenden einer vorhandenen Ressourcengruppe. Wählen Sie **vorhandene** , und wählen Sie <rgn>[Ressourcengruppennamen Sandkasten]</rgn> aus der Dropdownliste aus. Sie verwenden diese Gruppe für den Rest dieses Moduls.

1. Wählen Sie die Quelle für den neuen Server. Für diese laborumgebung, behalten Sie die Option festgelegt wird, um _leere_. Denken Sie daran, dass Sie die Option zum ändern können _Sichern_ , wenn Sie eine vorhandene serversicherung wiederherstellen möchten.

1. Wählen Sie einen Benutzernamen ein, der als eine administratoranmeldung für den neuen Server zu verwenden. Denken Sie daran, dass der Anmeldename des Serveradministrators Azure_superuser, Azure_pg_admin, Admin, Administrator, Root, Guest oder öffentlichen werden kann. Es kann nicht mit Pg_ gestartet. Denken Sie daran, oder notieren Sie den Namen für die zukünftige Verwendung.

1. Wählen Sie ein Kennwort für die Verwendung mit den oben genannten Anmeldename des Administrators ein. Denken Sie daran, =, dass das Kennwort Zeichen aus drei der folgenden Kategorien enthalten muss:
   - Englische Großbuchstaben
   - Englische Kleinbuchstaben
   - Zahlen (0 bis 9)
   - Nicht-alphanumerische Zeichen (!, $, #, % usw.)

   Denken Sie daran, oder notieren Sie sich das Kennwort für die zukünftige Verwendung.

1. Das Kennwort, um zu überprüfen, ob Ihr Kennwort erneut ein.

1. Wählen Sie einen Speicherort für Ihren Server aus. Sie sollten einen Speicherort, der Ihnen am nächsten gelegene auswählen.

1. Sie müssen nun die Version des Servers auswählen. Wählen Sie die neueste Version des PostgreSQL.

1. Wählen Sie als der zweite zum letzten Schritt der **Tarif** Option.

    Denken Sie daran, dass Sie müssen zum Konfigurieren des Servers mit bestimmten Speicher und compute-Optionen:

    - 10 GB an Speicherplatz
    - Berechnen der Generation 5-Unterstützung
    - Aufbewahrungszeitraum von 25 Tagen

    Klicken Sie auf **Tarif** um den Zugriff auf das Blatt mit Tarifen, und nehmen Sie die folgenden Änderungen:

    - Wählen Sie die **grundlegende** Registerkarte.
    - Wählen Sie die **Gen 5 Berechnung Generation** Option.
    - Wählen Sie 1 virtueller Kern aus der **vCore** Schieberegler. Beachten Sie die Auswirkungen der Änderungen in den Schieberegler auf die **Preisübersicht**.
    - Wählen Sie 10 GB aus dem **Storage** Schieberegler. Wenn Sie genau 10 GB gleitend Probleme auftreten, können die linke und Rechte Pfeiltasten auf der Tastatur Sie auf um einen genauen Wert zu erhalten.
    - Wählen Sie 25 Tage ab dem **Aufbewahrungszeit für Sicherung** Schieberegler.

        ![Screenshot des Azure-Portal mit der Tarif für eine neue Datenbank für PostgreSQL-Datenbank](../media-draft/4-azure-db-pricing-tier.png)

    - Klicken Sie auf **OK** , nachdem Sie mit der Auswahl committen Ihre Auswahl, und schließen die tarifoptionen zufrieden sind.

1. Noch ist nun überprüfen die Werte, die Sie eingegeben haben, und klicken Sie auf **erstellen**. Erstellung kann einige Minuten dauern. Sie können das Symbol "Benachrichtigungen" (eine Glocke) am oberen Bildschirmrand Azure Portal zur fortschrittsüberwachung auswählen.

Sie haben jetzt einen PostgreSQL-Server zur Verfügung. In der nächsten Einheit sehen Sie, wie Sie den gleichen Server mithilfe der Azure-Befehlszeilenschnittstelle erstellen.
