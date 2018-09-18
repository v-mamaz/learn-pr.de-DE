In dieser Übung verwenden Sie das Azure-Portal, um eine VM-Skalierungsgruppe mit Regeln für die automatische Skalierung zu erstellen.

## <a name="create-a-virtual-machine-scale-set"></a>Erstellen einer VM-Skalierungsgruppe

1. Klicken Sie im Azure-Portal auf **Ressource erstellen**.

1. Geben Sie im Suchfeld den Suchbegriff **Skalierungsgruppe** ein, und drücken Sie die EINGABETASTE. Klicken Sie auf dem Blatt **Ergebnisse** auf **VM-Skalierungsgruppe** und auf dem Blatt **VM-Skalierungsgruppe** auf **Erstellen**.

1. Geben Sie auf dem Blatt **VM-Skalierungsgruppe erstellen** die folgenden Werte ein (ersetzen Sie `<your initials>`, `<date>` und `<time>` durch die relevanten Daten), und klicken Sie dann auf **Erstellen**.

    |Einstellung|Wert|
    |---|---|
    |Name der VM-Skalierungsgruppe|WebServerSS|
    |Ressourcengruppe|Vorhandene verwenden – ExerciseRG|
    |Benutzername|LocalAdmin|
    |Kennwort und Kennwortbestätigung|Adm1nPa$$word|
    |Anzahl von Instanzen|2|
    |Instanzgröße|D2s_v3|
    |Optionen für den Lastenausgleich auswählen|Load Balancer|
    |Öffentliche IP-Adresse|WebServerPubIP|
    |Domänennamenbezeichnung|`<your initials><date><time>` (z.B. ja0904181202)|

1. Warten Sie, bis die Skalierungsgruppe erstellt wurde.

1. Navigieren Sie zur Ressourcengruppe **ExerciseRG**. Klicken Sie auf dem Blatt **ExerciseRG** auf das Objekt **WebServerSS** und auf dem Blatt **WebServerSS** auf **Instanzen**. Beachten Sie die beiden VM-Instanzen, die in der Skalierungsgruppe ausgeführt werden.

## <a name="create-and-apply-autoscale-rules"></a>Erstellen und Anwenden von Regeln für die automatische Skalierung

1. Klicken Sie auf dem Blatt **WebServerSS** auf **Skalierung**. Klicken Sie auf dem Blatt **WebServerSS – Skalierung** auf **Automatische Skalierung aktivieren**.

1. Klicken Sie auf dem Blatt **WebServerSS – Skalierung** auf **Regel hinzufügen**.

1. Geben Sie auf dem Blatt mit der Regel für die Skalierung die folgenden Informationen ein, um eine Regel zu erstellen, mit der zusätzlich zwei virtuelle Computer horizontal hochskaliert werden sollen (wenn die durchschnittliche CPU-Nutzung mehr als fünf Minuten lang über 75% liegt). Klicken Sie anschließend auf **Hinzufügen**.

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

1. Klicken Sie auf dem Blatt **WebServerSS – Skalierung** auf **Regel hinzufügen**.

1. Geben Sie auf dem Blatt mit der Regel für die Skalierung die folgenden Informationen ein, um eine Regel zu erstellen, mit der jeweils ein Server horizontal herunterskaliert werden soll (wenn die durchschnittliche CPU-Nutzung mehr als fünf Minuten lang unter 30% liegt). Klicken Sie anschließend auf **Hinzufügen**.

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

1. Geben Sie auf dem Blatt **WebServerSS – Skalierung** im Feld **Name der Einstellung für die automatische Skalierung** den Namen **WebAutoscaleSetting** ein. Legen Sie neben **Instanzgrenzwerte** die folgenden Werte fest, und klicken Sie dann auf **Speichern**.

    |Einstellung|Wert|
    |---|---|
    |Minimum|2|
    |Maximum|8|
    |Standard|2|

## <a name="generate-load-to-demonstrate-autoscaling"></a>Generieren einer Last zum Demonstrieren der automatischen Skalierung

Sie verwenden jetzt das Tool „CPUStress.exe“, um die Last für die virtuellen Computer in der Skalierungsgruppe zu generieren und das automatische horizontale Hochskalieren zu demonstrieren.

