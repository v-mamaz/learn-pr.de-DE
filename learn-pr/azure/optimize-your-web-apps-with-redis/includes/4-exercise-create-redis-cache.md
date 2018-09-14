Erstellen wir eine Azure Redis Cache-Instanz zum Speichern und häufig verwendete Werte zurückgeben.

<!-- TODO: do we need to activate the sandbox here? -->

## <a name="create-a-redis-cache-in-azure"></a>Erstellen eines Redis-Caches in Azure

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

1. Klicken Sie auf **erstellen Sie eine Ressource**, klicken Sie auf **Datenbanken**, und klicken Sie auf **Redis Cache**.

    Der folgende Screenshot zeigt den Redis Cache-Speicherort innerhalb der verschiedenen Datenbankressourcen-Optionen im Azure-Portal.

    ![Screenshot mit den Datenbankoptionen des Azure-Portals, wobei die Optionen „Ressource erstellen“, „Datenbank“ und „Redis Cache“ hervorgehoben sind.](../media/4-create-a-cache-1.png)

### <a name="identify-the-location-for-the-cache"></a>Geben Sie den Speicherort für den cache

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="configure-your-cache"></a>Konfigurieren Ihres Caches

Wenden Sie die folgenden Einstellungen auf den Cache ein.

1. **DNS-Name**: Erstellen Sie einen global eindeutigen Namen, z.B. **ContosoSportsApp1028**.

1. **Abonnement:** wählen Sie das Azure-Sandbox-Abonnement.

1. **Ressourcengruppe:** wählen <rgn>[Ressourcengruppennamen Sandkasten]</rgn> für die Ressourcengruppe aus.

1. **Speicherort:** normalerweise wählen Sie einen Speicherort in der Nähe Ihrer Kunden – in diesem Fall der Ostküste. Der Azure-Sandbox können jedoch nur bestimmte Regionen für Ressourcen, wie oben bereits erwähnt ausgewählt werden. Wählen Sie einen der Orte an.

1. **Tarif**: Wählen Sie **Basic C0** aus. Dies ist die niedrigste Ebene, die Sie verwenden können. Produktions-apps würden wahrscheinlich weitere Daten zu speichern und nutzen einige der Premium-Features wie z. B. Cluster, die eine höhere Ebene Auswahl erforderlich wäre.

1. Klicken Sie auf **Erstellen**.

    Der folgende Screenshot zeigt eine repräsentative Konfiguration, die zum Erstellen einer neuen Redis Cache-Ressource verwendet wird. Beachten Sie, dass Ihnen etwas unterscheidet sich aufgrund der Azure-Sandbox.

    ![Screenshot mit dem Azure-Portal-Blatt beim Erstellen einer neuen Redis Cache-Ressource mit DNS-Name, Abonnement, neuer Ressourcengruppe, Speicherort und Tarif der Beispielkonfiguration.](../media/4-create-a-cache-2.png)

> [!IMPORTANT]
> Warten Sie, bis der Cache bereitgestellt wurde. Dieser Vorgang kann eine Weile dauern.

## <a name="verify-your-data"></a>Überprüfen Ihrer Daten

Können Sie die **Konsole** Feature im Azure-Portal, Befehle an Ihre Redis Cache-Instanz, nachdem es erstellt wurde.

1. Suchen Sie den Redis Cache dazu **alle Ressourcen** in der linken Randleiste und verwenden das Feld "Filter" auf der linken Seite zum Auswählen von Redis Cache-Instanzen. Alternativ können Sie verwenden Sie das Suchfeld oben, und geben Sie den Namen des Caches.

1. Wählen Sie Ihr Redis Cache-Instanz.

1. In der **Übersicht** auf dem Blatt für Ihren Redis Cache wählen **Konsole**. Dadurch wird eine Redis-Konsole geöffnet, Low-Level-Redis-Befehle eingeben können.

1. Typ **Ping**. Stellen Sie sicher, dass der zurückgegebene Wert ist **PINGPONG**.

1. Typ **Set-Test eins**. Stellen Sie sicher, dass der zurückgegebene Wert ist **OK**.

1. Typ **erste Test**. Stellen Sie sicher, dass der zurückgegebene Wert ist **"one"**.

1. Wechseln Sie zurück zu den **Übersicht über die** entweder über die Breadcrumb-Leiste im oberen Bereich aus, oder verwenden Sie die Bildlaufleiste, schieben Sie die Ansicht auf der linken Seite zurück.

## <a name="retrieve-the-access-keys-and-host-name"></a>Abrufen der Zugriffsschlüssel und des Hostnamens

1. Wählen Sie **Einstellungen** > **Zugriffsschlüssel**. 

1. Kopieren der **primäre Verbindungszeichenfolge (StackExchange.Redis)** an einem sicheren Ort auf, Sie benötigen sie für die nächste Übung.

    Dieser Schlüssel enthält den Namen Ihres primären Schlüssels und des Hosts in eine vollständige Verbindungszeichenfolge für die Verwendung in den Einstellungen Ihrer Anwendung für die **"stackexchange.redis"** Paket, die wir verwenden wollen.

Als Nächstes betrachten wir einige der Befehle können mit den Cache abzufragen.