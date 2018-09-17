In dieser Einheit erstellen Sie über das Azure-Portal ein Speicherkonto für eine Web-App, mit der fiktive Surfberichte für Südkalifornien bereitgestellt werden.

Auf einer Website mit Surfberichten können Benutzer Fotos und Videos von den Surfbedingungen an Stränden hochladen. Andere Personen können sich diese Inhalte ansehen und sich dann für einen geeigneten Strand zum Surfen entscheiden. Sie verfolgen die folgenden Ziele im Hinblick auf die Features und das Design:

- Videoinhalte müssen schnell geladen werden.
- Die Website muss mit unerwarteten Lastspitzen beim Upload umgehen können.
- Veraltete Inhalte werden entfernt, wenn sich die Surfbedingungen ändern. Damit wird sichergestellt, dass immer die aktuellen Bedingungen auf der Website angezeigt werden.

Sie entscheiden sich für eine Implementierung, die hochgeladene Inhalte in einer Azure Queue Storage-Warteschlange für die Verarbeitung puffert und diese anschließend zur Speicherung in Azure Blob Storage verschiebt. Sie benötigen nun ein Speicherkonto, das sowohl Warteschlangen als auch Blobs aufnehmen kann, und müssen gleichzeitig Inhalte mit niedriger Latenz übertragen.

## <a name="use-the-azure-portal-to-create-a-storage-account"></a>Erstellen eines Speicherkontos über das Azure-Portal

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true)an.

1. Klicken Sie oben links im Azure-Portal auf **Ressource erstellen**.

1. Klicken Sie im angezeigten Auswahlbereich auf **Storage**.

1. Klicken Sie rechts in diesem Bereich auf **Speicherkonto – Blob, Datei, Tabelle, Warteschlange**.

    ![Screenshot des Azure-Portals mit dem Blatt „Ressourcengruppe erstellen“, der Kategorie „Storage“ und der hervorgehobenen Option „Speicherkonto“](..\media\5-portal-storage-select.png)

### <a name="configure-the-basic-options"></a>Konfigurieren der grundlegenden Optionen

Führen Sie unter **PROJEKTDETAILS** die folgenden Aktionen aus:

1. Wählen Sie das entsprechende **Abonnement** aus.

1. Wählen Sie die vorhandene Ressourcengruppe <rgn>[Sandbox resource group name]</rgn> (Sandbox Ressourcengruppenname) aus der Dropdownliste aus.

    > [!NOTE]
    > Diese kostenlose Ressourcengruppe wurde von Microsoft für das Lernprogramm zur Verfügung gestellt. Wenn Sie ein Konto für eine reale Anwendung erstellen, müssen Sie eine neue Ressourcengruppe in Ihrem Abonnement erstellen, um alle Ressourcen für die App zu speichern.

Führen Sie unter **INSTANZDETAILS** die folgenden Aktionen aus:

1. Geben Sie den **Speicherkontonamen** ein. Dieser wird zum Generieren der öffentlichen URL verwendet, mit der auf Kontodaten zugegriffen wird. Dieser Name muss unter allen vorhandenen Speicherkontonamen in Azure eindeutig sein. Er muss 3 bis 24 Zeichen lang sein und darf nur Kleinbuchstaben und Ziffern enthalten.

1. Wählen Sie einen **Standort** in Ihrer Nähe aus. 

1. Übernehmen Sie für _Resource Manager_ die Standardoption **Bereitstellungsmodell**. Dies ist das bevorzugte Modell für die Bereitstellung von Ressourcen in Azure und ermöglicht es Ihnen, alle Ressourcen für Ihre App in einer _Ressourcengruppe_ zu gruppieren, sodass Sie Ressourcen leichter verwalten können.

