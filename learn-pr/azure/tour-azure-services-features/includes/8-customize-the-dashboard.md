In dieser Übung erstellen und ändern Sie Dashboards über die Portalbenutzeroberfläche und durch direkte Bearbeitung der zugrunde liegenden JSON-Datei.

## <a name="what-is-a-dashboard"></a>Was ist ein Dashboard?

Ein _Dashboard_ ist eine anpassbare Sammlung von Benutzeroberflächenkacheln, die im Azure-Portal angezeigt werden. Sie können Kacheln hinzufügen, entfernen und positionieren, um genau die gewünschte Ansicht zu erstellen, und diese Ansicht dann als Dashboard speichern. Es werden mehrere Dashboards unterstützt, und Sie können nach Bedarf zwischen ihnen wechseln. Sie können Ihr Dashboards auch für andere Teammitglieder freigeben.

Dashboards bieten Ihnen viel Flexibilität bei der Verwaltung von Azure. Sie können z.B. Dashboards für bestimmte Rollen innerhalb der Organisation erstellen und dann die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) verwenden, um zu steuern, wer auf das Dashboard zugreifen darf. So kann Ihr Datenbankadministrator ein Dashboard einrichten, das Ansichten des SQL-Datenbank-Diensts enthält, und Ihr Azure Active Directory-Administrator kann Ansichten der Benutzer und Gruppen in Azure AD erhalten.

Dashboards werden als JSON-Dateien (JavaScript Object Notation) gespeichert. Das bedeutet, dass sie auf andere Computer hoch- und heruntergeladen oder mit Mitgliedern des Azure Active Directory gemeinsam genutzt werden. Azure speichert Dashboards in Ressourcengruppen genauso wie virtuelle Computer oder Speicherkonten, die Sie im Portal verwalten können.

Da Dashboards JSON-Dateien sind, können Sie sie auch programmgesteuert anpassen und zu sehr leistungsstarken Verwaltungstools machen. Darüber hinaus können einige Kacheltypen abfragebasiert sein und bei Änderung der Quelldaten automatisch aktualisiert werden.

## <a name="default-dashboard"></a>Standarddashboard

Das Standarddashboard heißt einfach Dashboard. Wenn Sie sich beim Portal anmelden, wird Ihnen dieses Dashboard mit fünf Webparts angezeigt.

![Standardwebparts](../images/4-dashboard-default-webparts.png)

Dies sind die Standardwebparts:

1. Alle Ressourcen
2. Schnellstarts + Tutorials
3. Dienstintegrität
4. Marketplace
5. Erste Schritte mit Azure

## <a name="creating-and-managing-dashboards"></a>Erstellen und Verwalten von Dashboards

Oberhalb des Dashboards befinden sich die Steuerelemente, mit denen Sie ein Dashboard erstellen, hochladen, herunterladen, bearbeiten und freigeben können. Sie können ein Dashboard auch in den Vollbildmodus schalten oder es klonen oder löschen.

![Anpassen von Dashboardsteuerelementen](../images/7-customise-dashboard-controls.PNG)

### <a name="select-dashboard"></a>Dashboard auswählen

Links befindet sich das Dropdown-Steuerelement „Dashboard auswählen“. Wenn Sie auf dieses Steuerelement klicken, können Sie aus Dashboards auswählen, die Sie bereits für Ihr Konto definiert haben. Mit diesem Steuerelement können Sie ganz einfach mehrere Dashboards für verschiedene Zwecke definieren und dann zwischen den Dashboards wechseln, je nachdem, welche Aufgabe Sie gerade erledigen möchten.

Beachten Sie, dass alle von Ihnen erstellten Dashboards zunächst privat sind, also nur Sie diese anzeigen können. Um ein Dashboard weiteren Personen in Ihrem Unternehmen zur Verfügung zu stellen, müssen Sie es freigeben. Weitere Informationen finden Sie im Abschnitt zum Freigeben bzw. Aufheben der Freigabe von Dashboards weiter unten in dieser Übung.

### <a name="create-a-new-dashboard"></a>Erstellen eines neuen Dashboards

Um ein neues Dashboard zu erstellen, klicken Sie einfach auf **Neues Dashboard**. Der Dashboardarbeitsbereich wird angezeigt, es sind keine Kacheln vorhanden. Sie können jetzt Kacheln hinzufügen, wie im Abschnitt zum Bearbeiten eines Dashboards über die Benutzeroberfläche weiter unten in dieser Übung erläutert. Wenn Sie mit dem Hinzufügen und Anpassen von Kacheln fertig sind und den Namen des Dashboards geändert haben, klicken Sie einfach auf **Anpassung abgeschlossen**, um das Dashboard zu speichern und dorthin zu wechseln.

### <a name="upload-and-download"></a>Hochladen und Herunterladen

Mit den Schaltflächen **Hochladen** und **Herunterladen** können Sie Ihr aktuelles Dashboard als JSON-Datei herunterladen, es anpassen und dann verteilen und hochladen. Auch eine andere Person kann diese Datei wieder in das Azure-Portal hochladen und dadurch ihr eigenes aktuelles Dashboard ersetzen.

