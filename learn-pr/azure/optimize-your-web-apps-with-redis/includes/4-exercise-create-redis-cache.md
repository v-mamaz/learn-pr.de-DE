Erstellen wir jetzt eine Azure Redis Cache-Instanz zum Speichern und Zurückgeben häufig verwendeter Werte.

<!-- TODO: do we need to activate the sandbox here? -->

## <a name="create-a-redis-cache-in-azure"></a>Erstellen einer Redis Cache-Instanz in Azure

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

1. Klicken Sie dann auf **Ressource erstellen**, **Datenbanken** und **Redis Cache**.

    Der folgende Screenshot zeigt den Redis Cache-Standort innerhalb der verschiedenen Optionen für Datenbankressourcen im Azure-Portal.

    ![Screenshot mit den Datenbankoptionen im Azure-Portal, mit hervorgehobenen Optionen „Ressource erstellen“, „Datenbank“ und „Redis Cache“](../media/4-create-a-cache-1.png)

### <a name="identify-the-location-for-the-cache"></a>Ermitteln des Standorts für den Cache

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="configure-your-cache"></a>Konfigurieren Ihres Caches

Legen Sie die folgenden Einstellungen für den Cache fest.

1. **DNS-Name**: Erstellen Sie einen global eindeutigen Namen, z.B. **ContosoSportsApp1028**.

1. **Abonnement**: Wählen Sie das Azure Sandbox-Abonnement aus.

1. **Ressourcengruppe**: Wählen Sie <rgn>[Name der Sandbox-Ressourcengruppe]</rgn> als Ressourcengruppe aus.

1. **Standort**: Normalerweise würden Sie einen Standort in der Nähe Ihres Kunden auswählen, in diesem Fall „East Coast“. Für Azure Sandbox können jedoch nur bestimmte Regionen für Ressourcen ausgewählt werden, wie oben angegeben. Wählen Sie einen dieser Standorte aus.

1. **Tarif**: Wählen Sie **Basic C0** aus. Dies ist der niedrigste Tarif, der verwendet werden kann. Für Produktions-Apps werden wahrscheinlich größere Datenmengen und einige der Premium-Features benötigt, z.B. das Clustering. Hierfür wäre die Auswahl eines höheren Tarifs erforderlich.

1. Klicken Sie auf **Erstellen**.

    Der folgende Screenshot zeigt eine repräsentative Konfiguration, die zum Erstellen einer neuen Redis Cache-Ressource verwendet wird. Beachten Sie, dass Ihre Konfiguration aufgrund von Azure Sandbox leicht abweicht.

    ![Screenshot mit dem Azure-Portal-Blatt beim Erstellen einer neuen Redis Cache-Ressource mit DNS-Name, Abonnement, neuer Ressourcengruppe, Speicherort und Tarif der Beispielkonfiguration](../media/4-create-a-cache-2.png)

> [!IMPORTANT]
> Warten Sie, bis der Cache bereitgestellt wurde. Dieser Vorgang kann eine Weile dauern.

## <a name="retrieve-the-access-keys-and-host-name"></a>Abrufen der Zugriffsschlüssel und des Hostnamens

1. Navigieren Sie im Azure-Portal zu Ihrer neuen Redis Cache-Instanz, und wählen Sie **Einstellungen** > **Zugriffsschlüssel** aus. 

1. Kopieren Sie die **Primäre Verbindungszeichenfolge (StackExchange.Redis)** an einen sicheren Ort. Sie benötigen sie für die nächste Übung.

    Dieser Schlüssel enthält Ihren Primärschlüssel und Hostnamen in einer vollständigen Verbindungszeichenfolge für die Verwendung in Ihren Anwendungseinstellungen für das **StackExchange.Redis**-Paket, das wir verwenden.

Als Nächstes lernen Sie einige der Befehle zum Abfragen des Caches kennen.