1. Wählen Sie für die Option **Leistung** den Eintrag _Standard_ aus. Damit wird der Typ des Datenträgerspeichers festgelegt, auf dem Daten innerhalb des Speicherkontos abgelegt werden. Bei Auswahl von „Standard“ werden übliche Festplatten verwendet. Bei „Premium“ werden SSD-Datenträger (Solid State Drive) genutzt, die einen schnelleren Zugriff ermöglichen. Beachten Sie jedoch, dass bei Auswahl von„Premium“ nur _Seitenblobs_ unterstützt werden. Sie benötigen jedoch Blockblobs für Ihre Videos und eine Warteschlange für die Pufferung. Beides ist nur verfügbar, wenn Sie die Option _Standard_ auswählen.

1. Wählen Sie als _Kontoart_ den Eintrag **StorageV2 (general purpose v2)** (StorageV2 (universell, Version 2)) aus. Dies ermöglicht den Zugriff auf die neuesten Features und Preise. Blobspeicherkonten verfügen bei Auswahl dieser Kontoart über weitere Optionen. Sie benötigen sowohl Blobs als auch eine Warteschlange. Die Option _Blobspeicher_ kann daher nicht verwendet werden. Für diese Anwendung ergäben sich beim Auswählen der Kontoart _Storage (general purpose v1)_ (Speicher (universell, Version 1)) keine Vorteile, da hierdurch die Anzahl der verfügbaren Features beschränkt würde. Außerdem wäre es unwahrscheinlich, dass Sie so die Kosten für die erwartete Arbeitsauslastung reduzieren können.

1. Übernehmen Sie für **Replikation** die Standardeinstellung _Lokal redundanter Speicher (LRS)_. Daten in Azure-Speicherkonten werden stets repliziert, um Hochverfügbarkeit sicherzustellen. Mit dieser Option können Sie auswählen, bis zu welcher Distanz die Replikation erfolgt, sodass Anforderungen an die Dauerhaftigkeit erfüllt werden können. In unserem Fall veralten die Bilder und Videos schnell und werden dann von der Website entfernt. Die Zusatzkosten globaler Redundanz würden hier zu keinem Mehrwert führen. Wenn es durch einen Notfall zu einem Datenverlust käme, könnten Sie die Website mit neuen Benutzerinhalten neu starten.

1. Legen Sie für die **Zugriffsebene** die Einstellung _Hot_ (Heiße Ebene) fest. Diese Einstellung wird nur für den Blobspeicher verwendet. Die **heiße Zugriffsebene** ist ideal für häufig verwendete Daten. Die **kalte Zugriffsebene** eignet sich hingegen besser für selten genutzte Daten. Beachten Sie, dass dadurch nur der _Standardwert_ festgelegt wird: Wenn Sie einen Blob erstellen, können Sie einen anderen Wert für die Daten festlegen. In unserem Fall sollen Videos schnell geladen werden. Daher muss die Hochleistungsoption für Blobs ausgewählt werden.
   
Auf dem folgenden Screenshot werden alle vorgenommenen Einstellungen für die Registerkarte **Basics** (Grundeinstellungen) angezeigt. Beachten Sie, dass für die Ressourcengruppe, das Abonnement und den Namen unterschiedliche Werte festgelegt werden.

![Screenshot des Blatts „Speicherkonto erstellen“ mit ausgewählter Registerkarte **Basics** (Grundeinstellungen)](../media-drafts/5-create-storage-account-basics.png)

### <a name="configure-the-advanced-options"></a>Konfigurieren der erweiterten Optionen

1. Klicken Sie auf **Next: Advanced >** (Weiter: Erweitert >), um die Registerkarte **Erweitert** aufzurufen, oder klicken Sie am oberen Bildschirmrand auf die Registerkarte **Erweitert**.

1. Mit der Einstellung **Sichere Übertragung erforderlich** wird festgelegt, ob REST-APIs über **HTTP** auf Daten im Speicherkonto zugreifen können. Wenn diese Option _Aktiviert_ ist, müssen alle Clients SSL (**HTTPS**) verwenden. In den meisten Fällen sollte diese Einstellung _Aktiviert_ sein, da die Verwendung von HTTPS für Netzwerkübertragungen als bewährte Methode betrachtet wird.

    > [!WARNING]
    > Wenn diese Option aktiviert ist, werden einige zusätzliche Einschränkungen erzwungen. Unverschlüsselte Verbindungen über den Dienst Azure Files schlagen fehl. Dies gilt auch für Szenarios, in denen SMB 2.1 oder 3.0 unter Linux verwendet wird. Diese Option kann nicht zusammen mit Namen benutzerdefinierter Domänen verwendet werden, da Azure Storage SSL für diese nicht unterstützt.

