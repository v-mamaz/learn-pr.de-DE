Nachdem Sie Ihre Daten in mehreren Regionen repliziert haben, können Sie die automatisierten Failoverlösungen nutzen, die von Azure Cosmos DB bereitgestellt werden. Automatisierte Failover sind ein Feature, das genutzt wird, wenn eine Katastrophe oder ein anderer Notfall eintritt und eine Ihrer Lese- oder Schreibregionen in den Offlinezustand versetzt wird. Anforderungen werden dann von der Offlineregion an die nächste Region der Prioritätsreihenfolge umgeleitet. 

Für Ihre Onlinetextilhandel-Website, die Sie gerade in den Regionen „USA, Osten“, „USA, Westen“ und „Vereinigtes Königreich, Westen“ repliziert haben, können Sie die Priorität wie folgt festlegen: Wenn „USA, Osten“ in den Offlinezustand versetzt wird, können Sie Lesevorgänge an „USA, Westen“ umleiten, anstatt an „Vereinigtes Königreich, Westen“, um die Latenz zu verringern. 

In dieser Einheit wird beschrieben, wie das Failover funktioniert, und es wird die Priorität für die Regionen festgelegt, in denen die Daten Ihres Unternehmens repliziert wurden.

## <a name="failover-basics"></a>Failovergrundlagen

Im seltenen Fall des Ausfalls einer Azure-Region oder eines Rechenzentrums löst Azure Cosmos DB automatisch ein Failover aller Azure Cosmos DB-Konten aus, die sich in der betroffenen Region befinden.

**Was passiert beim Ausfall einer Leseregion?**

Azure Cosmos DB-Konten mit einer Leseregion in einer der betroffenen Regionen werden automatisch von ihrer Schreibregion getrennt und als offline gekennzeichnet. Die Cosmos DB-SDKs implementieren ein Protokoll für die Regionsermittlung, mit dessen Hilfe automatisch erkannt werden kann, wenn eine Region verfügbar ist, und Leseaufrufe an die nächste verfügbar Region in der Liste der bevorzugten Regionen umgeleitet werden können. Wenn keine der Regionen in der Liste verfügbar ist, wird für die Aufrufe automatisch ein Fallback zur aktuellen Schreibregion durchgeführt. Zur Verarbeitung regionaler Failover sind keine Änderungen an Ihrem Anwendungscode erforderlich. Während des gesamten Prozesses werden die Konsistenzgarantien von Azure Cosmos DB weiterhin erfüllt.

Sobald die betroffene Region nach dem Ausfall wiederhergestellt wurde, werden alle betroffenen Azure Cosmos DB-Konten in der Region vom Dienst automatisch wiederhergestellt. Azure Cosmos DB-Konten, die über eine Leseregion in der betroffenen Region verfügen, werden automatisch mit der aktuellen Schreibregion synchronisiert und wieder online geschaltet. Die Azure Cosmos DB-SDKs ermitteln die Verfügbarkeit der neuen Region und bewerten anhand der von der Anwendung konfigurierten Liste mit den bevorzugten Regionen, ob die Region als aktuelle Leseregion ausgewählt werden soll. Nachfolgende Lesevorgänge werden an die wiederhergestellte Region weitergeleitet, ohne dass Änderungen an Ihrem Anwendungscode erforderlich sind.

**Was passiert beim Ausfall einer Schreibregion?**

Wenn die betroffene Region die aktuelle Schreibregion ist und für das Azure Cosmos DB-Konto die Funktion „Automatisches Failover“ aktiviert ist, wird die Region automatisch als offline gekennzeichnet. Danach wird eine andere Region zur Schreibregion für das betroffene Cosmos DB-Konto hochgestuft.

Während eines automatischen Failovers wählt Azure Cosmos DB anhand der angegebenen Prioritätsreihenfolge automatisch die nächste Schreibregion für ein bestimmtes Azure Cosmos DB-Konto aus. Anwendungen können die Eigenschaft „WriteEndpoint“ der Klasse „DocumentClient“ verwenden, um eine Änderung der Schreibregion zu ermitteln.

Sobald die betroffene Region nach dem Ausfall wiederhergestellt wurde, werden alle betroffenen Cosmos DB-Konten in der Region vom Dienst automatisch wiederhergestellt.

Als Nächstes ändern wir die Leseregion für Ihre Datenbank.

## <a name="set-read-region-priorities"></a>Festlegen von Prioritäten für die Leseregion

1. Klicken Sie im Azure-Portal auf dem Bildschirm **Daten global replizieren** auf **Automatisches Failover**. Das automatische Failover wird nur aktiviert, wenn die Datenbank bereits in mehr als eine Region repliziert wurde.
2. Ändern Sie auf dem Bildschirm **Automatisches Failover** die Option **Automatisches Failover aktivieren** in **EIN**.
3. Klicken Sie im Abschnitt **Leseregionen** auf den linken Teil der Zeile **USA, Osten**, und ziehen Sie ihn an die oberste Position.
4. Klicken Sie auf den linken Teil der Zeile **Japan, Osten**, und ziehen Sie ihn an die zweite Position.
5. Klicken Sie auf **OK**.

    ![Ändern von Leseregionen im Portal](../media/4-change-priorities/change-read-priorities.gif)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit wurde beschrieben, was automatische Failover sind, wie Sie diese als Schutz vor unvorhergesehenen Ausfällen verwenden können und wie Sie die Prioritäten der Leseregion ändern.