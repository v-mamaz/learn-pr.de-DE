In dieser Übung erstellen Sie über das Azure-Portal ein Speicherkonto für eine Web-App, mit der fiktive Surfberichte für Südkalifornien bereitgestellt werden.

## <a name="design-goals"></a>Entwurfsziele

Auf einer Website mit Surfberichten können Benutzer Fotos und Videos von den Surfbedingungen an Stränden hochladen. Andere Personen können sich diese Inhalte ansehen und sich dann für einen geeigneten Strand zum Surfen entscheiden. Sie verfolgen die folgenden Ziele im Hinblick auf die Features und das Design:

- Videoinhalte müssen schnell geladen werden.
- Die Website muss mit unerwarteten Lastspitzen beim Upload umgehen können.
- Veraltete Inhalte werden entfernt, wenn sich die Surfbedingungen ändern. Damit wird sichergestellt, dass immer die aktuellen Bedingungen auf der Website angezeigt werden.

Sie entscheiden sich für eine Implementierung, die hochgeladene Inhalte in einer Azure Queue Storage-Warteschlange für die Verarbeitung puffert und diese anschließend zur Speicherung in Azure Blob Storage verschiebt. Sie benötigen nun ein Speicherkonto, das sowohl Warteschlangen als auch Blobs aufnehmen kann, während Inhalte mit niedriger Latenz übertragen werden.

## <a name="exercise-steps"></a>Schritte in dieser Übung

### <a name="launch-the-blade"></a>Aufrufen des Blatts