1. Navigieren Sie zur Ressourcengruppe **ExerciseRG**, um die öffentliche IP-Adresse zu ermitteln, mit der die Verbindung hergestellt werden soll. Klicken Sie auf dem Blatt **ExerciseRG** auf das Objekt **WebServerSSlb**.

1. Klicken Sie auf dem Blatt **WebServerSSlb** auf die Front-End-IP-Konfiguration, und notieren Sie sich die angezeigte öffentliche IP-Adresse. Schließen Sie das Blatt **LoadBalancerFrontEnd**.

1. Klicken Sie auf dem Blatt **WebServerSSlb** auf **NAT-Eingangsregeln**, um die Portnummer für die Verbindungsherstellung zu ermitteln. Notieren Sie sich die benutzerdefinierte Portnummer, die für jeden virtuellen Computer jeweils in der Spalte „Dienst“ angegeben ist.

1. Starten Sie auf Ihrem lokalen Computer die **Remotedesktopverbindung**. Geben Sie im Feld **Computer** die öffentliche IP-Adresse des Lastenausgleichsmoduls ein, gefolgt von einem Doppelpunkt und des Wert für die Portnummer für die Instanz 0 (z.B. 40.67.191.221:50000), und klicken Sie anschließend auf „Verbinden“.

1. Klicken Sie im Dialogfeld **Windows-Sicherheit** auf **Weitere Optionen** und dann auf **Anderes Konto verwenden**, und geben Sie im Feld **Benutzername** den Namen **LocalAdmin** und im Feld **Kennwort** das Kennwort **Adm1nPa$$word** ein. Klicken Sie anschließend auf **OK**.

1. Klicken Sie im Dialogfeld **Remotedesktopverbindung** auf **Ja**.

1. Öffnen Sie über den Remotedesktop des virtuellen Computers den Internet Explorer, und klicken Sie im Dialogfeld **Internet Explorer einrichten** auf **OK**.

1. Geben Sie in **Internet Explorer** in der Adressleiste **http://download.sysinternals.com/files/CPUSTRES.zip** ein, und drücken Sie die EINGABETASTE. Klicken Sie im Dialogfeld **Internet Explorer** auf **Hinzufügen**. Klicken Sie im Dialogfeld **Vertrauenswürdige Sites** auf **Hinzufügen** und dann auf **Schließen**.

1. Falls die Eingabeaufforderung für den Download nicht automatisch angezeigt wird, müssen Sie die URL ggf. erneut eingeben und dann die EINGABETASTE drücken. Klicken Sie im Dialogfeld **Internet Explorer** auf **Speichern**. Klicken Sie nach Abschluss des Downloads auf **Ordner öffnen**.

1. Doppelklicken Sie im Ordner **Downloads** auf **CPUSTRES** und dann auf die Anwendung **CPUSTRES**. Klicken Sie im Dialogfeld **ZIP-komprimierte Ordner** auf **Ausführen**.

1. Wählen Sie im Fenster **CPU Stress** unter **Thread 1** in der Dropdownliste **Aktivität** die Option **Maximum**. Klicken Sie unter **Thread 2** in das Kontrollkästchen **Aktiv**, und wählen Sie in der Dropdownliste **Aktivität** die Option **Maximum**.

1. Klicken Sie auf die Schaltfläche „Start“ und dann auf **Task-Manager**. Klicken Sie im Task-Manager auf **Weitere Details**, und vergewissern Sie sich, dass der CPU-Wert oberhalb von 75% liegt.

1. Wiederholen Sie die Installation und den Start von **CPUSTRES** auf dem anderen virtuellen Computer in der Skalierungsgruppe, und warten Sie dann fünf Minuten.

1. Navigieren Sie im Azure-Portal zur Ressourcengruppe **ExerciseRG**, und klicken Sie auf dem Blatt **ExerciseRG** auf das Objekt **WebServerSS**. Klicken Sie anschließend auf dem Blatt **WebServerSS** auf **Instanzen**. Beachten Sie, wie viele VM-Instanzen in der Skalierungsgruppe aufgeführt sind und welcher Status angezeigt wird.

Hier haben Sie eine VM-Skalierungsgruppe mit zwei virtuellen Computern erstellt. Anschließend haben Sie Regeln zum automatischen horizontalen Hoch- und Herunterskalieren in der Skalierungsgruppe erstellt und die Regeln einem Profil für die automatische Skalierung hinzugefügt.