Wenn Sie auf **Herunterladen** klicken, wird das aktuelle Dashboard in Ihren standardmäßigen Ordner für Downloads heruntergeladen. Wenn Sie die heruntergeladene Datei öffnen, wird der JSON-Code angezeigt.

![JSON-Code des Dashboards](../images/7-dashboard-json-code.PNG)

Sie können diesen Code manuell bearbeiten, indem Sie z.B. Kachelgrößen ändern, und den Code dann per Klick auf die Schaltfläche **Hochladen** wieder in Azure hochladen.

### <a name="edit-a-dashboard"></a>Bearbeiten eines Dashboards

Weitere Informationen finden Sie im Thema „Bearbeiten eines Dashboard über die Benutzeroberfläche“.

### <a name="shareunshare-a-dashboard"></a>Freigeben bzw. Aufheben der Freigabe eines Dashboards

Wenn Sie ein neues Dashboard definieren, ist es privat und nur für Ihr Konto sichtbar. Um anderen Benutzer die Ansicht des Dashboards zu ermöglichen, müssen Sie es freigeben. Sie müssen jedoch, wie bei jeder anderen Azure-Ressource auch, eine Ressourcengruppe angeben (oder eine vorhandenen Ressourcengruppe verwenden), in der freigegebene Dashboards gespeichert werden. Wenn Sie nicht über eine vorhandene Ressourcengruppe verfügen, erstellt Azure eine Ressourcengruppe „Dashboards“ in einem von Ihnen angegebenen Speicherort. Wenn Sie über eine Ressourcengruppe verfügen, können Sie diese verwenden, um die Dashboards zu speichern.

![Freigabe und Zugriffssteuerung 1](../images/7-share-dashboards-default.PNG)

Wenn Sie die Vorlage freigegeben haben, sehen Sie ein zweites Blatt: **Freigabe + Zugriffssteuerung**.

![Freigabe und Zugriffssteuerung 2](../images/7-share-dashboards-access-control.PNG)

Sie können dann auf **Benutzer verwalten** klicken, um die Benutzer anzugeben, die auf dieses Dashboard zugreifen dürfen.

### <a name="switching-to-a-shared-dashboard"></a>Wechsel zu einem freigegebenen Dashboard

Um zu einem freigegebenen Dashboard zu wechseln, klicken Sie auf die Liste der Dashboards und dann auf **Alle Dashboards durchsuchen**.

![Alle Dashboards durchsuchen](../images/7-browse-dashboards.PNG)

Sie sehen das Blatt „Alle Dashboards“, auf dem die Namen aller freigegebenen Dashboards angezeigt werden. Klicken Sie einfach auf ein Dashboard, um es auf das Azure-Portal anzuwenden.

![Freigegebene Dashboards](../images/7-select-shared-dashboard.png)

### <a name="display-a-dashboard-as-a-full-screen"></a>Anzeigen eines Dashboards im Vollbildmodus

Wenn Sie das Dashboard möglichst groß anzeigen möchten, klicken Sie auf die Schaltfläche **Vollbild**, um Ihr aktuelles Dashboard ohne Browsermenüs anzuzeigen. Falls sich Kacheln außerhalb der Bildschirmanzeige befinden, werden rechts und unten auf dem Bildschirm Schieberegler angezeigt.

Um den Vollbildmodus zu beenden, drücken Sie die ESC-Taste, oder klicken Sie am oberen Bildschirmrand neben dem Dashboardnamen auf **Vollbildmodus beenden**.

### <a name="clone-a-dashboard"></a>Klonen eines Dashboards

Die Funktion „Klonen eines Dashboards“ erstellt einfach eine direkte Kopie namens „Klon von (Dashboardname)“ und zeigt diese Kopie als aktuelles Dashboard an. Klonen ist auch eine einfache Möglichkeit, Dashboards zu erstellen, bevor sie freigegeben werden. Wenn Sie z.B. über ein Dashboard verfügen, das bereits fast Ihren Wünschen entspricht, klonen Sie es einfach, nehmen die notwendigen Änderungen vor und geben es dann frei.

### <a name="delete-a-dashboard"></a>Löschen eines Dashboards

Durch Löschen eines Dashboards wird dieses aus der Liste der verfügbaren Dashboards entfernt. Sie werden aufgefordert, zu bestätigen, dass Sie das Dashboard löschen möchten. Beachten Sie aber, dass es keine Möglichkeit gibt, ein gelöschtes Dashboard wiederherzustellen.

## <a name="edit-a-dashboard-through-the-user-interface"></a>Bearbeiten eines Dashboards über die Benutzeroberfläche

Sie können zwar ein Dashboard bearbeiten, indem Sie die JSON-Datei herunterladen, Werte in der Datei ändern und die Datei wieder in Azure hochladen. Allerdings ist diese Vorgehensweise für den Entwurf einer Benutzeroberfläche nicht besonders intuitiv. Um die grafische Benutzeroberfläche zum Konfigurieren Ihres aktuellen Dashboards zu verwenden, klicken Sie auf die Schaltfläche **Bearbeiten**, oder klicken Sie mit der rechten Maustaste auf das Dashboard und klicken dann auf **Bearbeiten**. Das Dashboard wechselt in den Bearbeitungsmodus.

