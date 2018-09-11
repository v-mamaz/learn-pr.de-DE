In dieser Übung erstellen und konfigurieren Sie ein benutzerdefiniertes Dashboard.

## <a name="create-a-new-dashboard"></a>Erstellen eines neuen Dashboards

1. Klicken Sie im Azure-Portal auf die Schaltfläche **Neues Dashboard**.

2. Ändern Sie im Feld **Mein Dashboard** den Namen zu **Kundendashboard**.

## <a name="add-and-configure-the-clock-tile"></a>Hinzufügen und Konfigurieren der Kachel für die Uhrzeit

1. Ziehen Sie im Kachelkatalog die Uhr auf den Arbeitsbereich. Legen Sie die Kachel oben rechts auf dem verfügbaren Platz ab.

2. Ändern Sie auf dem Blatt **Uhr bearbeiten** den Standort in **Pacific Time (USA und Kanada)**.

3. Klicken Sie unter **Uhrzeitformat** auf **24 Stunden**.

4. Klicken Sie auf **Fertig**.

5. Wiederholen Sie die vorherigen vier Schritte, wählen Sie aber **Eastern Time (USA und Kanada)** aus. Sie verfügen jetzt über zwei Uhren: eine mit der Uhrzeit für die Westküste der USA, eine für die Ostküste.

## <a name="resize-a-tile"></a>Ändern der Größe einer Kachel

1. Klicken Sie im Bereich **Kachelkatalog** auf **Alle Ressourcen**, und legen Sie die Kachel auf der linken Seite des neuen Dashboardarbeitsbereichs ab.

2. Klicken Sie auf die Kachel, klicken Sie mit der rechten Maustaste auf die Auslassungspunkte, und klicken Sie dann auf **6x6**.

3. Klicken Sie unten rechts auf der Kachel auf die graue Ecke, und ändern Sie die Größe der Kachel in folgende Werte: 3,5 vertikal und 6 horizontal. Beachten Sie, dass die Größe in 4x6 geändert wird, wenn Sie die Ecke loslassen.

4. Klicken Sie im Kachelkatalog auf die Kachel **Ressourcengruppen**, und ziehen Sie sie auf den Arbeitsbereich. Platzieren Sie die Kachel unter die Kachel **Alle Ressourcen**.

5. Klicken Sie im Kachelkatalog auf die Kachel **Service Health**, und ziehen Sie sie auf den Arbeitsbereich. Platzieren Sie die Kachel rechts neben die Kachel **Alle Ressourcen**.

6. Fügen Sie jetzt die folgenden Kacheln hinzu, und passen Sie ihre Größe an:

    * Hilfe + Support
    * Schnelle Aufgaben
    * Marketplace
    * Neuerungen

7. Wenn Sie diese Kacheln hinzugefügt haben, klicken Sie auf **Anpassung abgeschlossen**. Das Dashboard **Kundendashboard** sollte angezeigt werden.

## <a name="clone-a-dashboard"></a>Klonen eines Dashboards

Nun möchten Sie ähnliche Dashboards für weitere Kunden erstellen.

1. Klicken Sie auf die Schaltfläche **Klonen**.

2. Ändern Sie den Namen des Dashboards von **Klon von „Kundendashboard“** zu **Azure AD-Administratordashboard**.

3. Klicken Sie auf der Kachel **Ressourcengruppen** auf das Papierkorbsymbol, um diese Kachel zu löschen.

4. Fügen Sie folgende Kacheln aus dem Kachelkatalog hinzu:

    * Organisationsidentität
    * Benutzer und Gruppen
    * Zusammenfassung zur Benutzeraktivität
    * Willkommen beim Azure AD Admin Center

5. Ordnen Sie die Kacheln nach Bedarf an, und klicken Sie auf **Anpassung abgeschlossen**.

## <a name="share-a-dashboard"></a>Freigeben eines Dashboards

Als Nächstes machen Sie dieses Dashboard für andere Benutzer verfügbar. Führen Sie dazu die folgenden Schritte aus:

1. Stellen Sie sicher, dass das Azure Active Directory-Administratordashboard (Azure AD) ausgewählt ist, und klicken Sie dann auf **Freigeben**.

2. Stellen Sie auf dem Blatt **Freigabe und Zugriffssteuerung** sicher, dass **In der Ressourcengruppe „Dashboards“ veröffentlichen** ausgewählt ist.

3. Legen Sie einen für Ihre Geografie geeigneten **Standort** fest. Dieser Wert ist in der Regel standardmäßig auf das nächstgelegene Rechenzentrum festgelegt.

4. Klicken Sie auf **Veröffentlichen**, und schließen Sie dann das Blatt **Freigabe und Zugriffssteuerung**.

5. Klicken Sie auf **Azure AD-Administratordashboard**, und wählen Sie dann **Kundendashboard** aus.

    Beachten Sie, dass in **Alle Ressourcen** eine freigegebene Dashboardressource und in **Ressourcengruppen** eine Dashboardressourcengruppe angezeigt wird.

6. Wiederholen Sie die Schritte 1 bis 3, um das Kundendashboard freizugeben.

## <a name="edit-a-dashboardjson-file"></a>Bearbeiten einer dashboard.json-Datei

Führen Sie zum Herunterladen und Bearbeiten einer Dashboarddatei die folgenden Schritte aus:

1. Klicken Sie auf **Download**.

2. Öffnen Sie den Windows-Explorer, und navigieren Sie zu Ihrem Ordner „Downloads“.

3. Suchen Sie die Datei *Customer Dashboard.json*, und doppelklicken Sie darauf.

