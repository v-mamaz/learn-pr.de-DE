Stellen Sie sich vor, dass Sie eine Warnung vom Sicherheitsadministrator Ihres Unternehmens erhalten, dass es sich bei eine potenziellen sicherheitsverletzung in Ihrem Netzwerk erkannt wurde. Zum Schutz Ihrer Datenbankserver aufzurüsten möchten hinzufügen und zum Überwachen.

In dieser Einheit betrachten wir wie die Überwachung für eine Datenbank konfiguriert ist, und wie diese Überwachungen verwendet.

## <a name="configure-auditing"></a>Konfigurieren der Überwachung

Aktivieren Sie Überwachung der Vorgänge, die auftreten, für die Datenbank zur späteren Untersuchung speichern, oder haben sie automatisierte Tools analysieren. Überwachung wird auch verwendet, für die Verwaltung von Compliance- oder verstehen, wie Ihre Datenbank verwendet wird. Überwachung ist auch erforderlich, wenn Sie die bedrohungserkennung von Azure für Ihre Azure SQL-Datenbank verwenden möchten.

Um Prüfungen der Datenbank zu speichern, wird ein Azure Storage-Konto zum Speichern des Überwachungsverlaufs benötigt.

Wir sehen uns die Schritte, die Sie zum Einrichten der Überwachung auf Ihrem System ausführen.

1. Wählen Sie die Azure SQL-Server im Portal.

2. Navigieren Sie zu dem Element "Überwachung" in den linken Konfigurationsoptionen. In der Kategorie "Sicherheit" finden Sie es.

3. Überwachung ist standardmäßig deaktiviert. Tippen Sie auf die Schaltfläche "Weiter", um sie auf dem Datenbankserver zu aktivieren.

4. Nachdem die Schaltfläche "Weiter" ausgewählt ist, wählen Sie die Schaltfläche "konfigurieren", um das Speicherkonto zu definieren. Sie können ein vorhandenes Speicherkonto auswählen oder erstellen ein neues Speicherkonto zum Speichern Ihrer Überwachungen. Das Speicherkonto muss für das Verwenden der gleichen Region wie Ihr Server konfiguriert werden.

5. Klicken Sie auf die Schaltfläche "Speichern" in der Symbolleiste, um die Änderungen zu speichern.

Diese Aktionen werden die Überwachungen auf Datenbankebene Server konfigurieren. Sie können auch konfigurieren, die Überwachung auf Datenbankebene ausgeführt.

Sie müssen nun die Advanced Threat Protection konfigurieren.

## <a name="configure-advanced-threat-protection"></a>Konfigurieren von erweiterten Schutz vor Bedrohungen

Das Advanced Threat Protection-System analysiert die Überwachungsprotokolle nach möglichen Problemen und Bedrohungen für Ihre Datenbank gesucht werden soll.

Betrachten Sie die Schritte, die Sie ergreifen, um die Konfiguration von Advanced Threat Protection auf einem System aus.

1. Wählen Sie die Azure SQL-Server im Portal.

2. Navigieren Sie zu dem Advanced Threat Protection-Element in der linken Konfigurationsoptionen. Sie finden sie in der Kategorie "Sicherheit".

3. Klicken Sie auf die Schaltfläche "Aktivieren Sie Advanced Threat Protection auf dem Server".

4. Ändern des Advanced Threat Protection-Schalters auf ON.

5. Wählen Sie die Ansicht Advanced Threat Protection-servereinstellungen, um die Optionen für das Datenbanksystem anzuzeigen.

6. Als Nächstes definieren Sie, in denen Benachrichtigung, die als eine Liste von durch Semikola e-Mails übermittelt werden e-Mail-Adressen getrennt. Wählen Sie die e-Mail-Dienst und Co-Administratoren die Bedrohungen für die Dienstadministratoren gesendet.

7. Geben Sie nun das Abonnement und Speicherkonto, das für die Bedrohungen auf dem System analysiert werden sollen. Dies sollte das Abonnement und Azure-Speicher sein Konto für die Überwachung konfiguriert. Sie müssen auch die Anzahl der Tage zum Beibehalten des Überwachungsverlaufs festlegen. Festlegen des Werts auf 0 (null) bedeutet, dass die Überwachung für immer gespeichert wird.

Wählen Sie dann den speicherzugriffsschlüssel für die Überwachungen die Verbindung ein. Nachdem Sie die Optionen konfiguriert haben, klicken Sie auf OK.

Legen Sie schließlich die Bedrohungserkennung Typen an. Die bevorzugte Option ist.

Alle steht für die folgenden Werte:

- SQL Injection-Berichten, in denen Angriffen durch Einschleusung von SQL-Befehlen aufgetreten sind.
- SQL Injection Sicherheitsrisiko Berichten, in denen die Möglichkeit, eine SQL-Einschleusung wahrscheinlich ist. und
- Ungewöhnliche Clientanmeldung untersucht, Anmeldungen, die unregelmäßig und möglicherweise Anlass zur Sorge, z. B. einem potenziellen Angreifer Zugriff erlangen.

Klicken Sie auf die **speichern** Schaltfläche, um die Änderungen zu übernehmen.