1. Legen Sie für die Option **Virtuelle Netzwerke** die Einstellung _Keine_ fest. Mit dieser Option können Sie das Speicherkonto in einem virtuellen Azure-Netzwerk isolieren. Wir wollen in unserem Szenario einen öffentlichen Zugriff über das Internet unterstützen. Da der Inhalt öffentlich verfügbar sein soll, müssen Sie den Zugriff über öffentliche Clients zulassen.

1. Übernehmen Sie für die Option **Data Lake Storage Gen2** die Standardeinstellung _Deaktiviert_. Diese Option ist für Big Data-Anwendungen relevant, die allerdings in diesem Modul keine Rolle spielen.

Auf dem folgenden Screenshot werden alle vorgenommenen Einstellungen für die Registerkarte **Erweitert** angezeigt.

![Screenshot des Blatts „Speicherkonto erstellen“ mit ausgewählter Registerkarte **Erweitert**](../media-drafts/5-create-storage-account-advanced.png)

### <a name="create"></a>Erstellen

1. Sie können sich die Einstellungen für **Tags** bei Bedarf genauer ansehen. Damit können Sie Ihrem Konto Schlüssel-Wert-Paare für die Kategorisierung zuordnen. Dieses Feature ist für alle Azure-Ressourcen verfügbar.

1. Klicken Sie auf **Überprüfen + erstellen**, um die Einstellungen zu überprüfen. Dadurch wird überprüft, ob alle Pflichtfelder ausgewählt wurden. Wenn Probleme vorliegen, werden diese hier angezeigt. Klicken Sie anschließend auf **Erstellen**, um das Speicherkonto bereitzustellen.

Die Bereitstellung des Kontos dauert einige Minuten. Während dieser Vorgang von Azure ausgeführt wird, sehen wir uns die APIs an, die wir im Folgenden für dieses Konto verwenden werden.

### <a name="verify"></a>Überprüfen

1. Klicken Sie in der linken Randleiste auf den Link **Speicherkonten**.

1. Suchen Sie das neue Speicherkonto in der Liste, um zu überprüfen, ob die Erstellung erfolgreich war.

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

Wenn Sie in Ihrem eigenen Abonnement arbeiten, können Sie die folgenden Schritte im Azure-Portal zum Löschen der Ressourcengruppe und aller zugehörigen Ressourcen ausführen.

1. Klicken Sie in der linken Randleiste auf den Link **Ressourcengruppen**.

1. Such Sie die erstellte Ressourcengruppe in der Liste.

1. Klicken Sie mit der rechten Maustaste auf den Eintrag für die Ressourcengruppe und anschließend im Kontextmenü auf **Ressourcengruppe löschen**. Dasselbe Kontextmenü können Sie aufrufen, indem Sie rechts neben dem Eintrag auf das Menüelement „...“ klicken.

1. Geben Sie den Namen der Ressourcengruppe in das Bestätigungsfeld ein.

1. Klicken Sie auf die Schaltfläche **Löschen**.

## <a name="summary"></a>Zusammenfassung

Sie haben ein Speicherkonto erstellt und die zugehörigen Einstellungen an Ihre geschäftlichen Anforderungen angepasst. Beispielsweise haben Sie für das Rechenzentrum die Region „USA, Westen“ ausgewählt, weil Ihre Kunden sich in erster Linie in Südkalifornien befinden. Dieser Ablauf ist typisch: Zunächst analysieren Sie Ihre Daten und Ziele, und anschließend konfigurieren Sie die entsprechenden Optionen für das Speicherkonto.