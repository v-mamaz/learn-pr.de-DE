Erstellen wir jetzt eine Azure Redis Cache-Instanz zum Speichern und Zurückgeben häufig verwendeter Werte.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-redis-cache-in-azure"></a>Erstellen einer Redis Cache-Instanz in Azure

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.

1. Klicken Sie dann auf **Ressource erstellen**, **Datenbanken** und **Redis Cache**.

    Der folgende Screenshot zeigt den Redis Cache-Standort innerhalb der verschiedenen Optionen für Datenbankressourcen im Azure-Portal.

    ![Screenshot mit den Datenbankoptionen des Azure-Portals, wobei die Optionen „Ressource erstellen“, „Datenbank“ und „Redis Cache“ hervorgehoben sind.](../media/4-create-a-cache-1.png)

### <a name="configure-your-cache"></a>Konfigurieren Ihres Caches

Legen Sie die folgenden Einstellungen für den Cache fest.

1. **DNS-Name:** Erstellen Sie einen global eindeutigen Namen wie z.B. **ContosoSportsApp[nnn]**, wobei `[nnn]` durch zufällige Zahlen ersetzt wird.

1. **Abonnement:** Wählen Sie das Concierge-Abonnement aus.

1. **Ressourcengruppe:** Wählen Sie <rgn>[Name der Sandbox-Ressourcengruppe]</rgn> als Ressourcengruppe aus.

1. **Standort**: Normalerweise würden Sie einen Standort in der Nähe Ihres Kunden auswählen, in diesem Fall „East Coast“. Für die Azure-Sandbox können jedoch nur bestimmte Regionen für Ressourcen ausgewählt werden. Wählen Sie einen der folgenden Standorte aus.
    
    [!include[](../../../includes/azure-sandbox-regions-note-friendly.md)]
        
5. **Tarif:** Wählen Sie **Basic C0** aus. Dies ist der niedrigste Tarif, der verwendet werden kann. Für Produktions-Apps werden wahrscheinlich größere Datenmengen und einige der Premium-Features benötigt, z.B. das Clustering. Hierfür wäre die Auswahl eines höheren Tarifs erforderlich.

1. Klicken Sie auf **Erstellen**. Azure erstellt die Redis Cache-Instanz und stellt sie Ihnen bereit.

    > [!IMPORTANT]
    > Normalerweise wird die Redis-Cache-Ressource sehr schnell erstellt und im Azure-Portal angezeigt, aber der Cache selbst ist erst nach einigen Minuten verfügbar. Die nächsten Schritte zeigen, wie der Status des Caches überprüft wird.

## <a name="verify-your-data"></a>Überprüfen Ihrer Daten

Über die **Konsole** im Azure-Portal können Sie Befehle für Ihre Redis Cache-Instanz ausführen, nachdem diese erstellt wurde.

1. Suchen Sie Ihren Redis Cache nach Abschluss der Bereitstellung mithilfe des Popups **Benachrichtigung** oder indem Sie auf der linken Randleiste auf **Alle Ressourcen** klicken und über das Filterfeld auf der linken Seite Redis Cache-Instanzen auswählen. Alternativ können Sie auch oben das Suchfeld verwenden und den Namen des Cache eingeben.

1. Wählen Sie Ihre Redis Cache-Instanz aus.

1. Überprüfen Sie den Wert des Felds „Status“. Der Cache ist erst aktiv, wenn der Status „Wird ausgeführt“ lautet. Sie müssen ggf. einige Minuten warten, ehe Sie fortfahren können.

1. Sobald der Cache aktiviert ist, klicken Sie auf der Symbolleiste auf dem Blatt **Übersicht** für Ihre Redis Cache-Instanz auf die Schaltfläche `>_ Console`. Dadurch wird eine Redis-Konsole geöffnet, in der Sie detaillierte Redis-Befehle eingeben können. Versuchen Sie Folgendes:

    ```console
    ping
    ```
    
    ```output
    PONG
    ```
    
    ```console
    set test one
    ```
    
    ```output
    OK
    ```
    
    ```console
    get test
    ```
    
    ```output
    "one"
    ```
    
Kehren Sie zum Panel **Übersicht** zurück. Verwenden Sie dazu entweder die Breadcrumb-Leiste im oberen Bereich, oder verschieben Sie die Ansicht mithilfe der Scrollleiste wieder nach links.

## <a name="retrieve-the-access-keys-and-host-name"></a>Abrufen der Zugriffsschlüssel und des Hostnamens

1. Klicken Sie auf **Einstellungen** > **Zugriffsschlüssel**. 

1. Kopieren Sie die **Primäre Verbindungszeichenfolge (StackExchange.Redis)** an einen sicheren Ort. Sie benötigen sie für die nächste Übung.

    Dieser Schlüssel enthält Ihren Primärschlüssel und Hostnamen in einer vollständigen Verbindungszeichenfolge für die Verwendung in Ihren Anwendungseinstellungen für das **StackExchange.Redis**-Paket, das wir verwenden.

Als Nächstes lernen Sie einige der Befehle zum Abfragen des Caches kennen.