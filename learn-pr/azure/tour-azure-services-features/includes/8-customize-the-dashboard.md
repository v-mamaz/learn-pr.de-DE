Als Nächstes schauen wir uns an, wie Sie Dashboards mithilfe des Azure-Portals und durch direktes Bearbeiten der zugrunde liegenden JSON-Datei erstellen und ändern können.

## <a name="what-is-a-dashboard"></a>Was ist ein Dashboard?

Ein _Dashboard_ ist eine anpassbare Sammlung von Benutzeroberflächenkacheln, die im Azure-Portal angezeigt werden. Sie können Kacheln hinzufügen, entfernen und anordnen, um genau die gewünschte Ansicht zu erstellen und sie dann als Dashboard zu speichern. Es werden mehrere Dashboards unterstützt, und Sie können nach Bedarf zwischen ihnen wechseln. Sie können Ihre Dashboards auch für andere Teammitglieder freigeben.

Dashboards bieten Ihnen viel Flexibilität bei der Verwaltung von Azure. Sie können z.B. Dashboards für bestimmte Rollen innerhalb der Organisation erstellen und dann die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) verwenden, um zu steuern, wer auf das jeweilige Dashboard zugreifen darf. So kann Ihr Datenbankadministrator ein Dashboard einrichten, das Ansichten des SQL-Datenbank-Diensts enthält, und Ihr Azure Active Directory-Administrator kann Ansichten der Benutzer und Gruppen in Azure AD erhalten. Sie können das Portal auch für Ihre Produktions- und Entwicklungsumgebung anpassen – dabei erstellen Sie ein spezielles Dashboard für jede Umgebung, die Sie verwalten.

Dashboards werden als JSON-Dateien (JavaScript Object Notation) gespeichert. Das bedeutet, dass sie auf andere Computer hoch- und heruntergeladen oder mit Mitgliedern des Azure Active Directory gemeinsam genutzt werden können. Azure speichert Dashboards in Ressourcengruppen genauso wie virtuelle Computer oder Speicherkonten, die Sie im Portal verwalten können.

> [!TIP]
> Da Dashboards JSON-Dateien sind, können Sie sie auch [programmgesteuert anpassen](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards-create-programmatically) und zu faszinierenden Verwaltungstools machen. Darüber hinaus können einige Kacheltypen abfragebasiert sein und bei Änderung der Quelldaten automatisch aktualisiert werden.

## <a name="explore-the-default-dashboard"></a>Untersuchen des Standarddashboards

Das Standarddashboard wird als „Dashboard“ bezeichnet. Wenn Sie sich beim Portal anmelden, wird Ihnen dieses Dashboard mit fünf Webparts angezeigt.

![Standardwebparts](../media-draft/8-dashboard-default-webparts.png)

Dies sind die Standardwebparts:

1. Alle Ressourcen

1. Schnellstarts + Tutorials

1. Service Health

1. Marketplace

1. Erste Schritte mit Azure

## <a name="creating-and-managing-dashboards"></a>Erstellen und Verwalten von Dashboards

Oberhalb des Dashboards befinden sich die Steuerelemente, mit denen Sie ein Dashboard erstellen, hochladen, herunterladen, bearbeiten und freigeben können. Sie können ein Dashboard auch in den Vollbildmodus schalten oder es klonen oder löschen.

![Anpassen von Dashboardsteuerelementen](../media-draft/8-customise-dashboard-controls.png)

