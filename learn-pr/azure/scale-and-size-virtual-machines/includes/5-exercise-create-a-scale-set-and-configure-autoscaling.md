In dieser Übung verwenden Sie das Azure-Portal, um eine VM-Skalierungsgruppe mit Regeln für die automatische Skalierung zu erstellen.

## <a name="create-a-virtual-machine-scale-set"></a>Erstellen einer VM-Skalierungsgruppe

1. Klicken Sie im [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) auf **Ressource erstellen**.

1. Geben Sie im Suchfeld den Suchbegriff **Skalierungsgruppe** ein, und drücken Sie die <kbd>EINGABETASTE</kbd>. Klicken Sie auf dem Blatt **Ergebnisse** auf **VM-Skalierungsgruppe** und auf dem Blatt **VM-Skalierungsgruppe** auf **Erstellen**.

1. Geben Sie auf dem Blatt **VM-Skalierungsgruppe erstellen** die folgenden Werte ein.
    - Verwenden Sie _WebServerSS_ als **Namen**.
    - Behalten Sie für **Betriebssystem-Datenträgerimage** den Wert _Windows Server 2016 Datacenter_ bei.
    - Wählen Sie unter **Abonnement** die Option _Concierge Subscription_ (Concierge-Abonnement) aus.
    - Wählen Sie **<rgn>[Name der Sandboxressourcengruppe]</rgn>** als **Ressourcengruppe** aus.
    - Wählen Sie einen Standort aus der folgenden Liste aus: [!include[](../../../includes/azure-sandbox-regions-note-friendly.md)]

    - Legen Sie einen gültigen **Benutzernamen** und ein gültiges **Kennwort** fest. (Notieren Sie sich beides für die spätere Verwendung.)
    - Legen Sie die **Instanzanzahl** auf _2_ fest.
    - Legen Sie die **Instanzgröße** auf _D2s_v3_ fest.
    - Behalten Sie für die **Autoskalierung** den Wert _Deaktiviert_ bei.
    - Wählen Sie **Load Balancer** aus.
    - Geben Sie _WebServerPubIP_ unter **Öffentliche IP-Adresse** ein.
    - Verwenden Sie Ihre Initialen, Ihr Datum und Ihre Uhrzeit für die **Domänennamenbezeichnung**, damit sie eindeutig ist.
    - Wählen Sie unter **Virtuelles Netzwerk** die Option **Neu erstellen** aus. Benennen Sie es **SSVNet**, und klicken Sie dann auf **Erstellen**, um das VNET zu erstellen.

1. Klicken Sie zum Bereitstellen der Skalierungsgruppe auf **Erstellen**.

1. Warten Sie, bis die Skalierungsgruppe erstellt wurde.

## <a name="create-and-apply-autoscale-rules"></a>Erstellen und Anwenden von Regeln für die automatische Skalierung

1. Klicken Sie in der linken Seitenleiste auf **Ressourcengruppen**.

1. Wählen Sie die Ressourcengruppe **<rgn>[Name der Sandboxressourcengruppe]</rgn>** aus.

1. Klicken Sie auf dem Blatt **<rgn>[Name der Sandboxressourcengruppe]</rgn>** auf das Objekt **WebServerSS**, um die Skalierungsgruppe zu öffnen.

1. Klicken Sie auf dem Blatt **WebServerSS** unter **Einstellungen** auf **Instanzen**. Beachten Sie die beiden VM-Instanzen, die in der Skalierungsgruppe ausgeführt werden.

1. Klicken Sie auf dem Blatt **WebServerSS** auf **Skalierung**.

1. Klicken Sie auf dem Blatt **WebServerSS – Skalierung** auf **Automatische Skalierung aktivieren**.

1. Legen Sie den Namen auf dem Konfigurationsbildschirm auf **WebAutoscaleSetting** fest.

1. Suchen Sie in der Standardbedingung die **Instanzgrenzwerte**, und legen Sie die folgenden Werte fest.

    |Einstellung|Wert|
    |---|---|
    |Minimum|2|
    |Maximum|8|
    |Standard|2|

1. Klicken Sie auf **Add a rule** (Regel hinzufügen).

1. Geben Sie auf dem Blatt **Regel skalieren** die folgenden Informationen ein, um eine Regel zu erstellen, mit der zusätzlich zwei virtuelle Computer horizontal hochskaliert werden können, wenn die durchschnittliche CPU-Nutzung mehr als fünf Minuten lang über 75 % liegt. Klicken Sie anschließend auf **Hinzufügen**.

    |Einstellung|Wert|
    |---|---|
    |Zeitaggregation|Durchschnitt|
    |Metrikname|CPU in Prozent|
    |Statistik zum Aggregationsintervall|Durchschnitt|
    |Operator|Größer als|
    |Schwellenwert|75|
    |Dauer (in Minuten)|5|
    |Vorgang|Anzahl erhöhen um|
    |Anzahl von Instanzen|2|
    |Abkühlen (Minuten)|5|

1. Fügen Sie eine andere Regel hinzu, und geben Sie die folgenden Informationen ein, um eine Regel zu erstellen, mit der jeweils ein Server horizontal herunterskaliert werden kann, wenn die durchschnittliche CPU-Nutzung mehr als fünf Minuten lang unter 30 % liegt. Klicken Sie anschließend auf **Hinzufügen**.

    |Einstellung|Wert|
    |---|---|
    |Zeitaggregation|Durchschnitt|
    |Metrikname|CPU in Prozent|
    |Statistik zum Aggregationsintervall|Durchschnitt|
    |Operator|Kleiner als|
    |Schwellenwert|30|
    |Dauer (in Minuten)|5|
    |Vorgang|Anzahl verringern um|
    |Anzahl von Instanzen|1|
    |Abkühlen (Minuten)|5|

