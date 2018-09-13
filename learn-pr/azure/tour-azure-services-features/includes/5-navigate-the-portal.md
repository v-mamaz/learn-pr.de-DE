Nachdem wir nun über ein Konto verfügen, können wir uns beim **Azure-Portal** anmelden. Beim Portal handelt es sich um einen webbasierten Standort der zentralen Verwaltung mit allen Abonnements und Ressourcen, die Sie erstellt haben. Über diese Webschnittstelle können Sie praktisch alle Aktionen mit Azure ausführen.

## <a name="azure-portal-layout"></a>Layout des Azure-Portals

Das Azure-Portal ist die zentrale grafische Benutzeroberfläche für die Steuerung von Microsoft Azure. Sie können einen Großteil der Verwaltungsaktionen im Portal ausführen. Das Portal ist in der Regel auch der beste Ort zur Durchführung einzelner Aufgaben oder zum Anzeigen detaillierter Konfigurationsoptionen.

![Das Azure-Portal](../media-draft/5-portal.png)

:::row:::

    :::column:::
    ![The resources and favorites](../media-draft/5-favorites.png)
    :::column-end:::

    :::column span="3":::
    **Resource Panel**
    
    In the left-hand sidebar of the portal is the resource pane, which lists the main resource types. Note that Azure has more resource types than just those shown. The resources listed are part of your _favorites_. 

    You can customize this with the specific resource types you tend to create or administer most often. 

    You can also collapse this pane; with the **<<** caret. This will minimize it to just icons which can be convenient if you are working with limited screen real-estate.
    :::column-end:::

:::row-end:::

Der restliche Teil der Portalansicht ist für die jeweiligen Elemente bestimmt, mit denen Sie arbeiten. Das _Dashboard_ ist die Standardseite (Hauptseite). Wir behandeln das Dashboard später. Aber soviel schon jetzt: Es stellt eine anpassbare Übersicht über Ihre Ressourcen dar. Sie können es verwenden, um zu bestimmten Ressourcen zu wechseln, die Sie verwalten möchten, oder um mit dem Eintrag **Alle Ressourcen** im Ressourcenbereich nach Ressourcen zu suchen. Beim Verwalten einer Ressource, wie etwa einem virtuellen Computer oder einer Web-App, arbeiten Sie mit einem _Blatt_, auf dem bestimmte Informationen über die Ressource angezeigt werden.

## <a name="what-is-a-blade"></a>Was ist ein Blatt?

Die Navigation im Azure-Portal erfolgt über Blätter. Ein _Blatt_ ist ein einblendbarer Bereich, der die Benutzeroberfläche für eine einzelne Ebene in einer Navigationssequenz enthält. Beispielsweise wird jedes der Elemente dieser Sequenz durch ein Blatt repräsentiert: **Virtuelle Computer** > **Compute** > **Ubuntu Server**.

Jedes Blatt enthält Informationen und konfigurierbare Optionen. Einige dieser Optionen generieren ein weiteres Blatt, das rechts neben vorhandenen Blättern angezeigt wird. Auch auf dem neuen Blatt erzeugen konfigurierbare Optionen ein weiteres Blatt usw. So ist möglicherweise bereits nach kurzer Zeit eine Vielzahl verschiedener Blätter geöffnet. Sie können Blätter auch maximieren, sodass sie den gesamten Bildschirm ausfüllen.

Da neue Blätter immer rechts neben dem Besitzer hinzugefügt werden, können Sie mithilfe der Scrollleiste am unteren Fensterrand zurückgehen, um nachzuvollziehen, wie Sie zum jeweiligen Teil der Konfiguration gelangt sind. Alternativ können Sie Blätter einzeln schließen, indem Sie auf die Schaltfläche `X` in der oberen Ecke des Blatts klicken. Wenn Sie Änderungen vorgenommen, aber noch nicht gespeichert haben, werden Sie von Azure darüber informiert, dass die Änderungen verloren gehen, wenn Sie den Vorgang fortsetzen.

## <a name="configuring-settings-in-the-azure-portal"></a>Konfigurieren von Einstellungen im Azure-Portal

Das Azure-Portal zeigt eine Reihe von Konfigurationsoptionen an, die meisten davon in der Statusleiste im oberen rechten Bereich des Bildschirms.

### <a name="notifications"></a>Benachrichtigungen

Durch Klicken auf das Glockensymbol wird der **Benachrichtigungsbereich** angezeigt. In diesem Bereich werden die letzten ausgeführten Aktionen mit dem zugehörigen Status aufgelistet.

