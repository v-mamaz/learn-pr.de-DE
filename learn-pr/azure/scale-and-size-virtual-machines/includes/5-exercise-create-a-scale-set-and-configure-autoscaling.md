In dieser Übung verwenden Sie das Azure-Portal eine VM-Skalierungsgruppe Regeln für die automatische Skalierung zu erstellen.

## <a name="create-a-virtual-machine-scale-set"></a>Erstellen einer Skalierungsgruppe für virtuelle Computer

1. Klicken Sie im Azure-Portal auf **Ressource erstellen**.

1. Geben Sie in das Suchfeld **Skalierungsgruppe** und drücken Sie EINGABETASTE. Auf der **Ergebnisse** auf dem Blatt klicken Sie auf **VM-Skalierungsgruppe**, und klicken Sie auf die **VM-Skalierungsgruppe** auf dem Blatt klicken Sie auf **erstellen**.

1. Auf der **VM-Skalierungsgruppe erstellen** auf dem Blatt, geben Sie die folgenden Werte (ersetzen `<your initials>`, `<date>`, und `<time>` mit relevanten Daten), und klicken Sie dann auf **erstellen**.

    |Einstellung|Wert|
    |---|---|
    |Name der VM-Skalierungsgruppe|WebServerSS|
    |Ressourcengruppe|Vorhandene - <rgn>[Sandkasten Resource Group-Name]</rgn>|
    |Username|LocalAdmin|
    |Das Kennwort und kennwortbestätigung|Adm1nPa$$word|
    |Anzahl von Instanzen|2|
    |Instanzgröße|D2s_v3|
    |Wählen Sie Optionen für den Lastenausgleich|Load Balancer|
    |Name der öffentlichen IP-Adresse|WebServerPubIP|
    |Domänennamenbezeichnung|`<your initials><date><time>` (z. B. ja0904181202)|

1. Warten Sie, bis die Skalierungsgruppe erstellt werden.

1. Navigieren Sie zu der **<rgn>[Ressourcengruppennamen Sandkasten]</rgn>** Ressourcengruppe aus. Auf der **<rgn>[Ressourcengruppennamen Sandkasten]</rgn>** auf dem Blatt klicken Sie auf die **WebServerSS** -Objekt, und klicken Sie auf die **WebServerSS** auf dem Blatt klicken Sie auf **Instanzen**. Beachten Sie die beiden VM-Instanzen, die in der Skalierungsgruppe ausgeführt.

## <a name="create-and-apply-autoscale-rules"></a>Erstellen und Anwenden von Regeln zur automatischen Skalierung

1. Auf der **WebServerSS** auf dem Blatt klicken Sie auf **Skalierung**. Auf der **WebServerSS - Skalierung** auf dem Blatt klicken Sie auf **Aktivieren der automatischen Skalierung**.

1. Auf der **WebServerSS - Skalierung** auf dem Blatt klicken Sie auf **fügen Sie eine Regel**.

1. Auf der **skalierungsregel** auf dem Blatt, geben Sie die folgende Informationen zum Erstellen einer Regel zum horizontalen hochskalieren einer zusätzlichen zwei virtuelle Computer, wenn der durchschnittliche CPU-Auslastung über 75 % über einen Zeitraum von fünf Minuten, und klicken Sie dann auf befindet **hinzufügen**.

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

1. Auf der **WebServerSS - Skalierung** auf dem Blatt klicken Sie auf **fügen Sie eine Regel**.

1. Auf der **skalierungsregel** auf dem Blatt, geben Sie die folgende Informationen zum Erstellen einer Regel zum Skalieren auf einem Server zu einer Zeit, durchschnittliche CPU-Auslastung unter 30 % über einen Zeitraum von fünf Minuten, und klicken Sie dann auf **hinzufügen**.

    |Einstellung|Wert|
    |---|---|
    |Zeitaggregation|Durchschnitt|
    |Metrikname|CPU in Prozent|
    |Statistik zum Aggregationsintervall|Durchschnitt|
    |Operator|Kleiner als |
    |Schwellenwert|30|
    |Dauer (in Minuten)|5|
    |Vorgang|Anzahl verringern um|
    |Anzahl von Instanzen|1|
    |Abkühlen (Minuten)|5|

1. Auf der **WebServerSS - Skalierung** Blatt in der **Name der Einstellung für die automatische Skalierung** geben **WebAutoscaleSetting**. Neben **Instanzgrenzwerte**, legen Sie die folgenden Werte, und klicken Sie dann auf **speichern**.

    |Einstellung|Wert|
    |---|---|
    |Minimum|2|
    |Maximum|8|
    |Standard|2|

