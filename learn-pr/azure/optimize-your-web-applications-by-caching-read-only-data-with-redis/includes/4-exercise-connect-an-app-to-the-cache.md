In dieser Übung erstellen Sie eine Azure Redis Cache-Instanz zum Speichern und Zurückgeben häufig verwendeter Werte.

## <a name="create-a-cache"></a>Erstellen eines Caches

1. Melden Sie sich beim Azure-Portal an. Klicken Sie dann auf **Ressource erstellen**, **Datenbanken** und **Redis Cache**.

    Der folgende Screenshot zeigt den Redis Cache-Speicherort innerhalb der verschiedenen Datenbankressourcen-Optionen im Azure-Portal.

    ![Screenshot mit den Datenbankoptionen des Azure-Portals, wobei die Optionen „Ressource erstellen“, „Datenbank“ und „Redis Cache“ hervorgehoben sind.](../media/4-create-a-cache-1.png)

## <a name="configure-your-cache"></a>Konfigurieren Ihres Caches

1. **DNS-Name**: Erstellen Sie einen global eindeutigen Namen, z.B. **ContosoSportsApp1028**.

1. **Abonnement**: Wählen Sie Ihr Abonnement aus.

1. **Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe, und geben Sie ihr einen Namen.

1. **Speicherort**: Da die meisten Ihrer Kunden sich im Bereich New York befinden, wählen Sie **USA, Osten** aus.

1. **Tarif**: Wählen Sie **Basic C0** aus.

1. Klicken Sie auf **Erstellen**.

    Der folgende Screenshot zeigt eine repräsentative Konfiguration, die zum Erstellen einer neuen Redis Cache-Ressource verwendet wird.

    ![Screenshot mit dem Azure-Portal-Blatt beim Erstellen einer neuen Redis Cache-Ressource mit Beispielkonfigurations-DNS-Name, Abonnement, neuer Ressourcengruppe, Speicherort und Tarif.](../media/4-create-a-cache-2.png)

> [!IMPORTANT]
> Bevor Sie fortfahren, müssen Sie warten, bis der Cache bereitgestellt wird. Dieser Vorgang kann eine Weile dauern.

## <a name="retrieve-the-access-keys-and-host-name"></a>Abrufen der Zugriffsschlüssel und des Hostnamens

1. Navigieren Sie im Azure-Portal zu Ihrem Cache, und wählen Sie **Einstellungen** > **Zugriffsschlüssel** aus. Notieren Sie sich die **primäre Verbindungszeichenfolge (StackExchange.Redis)**.

    Dieser Schlüssel enthält Ihren Primärschlüssel und Hostnamen in einer vollständigen Verbindungszeichenfolge für die Verwendung in Ihren Anwendungseinstellungen für das StackExchange.Redis-Paket, das wir verwenden.

1. Starten Sie den Editor oder einen anderen Texteditor auf Ihrem Computer.

1. Fügen Sie folgenden Inhalt hinzu:

    Ersetzen Sie `<connection-string>` durch die primäre Verbindungszeichenfolge Ihres Caches von oben.

    ```xml
    <appSettings>
        <add key="CacheConnection" value="<connection-string>"/>
    </appSettings>
    ```

1. Speichern Sie die Datei an einem Ort, an dem sie nicht in den Quellcode Ihrer Beispielanwendung einbezogen wird. In diesem Tutorial speichern wir die Datei unter `C:\AppSecrets\CacheSecrets.config`.

## <a name="create-a-console-app"></a>Erstellen einer Konsolen-App

1. Starten Sie Visual Studio, und klicken Sie auf das Menüelement **Datei** > **Neu** > **Projekt...**.

1. Wählen Sie die Vorlage **Visual C#** > **Windows Desktop** > **Konsolen-App** aus.

1. Geben Sie Ihrer App einen Namen, und klicken Sie auf **OK**, um eine neue Konsolenanwendung zu erstellen.

## <a name="configure-the-cache-client"></a>Konfigurieren des Cacheclients

In diesem Abschnitt konfigurieren Sie die Konsolenanwendung zur Verwendung des **StackExchange.Redis**-Clients für .NET.

1. Klicken Sie in Visual Studio auf **Tools**, zeigen Sie auf **NuGet-Paket-Manager**, klicken Sie auf **Paket-Manager-Konsole**, und führen Sie im Fenster der Paket-Manager-Konsole den folgenden Befehl aus:

    ```powershell
    Install-Package StackExchange.Redis
    ```

Nach Abschluss der Installation kann der StackExchange.Redis-Cacheclient für Ihr Projekt verwendet werden.

## <a name="connect-to-the-cache"></a>Herstellen einer Verbindung mit dem Cache

1. Öffnen Sie in Visual Studio die Datei **App.config** im **Projektmappen-Explorer**, und aktualisieren Sie sie, sodass sie ein **appSettings**-Dateiattribut enthält, das auf die Datei **CacheSecrets.config** verweist.

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.1" />
        </startup>

        <appSettings file="C:\AppSecrets\CacheSecrets.config"></appSettings>

    </configuration>
    ```

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Verweise**, und klicken Sie anschließend auf **Verweis hinzufügen...**. Wählen Sie **System.Configuration** in der Liste **Assemblys** > **Framework** aus, und klicken Sie auf **OK**.

1. Fügen Sie der Datei **Program.cs** die folgenden `using`-Anweisungen hinzu:

    ```csharp
    using StackExchange.Redis;
    using System.Configuration;
    ```

Die Verbindung mit Azure Redis Cache wird von der ConnectionMultiplexer-Klasse verwaltet. Diese Klasse sollte für Ihre gesamte Clientanwendung genutzt und wiederverwendet werden. Erstellen Sie nicht für jeden Vorgang eine neue Verbindung.

Speichern Sie niemals Anmeldeinformationen im Quellcode. Hier wird nur eine externe Konfigurationsdatei für Geheimnisse verwendet, um dieses Beispiel einfach zu halten. Ein besserer Ansatz wäre die Nutzung von Azure Key Vault mit Zertifikaten.

1. Fügen Sie in der Datei **Program.cs** der Program-Klasse Ihrer Konsolenanwendung die folgenden Member hinzu:

    ```csharp
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

Bei diesem Ansatz zum Freigeben einer ConnectionMultiplexer-Instanz in Ihrer Anwendung wird eine statische Eigenschaft verwendet, die eine verbundene Instanz zurückgibt. Dieser Code ist eine threadsichere Möglichkeit, um nur eine einzelne verbundene ConnectionMultiplexer-Instanz zu initialisieren. **abortConnect** ist auf „false“ festgelegt. Dies bedeutet, dass der Aufruf erfolgreich ist, auch wenn keine Verbindung mit Azure Redis Cache hergestellt wird. Eine wichtige Funktion von ConnectionMultiplexer ist, dass die Verbindung mit dem Cache automatisch wiederhergestellt wird, sobald das Netzwerkproblem oder andere Ursachen beseitigt wurden.

Der Wert der appSetting-Einstellung **CacheConnection** wird verwendet, um über das Azure-Portal auf die Cacheverbindungszeichenfolge als Kennwortparameter zu verweisen.