![Dashboard bearbeiten](../images/7-edit-dashboard.PNG)

Auf der linken Seite wird der Kachelkatalog mit einer Reihe von Kacheln angezeigt. Sie können den Kachelkatalog nach folgenden Kriterien filtern:

* Allgemein
* Typ
* Suchen
* Ressourcengruppe
* Tag

![Kachelkatalog](../images/7-tile-gallery.png)

Sie können jede dieser Optionen nach Kategorie weiter eingrenzen, z.B. Azure Active Directory, Internet der Dinge, Microsoft Intune usw.

Um Kacheln hinzuzufügen, wählen Sie einfach aus der Liste links eine Kachel aus und ziehen sie per Drag & Drop diese auf den Arbeitsbereich. Sie können jede Kachel verschieben, ihre Größe ändern oder die darin angezeigten Daten ändern.

Der Arbeitsbereich ist im Bearbeitungsmodus in Quadrate unterteilt. Jede Kachel muss mindestens ein Quadrat belegen, und Kacheln werden an den nächstgelegenen Trennlinien ausgerichtet. Überlappende Kacheln werden aus dem Weg geschoben. Wenn Sie eine Kachel verkleinern, werden die umgebenden Kacheln wieder in die Nähe geschoben.

### <a name="change-tile-sizes"></a>Ändern der Kachelgrößen

Einige Kacheln verfügen über eine festgelegte Größe. Diese können Sie nur programmgesteuert bearbeiten. Kacheln, deren rechte untere Ecke grau angezeigt wird, können Sie jedoch bearbeiten, indem Sie die Eckmarke ziehen und ablegen.

![Kachel mit veränderbarer Größe](../images/7-resizable-tile.png)

Alternativ dazu können Sie auch mit der rechten Maustaste auf das Kontextmenü klicken und die gewünschte Größe angeben.

![Kachelgröße](../images/7-tile-size.png)

Um ein Dashboard zu erstellen, ziehen Sie einfach Kacheln aus dem Kachelkatalog auf den Arbeitsbereich und ordnen sie an.

### <a name="change-tile-settings"></a>Ändern der Kacheleinstellungen

Einige Kacheln weisen Einstellungen auf, die sich bearbeiten lassen. Wenn Sie z.B. die Kachel „Uhr“ auf den Arbeitsbereich ziehen, wird die Kachel **Uhr bearbeiten** geöffnet. Dort können Sie die Zeitzone sowie die Anzeige im 12- oder 24-Stunden-Format festlegen.

![Bearbeiten der Uhr](../images/7-edit-clock.png)

In multinationalen oder transkontinentalen Unternehmen können Sie weitere Uhren hinzufügen, die jeweils unterschiedliche Zeitzonen anzeigen.

### <a name="accepting-your-edits"></a>Akzeptieren der Änderungen

Wenn Sie die Kacheln nach Wunsch angeordnet haben, klicken Sie auf **Anpassung abgeschlossen**, oder klicken Sie mit der rechten Maustaste und klicken dann auf **Anpassung abgeschlossen**.

## <a name="edit-a-dashboard-by-changing-the-json-file"></a>Bearbeiten eines Dashboards durch Ändern der JSON-Datei

Sie können ein Dashboard auch durch Ändern der JSON-Datei bearbeiten. Diese Vorgehensweise bietet mehr Optionen für das Ändern von Einstellungen, aber Sie können die Änderungen erst sehen, nachdem Sie die Datei wieder in Azure hochgeladen haben.

![JSON-Einstellungen](../images/7-json-code.png)

Um im Beispiel oben die Größe der Kachel zu ändern, bearbeiten Sie die Variablen „colSpan“ und „rowSpan“, speichern die Datei und laden sie dann wieder in Azure hoch. Sie können die Datei auch an andere Benutzer verteilen.

## <a name="reset-a-dashboard"></a>Zurücksetzen eines Dashboards

Sie können jedes Dashboard auf den Standardstil zurücksetzen. Klicken Sie im Bearbeitungsmodus mit der rechten Maustaste, und wählen Sie **Auf Standardzustand zurücksetzen** aus. Sie werden in einem Dialogfeld aufgefordert, zu bestätigen, dass Sie dieses Dashboard zurücksetzen möchten.

## <a name="summary"></a>Zusammenfassung

Mit Dashboards lassen sich verschiedene Aspekte von Azure-Diensten flexibel über das Portal verwalten. Sie bieten zudem eine praktische Möglichkeit, den Zustand Ihrer Dienste zu überwachen. Da sie freigegeben werden können, tragen sie dazu bei, dass alle Mitglieder Ihres Teams die gleichen Daten anzeigen und sich über den Zustand Ihrer kritischen Komponenten informieren können.