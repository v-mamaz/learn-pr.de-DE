Bevor wir einen Teil der SRE-Methoden untersuchen, sollten wir einige der Konzepte, die wir in der vorherigen Einheit kennengelernt haben, im Kontext betrachten. In dieser kurzen Einheit erfahren Sie etwas über die Geschichte von SRE und darüber, wie SRE mit anderen Betriebsmethoden in Zusammenhang steht, die Ihnen vertraut sind. Dadurch können wir später größere Erfolge erzielen, da diese Methoden im Kontext mehr Sinn ergeben werden. Darüber hinaus haben Sie direkt eine Antwort parat, wenn Ihre Freunde fragen: „Wie unterscheidet sich SRE von...?“

## <a name="history"></a>Geschichte

Die stark verkürzte Geschichte von SRE beginnt bei dessen Ursprüngen: bei Google im Jahr 2003. Ben Treynor, heute Treynor Sloss, übernahm die Leitung des „Produktionsteams“ von Google (damals bestand das Team nur aus sieben Softwareentwicklern) und entwickelte eine Idee, die er bekanntermaßen wie folgt beschrieb: „Was passiert, wenn Sie einen Softwareentwickler darum bitten, eine Betriebsfunktion zu entwickeln?“ Es ist hilfreich für das Verständnis, mehr über die Geschichte von SRE zu erfahren, da erläutert wird, weshalb SRE sich für Mitarbeiter, die für den Betrieb zuständig sind, sehr nach „Softwareentwicklung“ anfühlt, wenn ihnen SRE zum ersten Mal begegnet. Aus diesem Bereich wurden Werte und grundlegende Tools übernommen, wie z.B. die Priorität der Codierung und Quellcodeverwaltungssysteme. Die erste und die aktuelle Implementierung von Google SRE sind in den zugehörigen zwei Büchern, die von O'Reilly veröffentlicht wurden, umfassend dokumentiert (siehe die Einheit „Erste Schritte“).

Als Mitarbeiter von Google das Unternehmen verließen (und Mitarbeiter des Unternehmens häufiger in der Öffentlichkeit über ihre Methoden sprachen), begann die Verbreitung von SRE auf weitere Unternehmen in der Branche. Als sich SRE auf neue Unternehmen verbreitete, übernahmen diese Unternehmen die SRE-Prinzipien und -Methoden und passten sie so an, dass sie ihrer lokalen Kultur entsprachen. Durch diesen Erweiterungsprozess entstanden in dem Bereich viele unterschiedliche Implementierungen von SRE. 

## <a name="devops-and-sre"></a>DevOps und SRE

Die gesamte Branche musste sich den gleichen Herausforderungen rund um Skalierung, Entwicklungsgeschwindigkeit im Vergleich zu Betriebsstabilität und anderen Problemen bei der Softwarebereitstellung stellen, die die Site Reliability Engineering-Bewegung hervorbrachte. Durch parallele Anstrengungen zur Behebung dieser Probleme außerhalb von Google (und einigen größeren Unternehmen zu diesem Zeitpunkt) entstand DevOps. 

Viele nützliche Informationen zu DevOps finden Sie unter [https://docs.microsoft.com/azure/devops/learn/](https://docs.microsoft.com/azure/devops/learn/).

> [!NOTE]
> Bitte beachten Sie, dass DevOps und SRE zwei unterschiedliche parallele Ansätze zur Begegnung der gleichen Herausforderungen sind. SRE ist nicht der nächste Evolutionsschritt nach DevOps. SRE wurde nicht mit dem Ziel erstellt, „die Zukunft von DevOps“ zu sein.

Die Frage nach den Unterschieden von SRE und DevOps sorgt in dem Bereich nach wie vor für beträchtliche Diskussionen. Es gibt einige Unterschiede, über die ein breiter Konsens herrscht, z.B. folgende:

- SRE ist ein Ansatz, bei dem die Zuverlässigkeit im Fokus steht, während DevOps eine kulturelle Bewegung ist, die aus dem Drang entstanden ist, die Silos aufzuschlüsseln, die verschiedenen Unternehmen in der Regel für die Entwicklung und den Betrieb zugeordnet sind.
- SRE kann der Name einer Rolle sein, wie z.B. in der Aussage „Ich bin ein Site Reliability Engineer (SRE)“, DevOps nicht. Genau genommen verdient niemand als „DevOps“sein Geld.
- SRE ist tendenziell verbindlicher, DevOps ist ganz bewusst nicht so. Am ehesten geht es diesbezüglich um die nahezu weltweite Anwendung von Continuous Integration/Continuous Delivery- und Agile-Prinzipien.

Die beiden Betriebsmethoden, DevOps und SRE, teilen eine gemeinsame Leidenschaft für die Überwachung/Beobachtbarkeit und die Automatisierung. Daher ist es häufig einfacher, SRE-Prinzipien und -Methoden in ein Unternehmen zu importieren, das bereits eine DevOps-Methode verwendet. Dieser Prozess muss sorgfältig und bewusst durchgeführt werden. Zudem kann und sollte SRE schrittweise implementiert werden. Ein plötzlicher Wechsel ist nicht erforderlich.

> [!WARNING]
> Die Implementierungsstrategie, bei der einfach die Titel von Mitarbeitern eines Unternehmens ausgetauscht werden, ist fast nie erfolgreich. Dies führt nicht zu den Vorteilen, die SRE zu bieten hat. Einige bessere Vorschläge können Sie dem Abschnitt „Erste Schritte“ dieser Einheit entnehmen.

## <a name="conclusion"></a>Zusammenfassung

Ziel dieser kurzen Einheit war es, Ihnen etwas Kontext zu SRE und DevOps zu vermitteln. SRE und DevOps sind angrenzende Denkmodelle für Betriebe und wurden in dieser Hinsicht bestens durchdacht. 

Nun, da wir einen kurzen Blick auf den Hintergrund von SRE geworfen haben, können wir mit einigen der wichtigsten Prinzipien fortfahren.