Sie erhalten e-Mail-Benachrichtigungen, wie Sie Sicherheitsrisiken erkannt werden. Die e-Mail-Adresse wird beschrieben, was passiert ist und welche Aktionen durchgeführt werden.

## <a name="enable-advanced-threat-protection"></a>Erweiterter Schutz vor Bedrohungen

Nachdem Sie den Server für Advanced Threat Protection konfiguriert haben, aktivieren Sie die Option für jede einzelne Datenbank. Navigieren Sie zu den einzelnen Datenbanken aus, und Aktivieren von Advanced Threat Protection durch Auswahl von "Aktivieren Sie Advanced Threat Protection auf dem Server".

Sie können regelmäßige Überprüfungen aktivieren, die das System alle sieben Tage überprüft werden, um Sicherheitsrisiken zu suchen.

Wenn Sie die regelmäßige wiederkehrenden Scan-Option auswählen, wird eine Überprüfung durchgeführt, sofort nach dem Speichern der Einstellungen.

Klicken Sie auf die Schaltfläche **Speichern** , um die Änderungen zu speichern.

Sie erhalten eine e-Mail-Benachrichtigung darüber benachrichtigt werden alle eventuell vorhandenen Sicherheitsrisiken. Stellen Sie sicher, dass die Bedrohung sofort zu beheben. Sie erhalten eine Benachrichtigung für eine Reihe von Ursachen haben:

![Eine Warnung zu einem Beispiel Benachrichtigung von Advanced Threat Protection](../media-draft/5-email-with-warning.png)

Wenn Sie die Advanced Threat Protection-Option auswählen, wenn Advanced Threat Protection ausgeführt wird, sehen Sie eine Liste der Probleme angezeigt. Datenermittlung & Klassifizierungsprobleme auftreten, z. B. vertrauliche Daten, die eine Liste mit Sicherheitsrisiken auf dem System, und klicken Sie auf potenzielle Bedrohungen, kann dieser Liste enthalten.

![Datenermittlung und -klassifizierung](../media-draft/5-data-discovery-and-classification.png)

Die Datenermittlung und-Klassifizierung Bereich zeigt die Spalten in Tabellen, die geschützt werden müssen. Einige Spalten möglicherweise vertraulichen Informationen, oder in unterschiedlichen Ländern oder Regionen klassifiziert betrachtet werden.

Klicken Sie auf der Datenermittlung und-Klassifizierung-Bereich.

Ggf. alle Spalten-Schutz konfiguriert haben, wird eine Meldung angezeigt werden. Diese Meldung wird in Form von *"Wir haben 10 Spalten mit klassifizierungsempfehlungen gefunden"*. Sie können auf den Text der Empfehlungen anzeigen klicken.

Wählen Sie die Spalten, die Sie durch Klicken auf das Häkchen neben der Spalte klassifizieren möchten, oder aktivieren Sie das Kontrollkästchen auf der linken Seite des schemaheaders. Wählen Sie die Empfehlungen zur Klassifizierung anzuwendenden Optionen Empfehlungen annehmen ausgewählt.

Sie müssen die Spalten bearbeiten, und definieren Sie dann den Informationstyp und die vertraulichkeitsbezeichnung für die Datenbank. Klicken Sie auf die Schaltfläche "Speichern", um die Änderungen zu speichern.

Nachdem Sie die Empfehlungen erfolgreich verwaltet haben, sollten keine aktiven Empfehlungen aufgeführt werden.

![Sicherheitsanfälligkeit Bewertungsdashboard](../media-draft/5-vulnerability-assessment-dashboard.png)

Die Sicherheitsrisikobewertung werden Konfigurationsprobleme in Ihrer Datenbank und das Risiko aufgelistet. Z. B. in der obigen Abbildung sehen Sie, dass die Firewallregeln auf Serverebene muss eingerichtet werden.

Klicken Sie im Bereich zur Sicherheitsrisikobewertung, um eine vollständige Liste der Sicherheitsrisiken zu überprüfen. Klicken Sie auf jeder einzelnen Schwachstelle, dort zu werden.

Auf dieser Seite sehen Sie die Details wie z. B. die Risikostufe, welche Datenbank, eine Beschreibung der Sicherheitsanfälligkeit und die empfohlenen korrekturmaßnahmen zum Beheben des Problems angewendet. Wenden Sie die Lösungen, um das oder die Probleme zu beheben. Stellen Sie sicher, dass alle Sicherheitsprobleme zu beheben.

![Bedrohungserkennung](../media-draft/5-threat-detection-dashboard.png)

Die letzte Diagramm zeigt eine Liste der Erkennung von Bedrohungen. Z. B. in dieser Liste sehen eine Anzahl von möglichen SQL Injection-Angriffe Sie.

Wie die Sicherheitsrisiken klicken Sie auf im Bereich Bedrohungserkennung, navigieren zu der Liste der Einträge zu sehen, was die Bedrohung ist. Klicken Sie dann beheben Sie das Problem, indem Sie die Empfehlungen befolgen.  Informationen zu Problemen wie z. B. die SQL-Injection-Warnungen müssen Sie möglicherweise sehen Sie sich die Abfrage aus, und arbeiten sich rückwärts zu, in dem diese Abfrage im Code ausgeführt wird. Sobald eines gefunden wurde, müssen Sie den Code umzuschreiben, damit es ohne mehr das Problem hat.