4. Suchen Sie im Code-Editor nach dem Text *ClockPart*.

5. Ändern Sie beim ersten Vorkommen von „ClockPart“ den vorherigen **rowSpan**-Wert in 1.

6. Ändern Sie auch beim zweiten Vorkommen von „ClockPart“ den vorherigen **rowSpan**-Wert in 1.

7. Ändern Sie beim zweiten Vorkommen von „ClockPart“ den Y-Wert von 2 in 1.

8. Speichern Sie die Datei *Customer Dashboard.json*, und schließen Sie den Code-Editor.

9. Klicken Sie auf dem Azure-Dashboard auf **Hochladen**.

10. Navigieren Sie im Dialogfeld **Öffnen** zum Ordner „Downloads“, und doppelklicken Sie auf *Customer Dashboard.json*.

    Beachten Sie, dass die Größe der Uhren auf die Höhe einer Zeile geändert und die untere Uhr eine Zeile nach oben verschoben wurde.

## <a name="select-a-shared-dashboard"></a>Auswählen eines freigegebenen Dashboards

Sie haben festgestellt, dass Ihnen die kleineren Uhren nicht gefallen und Sie zur vorherigen freigegebenen Version des Kundendashboards zurückkehren möchten. Hierfür können Sie entweder die Datei bearbeiten und erneut hochladen oder auf die freigegebene Version zugreifen. Führen Sie die folgenden Schritte aus:

1. Klicken Sie neben **Kundendashboard** auf den nach unten weisenden Pfeil.

2. Klicken Sie auf **Alle Dashboards durchsuchen**.

3. Wählen Sie auf dem Blatt **Alle Dashboards** unter **TYP** die Option **Freigegebene Dashboards** aus.

4. Klicken Sie auf **Kundendashboard**.

5. Schließen Sie das Blatt **Alle Dashboards**.

    Beachten Sie, dass die Uhren wieder ihre ursprüngliche Größe aufweisen.

## <a name="switch-to-full-screen"></a>Wechseln zum Vollbildmodus

1. Klicken Sie neben **Kundendashboard** auf den nach unten weisenden Pfeil. 

    Beachten Sie, dass es ein weiteres Kundendashboard gibt, ohne das Freigabesymbol daneben. Klicken Sie auf diese Version des Kundendashboards, und die Uhren sind wieder klein.

2. Wechseln Sie zurück zum freigegebenen Kundendashboard.

3. Klicken Sie auf die Schaltfläche **Vollbild**. 

    Beachten Sie, dass keine Browsermenüs und Leisten mehr angezeigt werden.

4. Klicken Sie auf **Vollbildmodus beenden**, um zum normalen Bildschirm zurückzukehren.

## <a name="unshare-a-dashboard"></a>Aufheben der Freigabe eines Dashboards

Wenn Sie verhindern möchten, dass ein bestimmtes freigegebenes Dashboard ausgewählt werden kann, können Sie die Freigabe aufheben. Um die Freigabe eines Dashboards aufzuheben, führen Sie die folgenden Schritte aus:

1. Klicken Sie auf die Schaltfläche **Freigabe aufheben**. Das Blatt **Freigabe + Zugriffssteuerung** wird angezeigt.

2. Klicken Sie auf die Schaltfläche **Veröffentlichung aufheben**.

3. Klicken Sie in der Bestätigungsmeldung auf **OK**.

4. Klicken Sie neben **Kundendashboard** auf den nach unten weisenden Pfeil.

5. Klicken Sie auf **Alle Dashboards durchsuchen**.

6. Wählen Sie auf dem Blatt **Alle Dashboards** unter **TYP** die Option **Freigegebene Dashboards** aus.

    Beachten Sie, dass das **Kundendashboard** nicht mehr in der Liste der verfügbaren Dashboards angezeigt wird.

7. Schließen Sie das Blatt **Alle Dashboards**.

## <a name="delete-a-dashboard"></a>Löschen eines Dashboards

1. Stellen Sie sicher, dass das Dashboard **Azure AD-Administrator** ausgewählt ist.

2. Klicken Sie auf die Schaltfläche **Löschen**.

3. Aktivieren Sie im Meldungsfeld **Bestätigung** das Kontrollkästchen, um zu bestätigen, dass dieses Dashboard nicht mehr angezeigt wird, und klicken Sie dann auf **OK**.

## <a name="reset-a-dashboard"></a>Zurücksetzen eines Dashboards

1. Stellen Sie sicher, dass das **Kundendashboard** ausgewählt ist.

2. Klicken Sie auf **Edit**.

3. Klicken Sie mit der rechten Maustaste auf den Arbeitsbereich, und klicken Sie auf **Standardzustand wiederherstellen**.

4. Klicken Sie im Meldungsfeld **Dashboard auf Standardzustand zurücksetzen** auf **Ja**.

    Beachten Sie, dass das Kundendashboard wieder auf die Standardkacheln zurückgesetzt wurde.

5. Klicken Sie auf **Anpassung abgeschlossen**.

6. Klicken Sie rechts oben im Portal auf Ihren Namen.

7. Klicken Sie auf **Abmelden**.

8. Schließen Sie Ihren Browser.

## <a name="summary"></a>Zusammenfassung

Sie haben Dashboards erstellt, bearbeitet, freigegeben und in Form von **JSON**-Dateien geändert. Sie haben die Freigabe aufgehoben und die Dashboards letztendlich auf den Standardzustand zurückgesetzt. Sie wissen jetzt, dass Dashboards leistungsfähige Tools sein können und wie Sie diese verwenden können, um effiziente Schnittstellen für verschiedene Rollen in einer Organisation zu erstellen.