1. Ihre Regeln sollten in etwa so aussehen:

    ![Screenshot der Regeln für die Autoskalierung, die auf die VM-Skalierungsgruppe angewendet werden](../media/5-scale-rules.png)

1. Klicken Sie auf **Speichern**.

## <a name="generate-load-to-demonstrate-autoscaling"></a>Generieren einer Last zum Demonstrieren der automatischen Skalierung

Sie verwenden jetzt das Tool **CPUStress.exe** von SysInternals, um die Last für die virtuellen Computer in der Skalierungsgruppe zu generieren und das automatische horizontale Hochskalieren zu demonstrieren.

Sie führen dieses auf der VM aus. Sie benötigen zwar kein Windows, dafür ist jedoch ein Remotedesktopclient _erforderlich_. Microsoft hat einen für macOS und einen für Windows, und verschiedene Linux-Distributionen enthalten ebenfalls einen Client.

1. Navigieren Sie zur Ressourcengruppe **<rgn>[Name der Sandboxressourcengruppe]</rgn>**, um die öffentliche IP-Adresse zu ermitteln, mit der die Verbindung hergestellt werden soll. Klicken Sie auf dem Blatt **<rgn>[Name der Sandboxressourcengruppe]</rgn>** auf das Objekt **WebServerSSlb**.

1. Klicken Sie auf dem Blatt **WebServerSSlb** auf die **Front-End-IP-Konfiguration**, und notieren Sie sich die angezeigte öffentliche IP-Adresse. Schließen Sie das Blatt **LoadBalancerFrontEnd**.

1. Klicken Sie auf dem Blatt **WebServerSSlb** auf **NAT-Eingangsregeln**, um die Portnummer für die Verbindungsherstellung zu ermitteln. Notieren Sie sich die benutzerdefinierte Portnummer, die für jeden virtuellen Computer jeweils in der Spalte „Dienst“ angegeben ist.

1. Starten Sie auf Ihrem lokalen Computer die **Remotedesktopverbindung**. Geben Sie im Feld **Computer** die öffentliche IP-Adresse des Lastenausgleichsmoduls ein, gefolgt von einem Doppelpunkt und des Wert für die Portnummer für die Instanz 0 (z.B. 40.67.191.221:50000), und klicken Sie anschließend auf **Verbinden**.

1. Klicken Sie im Dialogfeld **Windows-Sicherheit** auf **Weitere Optionen** und dann auf **Anderes Konto verwenden**. Geben Sie die Dialogfelder **Benutzername** und **Kennwort** die Anmeldeinformationen ein, die Sie bei der Erstellung der Skalierungsgruppe oben angegeben haben.

1. Klicken Sie im Dialogfeld **Remotedesktopverbindung** auf **Ja**.

1. Öffnen Sie über den Remotedesktop des virtuellen Computers Internet Explorer, und klicken Sie im Dialogfeld **Internet Explorer einrichten** auf **OK**.

1. Geben Sie in **Internet Explorer** in der Adressleiste **http://download.sysinternals.com/files/CPUSTRES.zip** ein, und drücken Sie die <kbd>EINGABETASTE</kbd>. Klicken Sie im Dialogfeld **Internet Explorer** auf **Hinzufügen**. Klicken Sie im Dialogfeld **Vertrauenswürdige Sites** auf **Hinzufügen** und dann auf **Schließen**.

1. Falls die Eingabeaufforderung für den Download nicht automatisch angezeigt wird, müssen Sie die URL ggf. erneut eingeben und dann die <kbd>EINGABETASTE</kbd> drücken. Klicken Sie im Dialogfeld **Internet Explorer** auf **Speichern**. Klicken Sie nach Abschluss des Downloads auf **Ordner öffnen**.

1. Doppelklicken Sie im Ordner **Downloads** auf **CPUSTRES** und dann auf die Anwendung **CPUSTRES**. Klicken Sie im Dialogfeld **ZIP-komprimierte Ordner** auf **Ausführen**.

1. Wählen Sie im Fenster **CPU Stress** unter **Thread 1** in der Dropdownliste **Aktivität** die Option **Maximum** aus. Klicken Sie unter **Thread 2** auf das Kontrollkästchen **Aktiv**, und klicken Sie in der Dropdownliste **Aktivität** auf den Pfeil nach unten, und wählen Sie die Option **Maximum** aus. Diese Einstellungen werden sofort wirksam.

1. Klicken Sie auf die Windows-Startschaltfläche und dann auf **Task-Manager**. Klicken Sie im Task-Manager auf **Weitere Details**, und vergewissern Sie sich, dass der CPU-Wert oberhalb von 75 % liegt.

1. **Wiederholen** Sie die Installation und den Start von **CPUSTRES** auf dem anderen virtuellen Computer in der Skalierungsgruppe, und warten Sie dann fünf Minuten.

1. Navigieren Sie im Azure-Portal zur Ressourcengruppe **<rgn>[Name der Sandboxressourcengruppe]</rgn>**. Klicken Sie auf dem Blatt **<rgn>[Name der Sandboxressourcengruppe]</rgn>** auf das Objekt **WebServerSS**. Klicken Sie auf dem Blatt **WebServerSS** auf **Instanzen**. Beachten Sie, wie viele VM-Instanzen in der Skalierungsgruppe aufgeführt sind und welcher Status angezeigt wird.

Hier haben Sie eine VM-Skalierungsgruppe mit zwei virtuellen Computern erstellt. Anschließend haben Sie Regeln zum automatischen horizontalen Hoch- und Herunterskalieren in der Skalierungsgruppe erstellt und die Regeln einem Profil für die automatische Skalierung hinzugefügt.
