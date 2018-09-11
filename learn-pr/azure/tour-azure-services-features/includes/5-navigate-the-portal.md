Azure-Produkte weisen eine Hierarchie mit mehreren Ebenen auf. Nehmen Sie beispielsweise an, dass Sie einen virtuellen Linux-Computer erstellen möchten. Dafür müssen Sie möglicherweise durch diese Ebenen navigieren: **Startseite** > **Virtuelle Computer** > **Compute** > **Ubuntu Server**. Das Azure-Portal optimiert die Benutzeroberfläche, um solche Navigationssequenzen intuitiv zu gestalten. In dieser Übung untersuchen Sie die wichtigsten Elemente der Benutzeroberfläche, die dies ermöglichen. Sie navigieren durch Menüs und Untermenüs und verwenden Blätter, um Dienste zu suchen und zu konfigurieren.

## <a name="azure-portal-layout"></a>Layout des Azure-Portals

Das Azure-Portal ist die grafische Hauptbenutzeroberfläche für die Steuerung von Microsoft Azure. Sie können einen Großteil der Verwaltungsaktionen im Portal ausführen. Das Portal ist in der Regel auch der beste Ort zur Durchführung einzelner Aufgaben oder zum Anzeigen detaillierter Konfigurationsoptionen.

Im linken Bereich des Portals befindet sich der Ressourcenbereich, in dem die wichtigsten Ressourcentypen aufgeführt werden. Beachten Sie, dass Azure über wesentlich mehr Ressourcentypen verfügt als in dieser Liste angezeigt werden.

## <a name="using-blades-in-the-azure-portal"></a>Verwenden von Blättern im Azure-Portal

Die Navigation im Azure-Portal erfolgt über Blätter. Ein _Blatt_ ist ein einblendbarer Bereich, der die Benutzeroberfläche für eine einzelne Ebene in einer Navigationssequenz enthält. Beispielsweise wird jedes der Elemente dieser Sequenz durch ein Blatt repräsentiert: **Virtuelle Computer** > **Compute** > **Ubuntu Server**.

Jedes Blatt der Benutzeroberfläche enthält in der Regel eine Reihe von konfigurierbaren Optionen. Einige dieser Optionen generieren ein weiteres Blatt, das rechts neben vorhandenen Blättern angezeigt wird. Auch auf dem neuen Blatt erzeugen konfigurierbare Optionen ein weiteres Blatt usw. So ist möglicherweise bereits nach kurzer Zeit eine Vielzahl verschiedener Blätter geöffnet. Sie können Blätter auch maximieren, sodass sie den gesamten Bildschirm ausfüllen.

Wenn Sie versuchen, ein Blatt zu schließen, ohne Konfigurationsänderungen zu speichern, werden Sie in einer Meldung dazu aufgefordert.

## <a name="configuring-settings-in-the-azure-portal"></a>Konfigurieren von Einstellungen im Azure-Portal

Das Azure-Portal zeigt eine Reihe von Konfigurationsoptionen an, die meisten davon in der Statusleiste im oberen rechten Bereich des Bildschirms.

### <a name="notifications"></a>Benachrichtigungen

Durch Klicken auf das Glockensymbol wird der **Benachrichtigungsbereich** angezeigt. In diesem Bereich werden die letzten ausgeführten Aktionen mit dem zugehörigen Status aufgelistet.

![Das Blatt „Benachrichtigungen“](../media-draft/2-notifications-blade.PNG)

### <a name="cloud-shell"></a>Cloud Shell

Wenn Sie auf das **Cloud Shell-Symbol** (>_) klicken, erstellen Sie eine neue Azure Cloud Shell-Sitzung. Sie werden aufgefordert, in dieser Sitzung entweder Linux Bash oder PowerShell unter Linux zu verwenden.

![Cloud Shell](../media-draft/2-choose-shell.PNG)

### <a name="settings"></a>Einstellungen

Klicken Sie auf das **Zahnradsymbol**, um die Einstellungen des Azure-Portals zu ändern. Diese umfassen Folgendes:

* Uhrzeit der Abmeldung
* Farbschema
* Designs mit hohem Kontrast
* Popupbenachrichtigungen (auf einem mobilen Gerät)
* Doppelklicken zum Ändern des Themas
* Sprache
* Regionales Format

![Portaleinstellungen](../media-draft/2-settings-blade.PNG)

Wenn Sie die Einstellungen geändert haben, klicken Sie auf **Übernehmen**, um die Änderungen zu übernehmen.

### <a name="feedback-blade"></a>Das Blatt „Feedback“

Klicken Sie auf das **Smiley-Symbol**, um das Blatt **Senden Sie uns Feedback** zu öffnen. Hier können Sie Feedback zu Azure an Microsoft zu senden. Sie können angeben, ob Microsoft per E-Mail auf Ihr Feedback antworten darf.

![Feedback](../media-draft/2-feedback-blade.PNG)

### <a name="help-blade"></a>Das Blatt „Hilfe“

Klicken Sie auf das **Fragezeichensymbol**, um das Blatt **Hilfe** anzuzeigen. Hier können Sie aus einer Reihe von Themen wie z.B. den folgenden auswählen:

* Neuigkeiten
* Azure-Roadmap
* Interaktive Tour starten
* Tastenkombinationen
* Diagnose anzeigen
* Datenschutz und Nutzungsbedingungen

### <a name="directory-and-subscription"></a>Verzeichnis und Abonnement

Klicken Sie auf das Symbol **Book and Filter** (Buchen und Filtern), um das Blatt **Directory + subscription** (Verzeichnis und Abonnement) anzuzeigen.

In Azure können Sie mehrere Abonnements mit einem einzigen Verzeichnis verknüpfen. Auf dem Blatt **Verzeichnis und Abonnement** können Sie zwischen den Abonnements wechseln. Hier können Sie das Abonnement ändern oder zu einem anderen Verzeichnis wechseln.

![Verzeichnis](../media-draft/2-directory-blade-1.PNG)

### <a name="profile-settings"></a>Profileinstellungen

Wenn Sie in der rechten oberen Ecke auf Ihren Namen klicken, können Sie Ihre Profileinstellungen ändern.
Diese umfassen:

* Von Azure abmelden
* Kennwort ändern
* Kontaktinformationen ändern
* Berechtigungen anzeigen
* Eine Idee an das Azure-Team senden
* Ihre Rechnung anzeigen
* Verzeichnis wechseln (zeigt wie im vorherigen Abschnitt das Blatt **Verzeichnis und Abonnement** an)

![Profileinstellungen](../media-draft/2-portal-menu.png)

Wenn Sie jetzt auf **Meine Rechnung anzeigen** klicken, leitet Azure Sie zur Seite **Kostenverwaltung und Abrechnung – Rechnungen** weiter, auf der Sie analysieren können, wofür Azure-Kosten anfallen.

![Die Seite „Abrechnung“](../media-draft/2-portal-billing.PNG)

## <a name="summary"></a>Zusammenfassung

Azure ist ein sehr umfangreiches Produkt, und die Benutzeroberfläche des Azure-Portals spiegelt dies wider. Das Portal unterstützt Sie dabei, sich in dieser komplexen Struktur zurechtzufinden, indem es Blätter für die verschiedenen Ebenen der Hierarchie bereitstellt. Dank der Blätter können Sie sich auf eine bestimmte Aufgabe konzentrieren, und sie zeigen außerdem eindeutig an, auf welchem Weg Sie zu dieser Aufgabe gelangt sind.