![Das Blatt „Benachrichtigungen“](../media-draft/5-notifications-blade.png)

### <a name="cloud-shell"></a>Cloud Shell

Wenn Sie auf das **Cloud Shell-Symbol** (>_) klicken, erstellen Sie eine neue Azure Cloud Shell-Sitzung. Azure Cloud Shell ist eine interaktive, über den Browser zugängliche Shell für die Verwaltung von Azure-Ressourcen. Es bietet Ihnen die Flexibilität, die Shell-Benutzeroberfläche auszuwählen, die sich am besten für Ihre Arbeitsweise eignet. Linux-Benutzer können Bash-Benutzeroberflächen verwenden, während Windows-Benutzer PowerShell nutzen können. Mit diesem browserbasierten Terminal können Sie Ihre Azure-Ressourcen im aktuellen Abonnement über eine im Portal integrierte Befehlszeilenschnittstelle steuern und verwalten.

![Cloud Shell](../media-draft/5-choose-shell.png)

### <a name="settings"></a>Einstellungen

Klicken Sie auf das **Zahnradsymbol**, um die Einstellungen des Azure-Portals zu ändern. Diese umfassen Folgendes:

- Uhrzeit der Abmeldung
- Farbschema
- Designs mit hohem Kontrast
- Popupbenachrichtigungen (auf einem mobilen Gerät)
- Doppelklicken zum Ändern des Themas
- Sprache
- Regionales Format

![Portaleinstellungen](../media-draft/5-settings-blade.png)

Wenn Sie die Einstellungen geändert haben, klicken Sie auf **Übernehmen**, um die Änderungen zu übernehmen.

### <a name="feedback-blade"></a>Das Blatt „Feedback“

Klicken Sie auf das **Smiley-Symbol**, um das Blatt **Senden Sie uns Feedback** zu öffnen. Hier können Sie Feedback zu Azure an Microsoft zu senden. Sie können angeben, ob Microsoft per E-Mail auf Ihr Feedback antworten darf.

![Feedback](../media-draft/5-feedback-blade.png)

### <a name="help-blade"></a>Das Blatt „Hilfe“

Klicken Sie auf das **Fragezeichensymbol**, um das Blatt **Hilfe** anzuzeigen. Hier stehen verschiedene Optionen zur Auswahl, darunter Folgende:

- Neuigkeiten
- Azure-Roadmap
- Interaktive Tour starten
- Tastenkombinationen
- Diagnose anzeigen
- Datenschutz und Nutzungsbedingungen

### <a name="directory-and-subscription"></a>Verzeichnis und Abonnement

Klicken Sie auf das Symbol **Book and Filter** (Buchen und Filtern), um das Blatt **Directory + subscription** (Verzeichnis und Abonnement) anzuzeigen.

In Azure können Sie mehrere Abonnements mit einem einzigen Verzeichnis verknüpfen. Auf dem Blatt **Verzeichnis und Abonnement** können Sie zwischen den Abonnements wechseln. Hier können Sie das Abonnement ändern oder zu einem anderen Verzeichnis wechseln.

![Verzeichnis](../media-draft/5-directory-blade-1.png)

### <a name="profile-settings"></a>Profileinstellungen

Wenn Sie in der rechten oberen Ecke auf Ihren Namen klicken, können Sie Ihre Profileinstellungen ändern.
Diese umfassen:

- Von Azure abmelden
- Kennwort ändern
- Kontaktinformationen ändern
- Berechtigungen anzeigen
- Eine Idee an das Azure-Team senden
- Ihre Rechnung anzeigen
- Verzeichnis wechseln (zeigt wie im vorherigen Abschnitt das Blatt **Verzeichnis und Abonnement** an)

![Profileinstellungen](../media-draft/5-portal-menu.png)

Wenn Sie jetzt auf **Meine Rechnung anzeigen** klicken, leitet Azure Sie zur Seite **Kostenverwaltung und Abrechnung – Rechnungen** weiter, auf der Sie analysieren können, wofür Azure-Kosten anfallen.

![Die Seite „Abrechnung“](../media-draft/5-portal-billing.png)

Azure ist ein sehr umfangreiches Produkt, und die Benutzeroberfläche des Azure-Portals spiegelt dies wider. Dank dem Konzept der verschiebbaren Blätter können Sie in den verschiedenen Verwaltungsaufgaben mühelos vor und zurück navigieren. Experimentieren Sie mit dieser Benutzeroberfläche, damit Sie ein wenig Übung bekommen.