- [Auswählen eines Dashboards](#select-dashboard)
- [Erstellen eines neuen Dashboards](#create-new)
- [Hochladen und Herunterladen](#upload-download)
- [Bearbeiten](#edit-dashboard)
- [Freigeben](#share-dashboard)
- [Vollbild](#full-screen)
- [Klonen](#clone-dashboard)
- [Löschen](#delete-dashboard)

<a name="select-dashboard"></a>

## <a name="select-dashboard"></a>Auswählen eines Dashboards

Ganz links in der Symbolleiste befindet sich das Dropdownsteuerelement **Dashboard auswählen**. Wenn Sie auf dieses Steuerelement klicken, können Sie aus Dashboards auswählen, die Sie bereits für Ihr Konto definiert haben. Mit diesem Steuerelement können Sie ganz einfach mehrere Dashboards für verschiedene Zwecke definieren und dann zwischen den Dashboards wechseln, je nachdem, welche Aufgabe Sie gerade erledigen möchten.

Beachten Sie, dass alle von Ihnen erstellten Dashboards zunächst privat sind, also nur Sie diese anzeigen können. Um ein Dashboard weiteren Personen in Ihrem Unternehmen zur Verfügung zu stellen, müssen Sie es freigeben. Wir gehen in Kürze auf diese Option ein.

<a name="create-new"></a>

## <a name="create-a-new-dashboard"></a>Erstellen eines neuen Dashboards

Um ein neues Dashboard zu erstellen, klicken Sie einfach auf **Neues Dashboard**. Der Dashboardarbeitsbereich wird ohne Kacheln angezeigt. Sie können dann Kacheln nach Belieben hinzufügen, entfernen und anpassen, womit wir uns in Kürze näher befassen werden. Wenn Sie mit der Anpassung des Dashboards fertig sind, klicken Sie auf **Anpassung abgeschlossen**, um es zu speichern und zu diesem Dashboard zu wechseln.

<a name="upload-download"></a>

## <a name="upload-and-download"></a>Hochladen und Herunterladen

Mit den Schaltflächen **Hochladen** und **Herunterladen** können Sie Ihr aktuelles Dashboard als JSON-Datei herunterladen, es anpassen und dann verteilen und hochladen. Auch eine andere Person kann diese Datei wieder in das Azure-Portal hochladen und dadurch ihr eigenes aktuelles Dashboard ersetzen.

Wenn Sie auf **Herunterladen** klicken, wird das aktuelle Dashboard in Ihren standardmäßigen Ordner für Downloads heruntergeladen. Wenn Sie die heruntergeladene Datei öffnen, wird der JSON-Code angezeigt.

![JSON-Code des Dashboards](../media-draft/8-dashboard-json-code.png)

Sie können diesen Code manuell bearbeiten, indem Sie z.B. Kachelgrößen ändern und den Code dann per Klick auf die Schaltfläche **Hochladen** wieder in Azure hochladen.

<a name="edit-dashboard"></a>

### <a name="edit-a-dashboard"></a>Bearbeiten eines Dashboards

Sie können zwar ein Dashboard bearbeiten, indem Sie die JSON-Datei herunterladen, Werte in der Datei ändern und die Datei wieder in Azure hochladen. Allerdings ist diese Vorgehensweise für den Entwurf einer Benutzeroberfläche nicht intuitiv. Um die grafische Benutzeroberfläche zum Konfigurieren Ihres aktuellen Dashboards zu verwenden, können Sie auf verschiedene Weise in den Bearbeitungsmodus wechseln:

1. Klicken Sie auf die Schaltfläche **Bearbeiten**.
1. Klicken Sie mit der rechten Maustaste auf das Dashboard, und klicken Sie auf **Bearbeiten**. 
1. Bewegen Sie den Mauszeiger auf dem Dashboard auf eine Kachel, sodass ein `...`-Menü mit Bearbeitungsoptionen in der oberen rechten Ecke angezeigt wird.

Das Dashboard wechselt in den Bearbeitungsmodus.

![Dashboard bearbeiten](../media-draft/8-edit-dashboard.png)

Auf der linken Seite wird der Kachelkatalog mit einer Reihe möglicher Kacheln angezeigt. Sie können den Kachelkatalog nach folgenden Kriterien filtern:

- Allgemein
- Typ
- Suchen
- Ressourcengruppe
- Tag

![Kachelkatalog](../media-draft/8-tile-gallery.png)

Sie können jede dieser Optionen nach Kategorie weiter eingrenzen, z.B. Azure Active Directory, Internet der Dinge (IoT), Microsoft Intune usw.

Um Kacheln hinzuzufügen, wählen Sie einfach aus der Liste links eine Kachel aus, und ziehen Sie diese in den Arbeitsbereich. Sie können jede Kachel verschieben, ihre Größe oder die darin angezeigten Daten ändern.

> [!TIP]
> Ein interessantes Feature, das viele Benutzer nicht kennen, ist die Möglichkeit, dass Sie Elemente von untergeordneten Blättern auf Ihrem Dashboard platzieren können. Bewegen Sie einfach den Mauszeiger auf das Element, und platzieren Sie mit der „An Dashboard anheften“-Option des `...`-Kachelbearbeitungsmenüs schnell eine Kachel aus einem Dienst auf dem Dashboard.

Der Arbeitsbereich ist im Bearbeitungsmodus in Quadrate unterteilt. Jede Kachel muss mindestens ein Quadrat belegen, wobei Kacheln an den nächstgelegenen Trennlinien ausgerichtet werden. Überlappenden Kacheln werden beiseite verschoben. Wenn Sie eine Kachel verkleinern, werden die umgebenden Kacheln wieder in die Nähe geschoben.

#### <a name="change-tile-sizes"></a>Ändern der Kachelgrößen

Einige Kacheln verfügen über eine festgelegte Größe, die Sie nur programmgesteuert bearbeiten können. Sie können jedoch Kacheln mit einer grauen Ecke rechts unten bearbeiten, indem Sie die Eckmarkierung mit der Maus ziehen.

![Kachel mit veränderbarer Größe](../media-draft/8-resizable-tile.png)

Alternativ dazu können Sie auch mit der rechten Maustaste auf das Kontextmenü klicken und die gewünschte Größe angeben.

![Kachelgröße](../media-draft/8-tile-size.png)

Um ein Dashboard zu erstellen, ziehen Sie Kacheln aus dem Kachelkatalog in den Arbeitsbereich und ordnen sie an.

#### <a name="change-tile-settings"></a>Ändern der Kacheleinstellungen

Einige Kacheln weisen Einstellungen auf, die sich bearbeiten lassen. Wenn Sie z.B. die Kachel „Uhr“ in den Arbeitsbereich ziehen, wird die Kachel **Uhr bearbeiten** geöffnet. Dort können Sie die Zeitzone sowie die Anzeige im 12- oder 24-Stunden-Format festlegen.

![Bearbeiten der Uhr](../media-draft/8-edit-clock.png)

In multinationalen oder transkontinentalen Unternehmen können Sie Uhren hinzufügen, die jeweils unterschiedliche Zeitzonen anzeigen.

#### <a name="accepting-your-edits"></a>Übernehmen der Änderungen

Wenn Sie die Kacheln nach Wunsch angeordnet haben, klicken Sie auf **Anpassung abgeschlossen**, oder klicken Sie mit der rechten Maustaste und klicken dann auf **Anpassung abgeschlossen**.

## <a name="edit-a-dashboard-by-changing-the-json-file"></a>Bearbeiten eines Dashboards durch Ändern der JSON-Datei

Sie können ein Dashboard auch durch Ändern der JSON-Datei bearbeiten. Diese Vorgehensweise bietet mehr Optionen für das Ändern von Einstellungen, aber Sie können die Änderungen erst sehen, nachdem Sie die Datei wieder in Azure hochgeladen haben.

![JSON-Einstellungen](../media-draft/8-json-code.png)

Um im Beispiel oben die Größe der Kachel zu ändern, bearbeiten Sie die Variablen **colSpan** und **rowSpan**. Speichern Sie dann die Datei, und laden Sie sie wieder in Azure hoch. Sie können die Datei auch an andere Benutzer verteilen.

## <a name="reset-a-dashboard"></a>Zurücksetzen eines Dashboards

Sie können jedes Dashboard auf den Standardstil zurücksetzen. Klicken Sie im Bearbeitungsmodus mit der rechten Maustaste, und wählen Sie **Auf Standardzustand zurücksetzen** aus. Sie werden in einem Dialogfeld aufgefordert, zu bestätigen, dass Sie dieses Dashboard zurücksetzen möchten.

<a name="share-dashboard"></a>

## <a name="share-or-unshare-a-dashboard"></a>Freigeben bzw. Aufheben der Freigabe eines Dashboards

Wenn Sie ein neues Dashboard definieren, ist es privat und nur für Ihr Konto sichtbar. Um anderen Benutzer die Ansicht des Dashboards zu ermöglichen, müssen Sie es freigeben. Sie müssen jedoch, wie bei jeder anderen Azure-Ressource auch, eine Ressourcengruppe angeben (oder eine vorhandenen Ressourcengruppe verwenden), in der freigegebene Dashboards gespeichert werden. Wenn Sie nicht über eine vorhandene Ressourcengruppe verfügen, erstellt Azure die Ressourcengruppe *Dashboards* an einem von Ihnen angegebenen Speicherort. Wenn Sie über eine Ressourcengruppe verfügen, können Sie diese verwenden, um die Dashboards zu speichern.

![Freigabe und Zugriffssteuerung 1](../media-draft/8-share-dashboards-default.png)

Wenn Sie die Vorlage freigegeben haben, sehen Sie ein zweites Blatt: **Freigabe + Zugriffssteuerung**.

![Freigabe und Zugriffssteuerung 2](../media-draft/8-share-dashboards-access-control.png)

Sie können dann auf **Benutzer verwalten** klicken, um die Benutzer anzugeben, die auf dieses Dashboard zugreifen dürfen.

### <a name="switching-to-a-shared-dashboard"></a>Wechsel zu einem freigegebenen Dashboard

Um zu einem freigegebenen Dashboard zu wechseln, klicken Sie auf die Liste der Dashboards und dann auf **Alle Dashboards durchsuchen**.

![Alle Dashboards durchsuchen](../media-draft/8-browse-dashboards.png)

Sie sehen das Blatt **Alle Dashboards**, auf dem die Namen aller freigegebenen Dashboards angezeigt werden. Klicken Sie auf ein Dashboard, um es auf das Azure-Portal anzuwenden.

![Freigegebene Dashboards](../media-draft/8-select-shared-dashboard.png)

<a name="full-screen"></a>

## <a name="display-a-dashboard-as-a-full-screen"></a>Anzeigen eines Dashboards im Vollbildmodus

Wenn Sie das Dashboard möglichst groß anzeigen möchten, klicken Sie auf die Schaltfläche **Vollbild**, um Ihr aktuelles Dashboard ohne Browsermenüs anzuzeigen. Falls sich Kacheln außerhalb der Bildschirmanzeige befinden, werden rechts und unten auf dem Bildschirm Schieberegler angezeigt.

Um den Vollbildmodus zu beenden, drücken Sie die ESC-Taste, oder klicken Sie am oberen Bildschirmrand neben dem Dashboardnamen auf **Vollbildmodus beenden**.

<a name="clone-dashboard"></a>

## <a name="clone-a-dashboard"></a>Klonen eines Dashboards

Beim Klonen eines Dashboards wird eine Sofortkopie namens „Klon von \<Dashboardname>“ erstellt, wobei diese Kopie zum aktuellen Dashboard wird. Klonen ist auch eine einfache Möglichkeit, Dashboards zu erstellen, bevor sie freigegeben werden. Wenn Sie z.B. über ein Dashboard verfügen, das bereits fast Ihren Wünschen entspricht, klonen Sie es, nehmen die notwendigen Änderungen vor und geben es dann frei.

<a name="delete-dashboard"></a>

## <a name="delete-a-dashboard"></a>Löschen eines Dashboards

Durch Löschen eines Dashboards wird es aus der Liste der verfügbaren Dashboards entfernt. Sie werden aufgefordert zu bestätigen, dass Sie das Dashboard löschen möchten. Beachten Sie aber, dass es keine Möglichkeit gibt, ein gelöschtes Dashboard wiederherzustellen.

Wir werden nun einige dieser Optionen ausprobieren, indem wir ein neues Dashboard erstellen.