1. Rufen Sie in Ihrem Webbrowser das [Azure-Portal](https://portal.azure.com?azure-portal=true) auf, und melden Sie sich bei Ihrem Konto an.

1. Klicken Sie in der linken Randleiste auf **Ressource erstellen**.

1. Klicken Sie auf die Überschrift **Storage** im Azure Marketplace.

1. Klicken Sie auf **Speicherkonto**. Im Portal wird das Blatt **Speicherkonto erstellen** angezeigt.

### <a name="configure-the-basic-options"></a>Konfigurieren der grundlegenden Optionen

1. Klicken Sie oben auf dem Blatt auf die Registerkarte **Basics** (Grundeinstellungen).

1. **Abonnement:** Wählen Sie eines Ihrer Abonnements aus.

1. **Ressourcengruppe:** Erstellen Sie eine neue Ressourcengruppe mit dem Namen **SurfReportResourceGroup**.

1. **Speicherkontoname:** Geben Sie einen global eindeutigen Wert ein, der sich beispielsweise aus `surfreport`, Ihren Initialen und einer Zahl zusammensetzt.

 1. **Speicherort:** Wählen Sie **USA, Westen** aus.

    Begründung: Die Anwendung ist für Benutzer in Südkalifornien vorgesehen. Zur Minimierung der Latenz beim Laden von Videos sollten die Blobs in der Nähe dieser Benutzer gehostet werden. Daher ist **USA, Westen** in diesem Fall eine gute Wahl.

1. **Bereitstellungsmodell:** Wählen Sie **Resource Manager** aus.
    
    Begründung: **Resource Manager** ist geeignet, da Sie damit eine Ressourcengruppe verwenden können, um beispielsweise die Web-App und das Speicherkonto für die Anwendung zu verwalten.

1. **Leistung:** Wählen Sie **Standard** aus.

    Begründung: Sie können die Option **Premium** nicht auswählen, da hierdurch nur Seitenblobs für das Speicherkonto verwendet werden können. Sie benötigen für Ihre Videos jedoch Blockblobs und zur Pufferung Warteschlangen. Beides ist nur verfügbar, wenn Sie die Option **Standard** auswählen.

1. **Kontoart:** Wählen Sie **StorageV2 (general purpose v2)** (StorageV2 (allgemein, Version 2)) aus.

    Begründung: **StorageV2 (general purpose v2)** (StorageV2 (allgemein, Version 2)) ist hier die richtige Wahl. Sie benötigen sowohl Blobs als auch eine Warteschlange. Die Option **Blob-Speicher** kann daher nicht verwendet werden. Für diese Anwendung ergäben sich beim Auswählen des Kontotyps **Speicher (Allgemein v1)** keine Vorteile, da hierdurch die Anzahl der verfügbaren Features beschränkt würde. Außerdem wäre es unwahrscheinlich, dass Sie so die Kosten für die erwartete Arbeitsauslastung reduzieren können.

1. **Replikation:** Wählen Sie **Lokal redundanter Speicher (LRS)** aus.

    Begründung: Die Bilder und Videos veralten schnell und werden dann von der Website entfernt. Die Zusatzkosten globaler Redundanz würden hier zu keinem Mehrwert führen. Wenn es durch einen Notfall zu einem Datenverlust käme, könnten Sie die Website mit neuen Benutzerinhalten neu starten.

1. **Zugriffsebene (Standard)**: Wählen Sie **Hot** (Heiße Ebene) aus.
   
    Begründung: Videos sollen schnell geladen werden. Daher muss die Hochleistungsoption für Blobs ausgewählt werden.
   
Auf dem folgenden Screenshot werden alle vorgenommenen Einstellungen für die Registerkarte **Basics** (Grundeinstellungen) angezeigt.

![Screenshot des Blatts „Speicherkonto erstellen“ mit ausgewählter Registerkarte **Basics** (Grundlagen)](../media-drafts/5-create-storage-account-basics.png)

### <a name="configure-the-advanced-options"></a>Konfigurieren der erweiterten Optionen

1. Klicken Sie oben auf dem Blatt auf die Registerkarte **Erweitert**.

1. **Sichere Übertragung erforderlich:** Wählen Sie **Aktiviert** aus.

    Begründung: HTTPS-Übertragungen gehören in der Regel zu den Best Practices.

1. **Virtuelle Netzwerke:** Wählen Sie **Deaktiviert** aus.

    Begründung: Der Inhalt ist öffentlich verfügbar. Sie müssen daher den Zugriff über öffentliche Clients zulassen.

Auf dem folgenden Screenshot werden alle vorgenommenen Einstellungen für die Registerkarte **Erweitert** angezeigt.

![Screenshot des Blatts „Speicherkonto erstellen“ mit ausgewählter Registerkarte **Erweitert**](../media-drafts/5-create-storage-account-advanced.png)

### <a name="create"></a>Erstellen

1. Klicken Sie unten auf dem Blatt auf **Überprüfen + erstellen**.

1. Klicken Sie auf dem nächsten Bildschirm unten auf dem Blatt auf **Erstellen**.

1. Warten Sie, bis die Ressource erstellt wurde.

### <a name="verify"></a>Überprüfen

1. Klicken Sie in der linken Randleiste auf den Link **Speicherkonten**.

1. Suchen Sie das neue Speicherkonto in der Liste, um zu überprüfen, ob die Erstellung erfolgreich war.

### <a name="clean-up"></a>Bereinigen

1. Klicken Sie in der linken Randleiste auf den Link **Ressourcengruppen**.

1. Suchen Sie **SurfReportResourceGroup** in der Liste.

1. Klicken Sie mit der rechten Maustaste auf den Eintrag **SurfReportResourceGroup**, und wählen Sie aus dem Kontextmenü **Ressourcengruppe löschen** aus.

1. Geben Sie den Namen der Ressourcengruppe in das Bestätigungsfeld ein.

1. Klicken Sie auf die Schaltfläche **Löschen**.

## <a name="summary"></a>Zusammenfassung

Sie haben ein Speicherkonto erstellt und die zugehörigen Einstellungen an Ihre geschäftlichen Anforderungen angepasst. Beispielsweise haben Sie für das Rechenzentrum die Region „USA, Westen“ ausgewählt, weil Ihre Kunden sich in erster Linie in Südkalifornien befinden. Dieser Ablauf ist typisch: Zunächst analysieren Sie Ihre Daten und Ziele, und anschließend konfigurieren Sie die entsprechenden Optionen für das Speicherkonto.