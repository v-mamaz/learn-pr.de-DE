Ein erfolgreicher Betriebsprozess, bei dem die gewünschte Zuverlässigkeit erzielt und aufrechterhalten wird, ist gleichermaßen von dem Umgang mit den Computern als auch von dem Umgang mit den für diese Umgebung verantwortlichen Personen abhängig. Site Reliability Engineering erkennt diese Wahrheit auf mehrere Arten an, die für die zugehörige Methode entscheidend sind.

## <a name="toil"></a>Arbeitsaufwand

Zunächst steht das Konzept „Toil“, der Arbeitsaufwand, im Mittelpunkt. In einem SRE-Kontext bezieht sich Toil auf Betriebsvorgänge, die von einem Menschen ausgeführt werden und bestimmte Merkmale aufweisen. Toil weist keinen langfristigen Wert auf. Durch das Konzept wird der Dienst nicht in bedeutsamer Weise vorangebracht. Es ist häufig wiederkehrend und weitgehend manuell (auch wenn es automatisiert sein könnte). Da der Dienst bzw. die Systeme im Verlauf der Zeit größer werden, steigt voraussichtlich auch die Anzahl der Anforderungen für dieses System proportional an. Dadurch wird noch mehr manuelle Arbeit erforderlich.

Wenn das SRE-Team beispielsweise für einen Dienst wöchentlich etwas zurücksetzen muss, manuell neue Konten und Speicherplatz auf dem Datenträger bereitstellen muss oder den Dienst wiederholt manuell neu starten muss, wird diese betriebliche Belastung als Arbeitsaufwand bezeichnet. Durch das Ausführen dieser Aktionen konnte der Dienst langfristig oder dauerhaft nicht verbessert werden. Diese Aktionen müssen wahrscheinlich immer wieder wiederholt werden.

> [!NOTE]
> Auch wenn Sie Anforderungen wie diese in einer Art Ticketsystem verfolgen, wie es bei vielen Unternehmen üblich ist, gelten die Ausführung der Aktion und das Lösen eines Tickets nach wie vor als Arbeitsaufwand. Es ist lediglich gut nachverfolgter Arbeitsaufwand.

SREs mögen keinen Arbeitsaufwand. Ziel ihrer Arbeit ist es, Arbeit zu eliminieren, wann immer dies möglich und sinnvoll ist. Dies ist eine der Stellen, an der die Automatisierung in SRE ins Spiel kommt. Wenn diese Anforderungen automatisch bearbeitet werden können, kann das Team an lohnenswerteren und wirkungsvolleren Dingen arbeiten, statt die Warteschlange für Anforderungen abzuarbeiten.

Es sollte erwähnt werden, dass die Verwendung des Wortes „angemessen“ hier vergleichbar mit seiner Verwendung im Bereich der Zuverlässigkeit ist. Es gibt Fälle, in denen das Eliminieren von Arbeitsaufwand weniger Priorität als andere Aufgaben hat. Alles in allem ist das Beseitigen von Arbeitsaufwand aus einem Dienst jedoch der Schwerpunkt für einen SRE.

## <a name="project-work-vs-reactive-ops-work"></a>Projektarbeit im Vergleich zu reaktiver „Betriebsarbeit“

Damit sich ein SRE den erforderlichen Aufgaben zum Beseitigen von Arbeitsaufwand oder zum Verbessern der Zuverlässigkeit eines Systems widmen kann, muss seine Zeit so geplant werden, dass er nicht seine gesamte Arbeitszeit mit Erste Hilfe-Maßnahmen, dem Antworten auf Seiten oder schlichtweg dem Verarbeiten einer Warteschlange für Tickets verbringt. Er muss Zeit zum Schreiben von Code haben, welcher der Eliminierung von Arbeitsaufwand dient, sowie Zeit zum Erstellen von Self-Service-Automatisierung, damit keine Tickets erforderlich sind, und zum Erstellen von Projekten, die zur Effizienzsteigerung von Service und Mitarbeitern beitragen. In der Abbildung, die normalerweise genannt wird (aus dem ursprünglichen Google-Modell), beträgt die betriebliche Auslastung in einem Team nicht mehr als 50 %.

> [!NOTE]
> 50 % ist eine mehr oder weniger willkürlich Zahl, in der Praxis scheint dies jedoch häufig ein angemessenes Ziel zu sein.

Es gibt Momente im Leben eines SRE, in denen er sich nur mit Erste Hilfe-Maßnahmen befasst. Das darf jedoch kein Dauerzustand sein. Wenn die reaktive „Betriebsarbeit“ (vieles davon gilt als Arbeitsaufwand) eines Teams für einen längeren Zeitraum mehr als 50 % seiner Zeit beansprucht, ist dies der Vorbote für ein Burnout und mangelhafte Zuverlässigkeit. In diesem Fall können die zuvor besprochenen positiven Kreisläufe nicht bedient oder erstellt werden. SRE achtet gleichermaßen auf eine schlecht ausgeglichene Auslastung bei Bereitschaftsdiensten, da dies ebenfalls Potenzial für eine sehr negative Beeinträchtigung des Teams hat.

Nun, da wir einige der grundlegenden Methoden und Prinzipien von SRE kennengelernt haben, können wir uns mit den ersten Schritten beschäftigen.
