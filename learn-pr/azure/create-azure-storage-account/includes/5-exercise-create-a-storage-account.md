In dieser Einheit verwenden Sie das Azure-Portal, um ein Speicherkonto zu erstellen, die für eine fiktive southern California Surf Bericht Web-app geeignet ist.

Die Berichtsserver-Website durchsuchen ermöglicht Benutzern das Hochladen von Fotos und Videos mit ihren lokalen Beach Bedingungen. Andere Personen können sich diese Inhalte ansehen und sich dann für einen geeigneten Strand zum Surfen entscheiden. Sie verfolgen die folgenden Ziele im Hinblick auf die Features und das Design:

- Videoinhalte müssen schnell geladen werden.
- Die Website muss mit unerwarteten Lastspitzen beim Upload umgehen können.
- Veraltete Inhalte werden entfernt, wenn sich die Surfbedingungen ändern. Damit wird sichergestellt, dass immer die aktuellen Bedingungen auf der Website angezeigt werden.

Sie entscheiden sich für eine Implementierung, die hochgeladene Inhalte in einer Azure Queue Storage-Warteschlange für die Verarbeitung puffert und diese anschließend zur Speicherung in Azure Blob Storage verschiebt. Sie benötigen ein Speicherkonto, das sowohl Warteschlangen und Blobs aufnehmen kann, während der Übermittlung von niedriger Latenz beim Zugriff auf Ihre Inhalte.

## <a name="use-the-azure-portal-to-create-a-storage-account"></a>Verwenden Sie zum Erstellen eines Speicherkontos im Azure-portal

[!include[](../../../includes/azure-sandbox-activate.md)]

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true)an.

1. Oben links im Azure-Portal wählen **erstellen Sie eine Ressource**.

1. Wählen Sie im Auswahlbereich, der angezeigt wird, **Storage**.

1. Wählen Sie auf der rechten Seite dieses Bereichs **Speicherkonto – Blob, Datei, Tabelle, Warteschlange**.

    ![Screenshot des Azure-Portal mit dem Erstellen der Blatt einer Ressource mit der Kategorie "Speicher" und hervorgehobener Option für Storage-Konto.](..\media\5-portal-storage-select.png)

### <a name="configure-the-basic-options"></a>Konfigurieren der grundlegenden Optionen

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

Klicken Sie unter **PROJEKTDETAILS**:

1. Wählen Sie das entsprechende **Abonnement** aus.

1. Wählen Sie die vorhandene Ressourcengruppe <rgn>[Ressourcengruppennamen Sandkasten]</rgn> aus der Dropdown-Liste.

    > [!NOTE]
    > Dieser kostenlose Ressourcengruppe wurde von Microsoft als Teil der Learning-Umgebung bereitgestellt. Wenn Sie ein Konto für eine reale Anwendung erstellen, möchten Sie erstellen eine neue Ressourcengruppe in Ihrem Abonnement aus, um alle Ressourcen für die app zu speichern.

Klicken Sie unter **INSTANZDETAILS**:

1. Geben Sie einen **speicherkontonamen**. Der Name wird zum Generieren der öffentlichen URL für den Zugriff auf die Daten im Konto verwendet werden. Sie müssen für alle vorhandenen speicherkontonamen in Azure eindeutig sein. Er muss 3 bis 24 Zeichen lang sein und darf nur Kleinbuchstaben und Ziffern enthalten.

1. Wählen Sie eine **Speicherort** Nähe Sie. 

1. Lassen Sie die **Bereitstellungsmodell** als _RM_. Dies ist die bevorzugte Methode für alle ressourcenbereitstellungen in Azure und ermöglicht Ihnen, alle zugehörigen Ressourcen für Ihre app zu gruppieren einer _Ressourcengruppe_ zur einfacheren Verwaltung.

1. Wählen Sie _Standard_ für die **Leistung** Option. Diese entscheidet sich der Datenträger-Speichertyp zum Speichern der Daten im Speicherkonto verwendet. Standard verwendet herkömmliche-Festplatten und Premium Solid State Drives (SSD) für einen schnelleren Zugriff. Beachten Sie jedoch, dass Premium nur unterstützt _Seitenblobs_ und Sie müssen blockiert, Blobs, die für Ihre Videos und eine Warteschlange für die Pufferung – beide sind nur verfügbar, mit der _Standard_ Option.

1. Wählen Sie _StorageV2 (Allgemein, Version 2)_ für die **Kontoart**. Dies ermöglicht den Zugriff auf die neuesten Features und Preise. Blob Storage-Konten haben insbesondere Weitere Optionen, die mit diesem Konto verfügbar. Sie benötigen eine Mischung aus Blobs und eine Warteschlange, sodass die _Blob-Speicher_ Option funktioniert nicht. Für diese Anwendung, es gäbe keine Vorteile beim Auswählen einer _Speicher (Allgemein v1)_ -Konto, da, die die Features, Sie einschränken würden zugreifen können und wäre es unwahrscheinlich, dass die Kosten für die erwartete arbeitsauslastung zu reduzieren.

1. Lassen Sie die **Replikation** als _lokal redundanter Speicher (LRS)_. Daten in Azure Storage-Konten werden stets repliziert, um hochverfügbarkeit sicherzustellen – mit dieser Option können Sie auswählen, wie weit Sie entfernt die Replikation erfolgt entsprechend Ihrer Anforderungen an die Dauerhaftigkeit. In unserem Fall die Bilder und Videos schnell sind veraltet und werden vom Standort entfernt. Die Zusatzkosten globaler Redundanz würden hier zu keinem Mehrwert führen. Wenn es durch einen Notfall zu einem Datenverlust käme, könnten Sie die Website mit neuen Benutzerinhalten neu starten.