## <a name="generate-load-to-demonstrate-autoscaling"></a>Generieren einer Last, um die automatische Skalierung zu demonstrieren.

Verwenden Sie das Tool CPUStress.exe jetzt zum Generieren einer Last auf den virtuellen Computern in der Skalierungsgruppe, und zeigen Sie die automatische Skalierung.

1. Um die öffentliche IP-Adresse für die Verbindung zu bestimmen, navigieren Sie zu der **ExerciseRG** Ressourcengruppe aus. Auf der **ExerciseRG** auf dem Blatt klicken Sie auf die **WebServerSSlb** Objekt.

1. Auf der **WebServerSSlb** auf dem Blatt klicken Sie auf **Frontend IP-Konfiguration** und notieren Sie sich die öffentliche IP-Adresse angezeigt. Schließen der **LoadBalancerFrontEnd** Blatt.

1. Um zu bestimmen, die Portnummer für die Verbindung, auf die **WebServerSSlb** auf dem Blatt klicken Sie auf **NAT-Eingangsregeln**. Notieren Sie sich die benutzerdefinierte Portnummer in der Spalte "Dienst" für jeden virtuellen Computer.

1. Starten Sie auf dem lokalen Computer die **Remotedesktopverbindung**. In der **Computer** Feld, geben Sie die öffentliche IP-Adresse des Load Balancers, gefolgt von einem Doppelpunkt und dann die Nummer des Ports den Wert für die Instanz 0 (z. B. 40.67.191.221:50000), und klicken Sie dann auf **Connect**.

1. In der **Windows-Sicherheit** Dialogfeld klicken Sie auf **Weitere Optionen**, und klicken Sie dann auf **verwenden ein anderes Konto**. In der **Benutzernamen** geben **LocalAdmin**. In der **Kennwort** geben **Adm1nPa$ $Word**, und klicken Sie dann auf **OK**.

1. In der **Remotedesktopverbindung** Dialogfeld klicken Sie auf **Ja**.

1. Auf dem virtuellen Computer remote Desktop, öffnen Sie Internet Explorer, und in der **richten Sie Internet Explorer** Dialogfeld klicken Sie auf **OK**.

1. In **Internet Explorer**, geben Sie in der Adressleiste **http://download.sysinternals.com/files/CPUSTRES.zip** und drücken Sie EINGABETASTE. In der **Internet Explorer** Dialogfeld klicken Sie auf **hinzufügen**. In der **vertrauenswürdige Sites** Dialogfeld klicken Sie auf **hinzufügen** , und klicken Sie dann auf **schließen**.

1. Wenn die downloadeingabeaufforderung nicht automatisch angezeigt wird, müssen Sie möglicherweise geben die URL erneut ein, und drücken EINGABETASTE. In der **Internet Explorer** Dialogfeld klicken Sie auf **speichern**. Nachdem der Download abgeschlossen ist, klicken Sie auf **"Ordner öffnen"**.

1. In der **Downloads** Ordner doppelklicken Sie auf **CPUSTRES**, und doppelklicken Sie dann auf die **CPUSTRES** Anwendung. In der **komprimierten (gezippten) Ordner** Dialogfeld klicken Sie auf **ausführen**.

1. In der **CPU Stress** Fenster unter **Thread 1**in die **Aktivität** Dropdownliste, wählen **maximale**. Unter **Thread 2**, klicken Sie auf die **Active** Kontrollkästchen, und klicken Sie in der **Aktivität** Dropdownliste, wählen **maximale**.

1. Klicken Sie auf die Schaltfläche "Start", und klicken Sie dann **Task-Manager**. Klicken Sie im Task-Manager **mehr**, und vergewissern Sie sich, dass die CPU über 75 % ist.

1. Wiederholen Sie die Installation und die Einführung von **CPUSTRES** auf dem anderen virtuellen Computer in der Skalierungsgruppe festgelegt, und klicken Sie dann auf fünf Minuten warten.

1. Navigieren Sie im Azure-Portal zu der **ExerciseRG** Ressourcengruppe aus. Auf der **ExerciseRG** auf dem Blatt klicken Sie auf die **WebServerSS** Objekt. Auf der **WebServerSS** auf dem Blatt klicken Sie auf **Instanzen**. Beachten Sie, wie viele VM-Instanzen in der Skalierungsgruppe und den Status angezeigt werden.

Hier haben Sie eine VM-Skalierungsgruppe mit zwei virtuellen Computern erstellt. Sie klicken Sie dann Regeln aus, um Automatisches horizontales hochskalieren und Herunterskalieren der Skalierungsgruppe erstellt und Sie die Regeln zu einem Profil für die automatische Skalierung hinzugefügt.