1. Legen Sie die **Zugriffsebene** zu _"heiß"_. Diese Einstellung wird nur für Blob Storage verwendet. Die **heiße Zugriffsebene** eignet sich ideal für häufig verwendete Daten und die **kalte Zugriffsebene** ist besser für selten genutzte Daten. Beachten Sie, dass dies nur die _Standard_ -Wert: Wenn Sie ein Blob erstellen können Sie festlegen einen anderen Wert für die Daten. In diesem Fall möchten wir die Videos, die schnell geladen werden, daher Sie die Option für hohe Leistung für Ihre Blobs verwenden.
   
Auf dem folgenden Screenshot werden alle vorgenommenen Einstellungen für die Registerkarte **Basics** (Grundeinstellungen) angezeigt. Beachten Sie, dass die Ressourcengruppe, Abonnements und Namen unterschiedliche Werte.

![Screenshot: Erstellen einer Storage-Konto auf dem Blatt mit den ** Grundlagen ** Registerkarte ausgewählt.](../media/5-create-storage-account-basics.png)

### <a name="configure-the-advanced-options"></a>Konfigurieren der erweiterten Optionen

1. Klicken Sie auf die **weiter: Erweitert >** Schaltfläche zum Verschieben der **erweitert** Registerkarte, oder wählen Sie die **erweitert** Registerkarte am oberen Rand des Bildschirms.

1. Die **sichere Übertragung erforderlich** Einstellung steuert, ob **HTTP** für die REST-APIs verwendet, um Zugriff auf Daten in das Speicherkonto verwendet werden kann. Wenn diese Option auf _aktiviert_ erzwingt, dass alle Clients zur Verwendung von SSL (**HTTPS**). In den meisten Fällen möchten diese Einstellung auf _aktiviert_ wie die Verwendung von HTTPS über das Netzwerk wird als bewährte Methode betrachtet.

    > [!WARNING]
    > Wenn diese Option aktiviert ist, wird es einige zusätzlichen Einschränkungen erzwungen. Azure Files-Dienst-Verbindungen ohne Verschlüsselung schlägt fehl, einschließlich Szenarien für die Verwendung von SMB 2.1 oder 3.0 unter Linux. Da es sich bei Azure-Speicher SSL für benutzerdefinierte Domänennamen nicht unterstützt, kann nicht diese Option mit einem benutzerdefinierten Domänennamen verwendet werden.

1. Legen Sie die **virtuelle Netzwerke** option _keine_. Diese Option können Sie das Speicherkonto in ein Azure virtual Network zu isolieren. Öffentlichen Zugriff auf das Internet verwendet werden soll. Unsere Inhalte ist öffentlich, und Sie müssen, um den Zugriff aus öffentlichen Clients zu ermöglichen.

1. Lassen Sie die **Data Lake-Speicher Gen2** option _deaktiviert_. Dies ist für big Data-Anwendungen, die nicht auf dieses Modul relevant sind.

Auf dem folgenden Screenshot werden alle vorgenommenen Einstellungen für die Registerkarte **Erweitert** angezeigt.

![Screenshot des Blatts „Speicherkonto erstellen“ mit ausgewählter Registerkarte **Erweitert**](../media/5-create-storage-account-advanced.png)

### <a name="create"></a>Erstellen

1. Sie können untersuchen, die **Tags** Einstellungen bei Bedarf. Dies können Sie Schlüssel/Wert-Paare, mit dem Konto für Ihre Kategorisierung zuordnen und eine Funktion, die für alle Azure-Ressource verfügbar ist.

1. Klicken Sie auf **überprüfen + erstellen** zur Überprüfung der Einstellungen. Dies ist eine schnelle Überprüfung die Optionen, um sicherzustellen, dass alle erforderlichen Felder ausgewählt werden. Wenn Probleme vorliegen, werden diese hier angezeigt. Nachdem Sie die Einstellungen überprüft haben, klicken Sie auf **erstellen** das Storage-Konto bereitstellen.

Es dauert einige Minuten, bis das Konto bereitstellen. Während es sich bei Azure an, die arbeitet, sehen wir uns auf die APIs, die wir für dieses Konto verwendet werden.

### <a name="verify"></a>Überprüfen

1. Klicken Sie in der linken Randleiste auf den Link **Speicherkonten**.

1. Suchen Sie das neue Speicherkonto in der Liste, um zu überprüfen, ob die Erstellung erfolgreich war.

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

Wenn Sie in Ihrem eigenen Abonnement arbeiten, können Sie die folgenden Schritte im Azure-Portal die Ressourcengruppe und alle zugehörigen Ressourcen zu löschen.

1. Klicken Sie in der linken Randleiste auf den Link **Ressourcengruppen**.

1. Suchen Sie die Ressourcengruppe aus, die Sie in der Liste erstellt haben.

1. Mit der rechten Maustaste auf den Ressourceneintrag für die Gruppe aus, und wählen Sie **Ressourcengruppe löschen** aus dem Kontextmenü. Klicken Sie auf "..." Menu-Elements auf der rechten Seite des Eintrags, um das gleiche Kontextmenü zu erhalten.

1. Geben Sie den Namen der Ressourcengruppe in das Bestätigungsfeld ein.

1. Klicken Sie auf die Schaltfläche **Löschen**.

## <a name="summary"></a>Zusammenfassung

Sie haben ein Speicherkonto erstellt und die zugehörigen Einstellungen an Ihre geschäftlichen Anforderungen angepasst. Sie können z. B. ein Rechenzentrum USA (Westen) ausgewählt haben, weil Ihre Kunden sich in erster Linie in Südkalifornien befanden. Dies ist ein typischer Ablauf: zunächst analysieren Ihrer Daten und die Ziele, und die Optionen für das Storage-Konto entsprechend konfigurieren.