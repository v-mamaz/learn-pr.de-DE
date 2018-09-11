Angenommen, Sie arbeiten bei einem Unternehmen im Gesundheitswesen. Sie haben ältere Systeme, branchenspezifische Systeme, und Zukunftspläne für neue Systeme. Sie haben gehört, dass der Einsatz von Cloud Computing Vorteile bringt. Wie wählen Sie das beste Bereitstellungsmodell für verschiedene Lösungen aus: öffentliche Cloud, private Cloud oder Hybrid Cloud?

## <a name="what-is-cloud-computing"></a>Was ist Cloud Computing?

Cloud Computing ist die bedarfsgesteuerte Bereitstellung von Diensten und Anwendungen über das Internet. Server, Anwendungen, Daten und andere Ressourcen werden als Dienst bereitgestellt. 

Für den Benutzer werden die Details der Dienste abstrahiert. Sie können Computingressourcen schnell bereitstellen und den Dienst mit minimalem Verwaltungsaufwand nutzen. Sie sollten sich Cloud Computing nicht als Rechenzentrum vorstellen, das über das Internet verfügbar ist. Beim Cloud Computing kommen Virtualisierung, handelsübliche Hardware und automatisierte Prozesse zum Einsatz, um den Kunden ein Self-Service-Benutzererlebnis zu bieten, das dem eines öffentlichen Versorgungsunternehmens ähnlich ist.

Es gibt drei Bereitstellungsmodelle für Cloud Computing: öffentliche Cloud, private Cloud und Hybrid Cloud. Die folgende Abbildung stellt eine Übersicht über diese Bereitstellungsmodelle dar.

![Eine Abbildung, die eine allgemeine Übersicht über Cloudbereitstellungsmodelle darstellt.](../media/2-cloud-deployment.png)

!!! Video TC-008-Platzhalter !!! 

> [!VIDEO https://channel9.msdn.com/Series/History/The-History-of-Microsoft-1995/player]

## <a name="public-cloud"></a>Öffentliche Cloud

Öffentliche Clouds sind die gängigste Methode der Bereitstellung von Cloud Computing. Dienste werden über das öffentliche Internet angeboten und sind für alle Benutzer verfügbar, die sie erwerben möchten. Besitzer und Betreiber der Cloudressourcen wie Server und Speicher sind Drittanbieter von Clouddiensten, die diese über das Internet bereitstellen. Dienste werden entweder kostenlos angeboten oder nach Bedarf verkauft, sodass Kunden nur für die Nutzung von CPU-Zyklen, Speicher und Bandbreite zahlen müssen, die sie verwenden. Microsoft Azure ist ein Beispiel einer öffentlichen Cloud. 

Angenommen Sie, Ihr Unternehmen im Gesundheitswesen benötigt eine Registrierungswebsite. Die Website muss zu verschiedenen Spitzenzeiten bei Registrierungen im Verlauf des Jahres skalierbar und reaktionsschnell sein. Ihre Kunden greifen auf die Website von globalen Standorten aus zu. Sie können die öffentliche Cloud verwenden, um die Website zum Erfüllen des Bedarfs zu Spitzenzeiten bei Registrierungen automatisch zentral hoch zu skalieren. Wenn der Datenverkehr auf der Website niedrig ist, können Sie die Website zentral herunterskalieren, um Kosten zu sparen. Ihre Website ist bei Bedarfsspitzen reaktionsbereit, und Sie zahlen nur bei entsprechendem Bedarf für mehr Ressourcen. Sie können Ihre Website auch in mehreren geografischen Regionen bereitstellen, um Zuverlässigkeit und Reaktionsfähigkeit zu erhöhen.

Während der Entwicklung Ihrer Website möchten Entwickler mehrere Entwicklungsumgebungen erstellen, um ihren Entwicklungsprozess zu beschleunigen. Entwickler können die öffentliche Cloud nutzen, um schnell virtuelle Computer für Sandkastenumgebungen bereitzustellen und eine Lösung zu entwickeln. Wenn die Entwickler eine Umgebung nicht mehr benötigen, können sie sie löschen.

### <a name="why-public-cloud"></a>Gründe für die öffentliche Cloud

Öffentliche Clouds können schneller als lokale Infrastrukturen und mit einer nahezu beliebig skalierbaren Plattform bereitgestellt werden. Jeder Mitarbeiter eines Unternehmens kann im Büro oder in der Filiale die gleiche Anwendung mit dem Gerät seiner Wahl nutzen, solange er auf das Internet zugreifen kann. 

Szenarios, in denen sich die öffentliche Cloud eignet:

- **Bedarfsgesteuerte oder abonnementgestützte Dienstnutzung:** Beim bedarfsgesteuerten oder Abonnementmodell zahlen Sie nur für den Anteil an CPU, Speicher und anderen Ressourcen, den Sie nutzen oder reservieren.
- **Keine direkten Investitionen in Hardware:** Sie müssen keine lokale Hardware- und Anwendungsinfrastruktur kaufen, verwalten und warten. Der Cloud-Dienstanbieter ist für die gesamte Verwaltung und Wartung des Systems verantwortlich. 
- **Automatisierung:** Sie können Infrastrukturressourcen über ein Webportal, Skripts oder automatisch bereitstellen. 
- **Geografische Verteilung:** Halten Sie Daten dort vor, wo sie gebraucht werden, ohne viele eigene Rechenzentren zu betreiben.
- **Reduzierte Hardwarewartung:** Der Dienstanbieter ist für die Hardwarewartung verantwortlich.

## <a name="private-cloud"></a>Private Cloud

Eine private Cloud besteht aus IT-Ressourcen, die ausschließlich von ausgewählten Benutzern eines Unternehmens oder einer Organisation genutzt werden. Sie kann physisch im lokalen Rechenzentrum Ihres Unternehmens oder bei einem Drittanbieter gehostet werden. Die Begriff „Private Cloud“ sollte nicht als Umfirmierung herkömmlicher lokaler Rechenzentren betrachtet werden. Eine private Cloud nutzt lokale Infrastruktur und Dienste, um ähnliche Vorteile wie die öffentliche Cloud zu bieten. Sie nutzt eine Abstraktionsplattform, um *cloudähnliche Dienste* wie Kubernetes-Cluster oder eine komplette Cloudumgebung wie Azure Stack bereitzustellen. Die Organisation ist für Erwerb, Konfiguration und Wartung der Hardware verantwortlich. Die Kommunikation zwischen den Systemen erfolgt in der Regel über die Netzwerkinfrastruktur, die das Unternehmen besitzt und verwaltet. Beispielsweise ein privates internes Netzwerk oder eine dedizierte Glasfaserverbindung zwischen Gebäuden.

Angenommen, Sie arbeiten in einem Unternehmen im Gesundheitswesen und haben eine Anwendung, die in einem Ihrer Rechenzentren im Einsatz ist. Die Betriebsumgebung kann nicht in der öffentlichen Cloud repliziert werden. Es gibt eine neue Anforderung, auf Daten in einem anderen Ihrer Rechenzentren zuzugreifen. Die Datenbank mit den Daten muss zwecks Einhaltung gesetzlicher Vorschriften am anderen Standort verbleiben. Dies ist ein Szenario für eine private Cloud. Sie verfügen über zwei Rechenzentren im Besitz Ihrer Organisation. Sie können ein VPN in der öffentlichen Cloud über das Internet verwenden, um eine Verbindung mit den Rechenzentren herzustellen. Dieses Szenario würde jedoch als private Cloud betrachtet werden, da die Lösung für die Organisation privat ist.

### <a name="why-private-cloud"></a>Gründe für eine private Cloud

Eine private Cloud kann einer Organisation mehr Flexibilität bieten. Ihr Unternehmen kann seine Cloudumgebung an spezifische Geschäftsanforderungen anpassen. Da Ressourcen nicht mit anderen gemeinsam genutzt werden, ist ein hohes Maß an Kontrolle und Sicherheit möglich. Darüber hinaus bieten private Clouds ein gewisses Maß an Skalierbarkeit und Effizienz.

Szenarios, in denen sich die private Cloud eignet:

- **Bereits vorhandene Umgebung:** Eine bestehende Betriebsumgebung, die nicht in der öffentlichen Cloud repliziert werden kann. Es wurde bereits in Hardware und Mitarbeiter mit Fachwissen zu Lösungen investiert. Eine große Organisation kann sich dafür entscheiden, ihre IT-Ressourcen zu einem Standardprodukt zu machen.
- **Ältere Anwendungen:** Es gibt unternehmenswichtige ältere Anwendungen, die nicht ohne Weiteres physisch verlagert werden können.
- **Datenhoheit und Sicherheit:** Politische Grenzen oder gesetzliche Vorgaben können vorschreiben, wo Daten physisch gespeichert werden müssen.
- **Einhaltung gesetzlicher Bestimmungen/Zertifizierung:** PCI- und HIPAA-Konformität. Zertifiziertes lokales Rechenzentrum.

## <a name="hybrid-cloud"></a>Hybrid Cloud

Eine Hybrid Cloud ist eine IT-Umgebung, in der eine öffentliche und private Cloud kombiniert werden, um Daten und Anwendungen gemeinsam zu nutzen. Bei schwankendem Rechen- und Verarbeitungsbedarf bietet eine Hybrid Cloud Unternehmen die Möglichkeit, ihre lokale Infrastruktur nahtlos mithilfe der öffentlichen Cloud hoch zu skalieren, um eine eventuelle Spitze zu bewältigen, ohne Rechenzentren von Drittanbietern Zugriff auf die Gesamtheit ihrer Daten zu gewähren. Unternehmen kommen in den Genuss der Flexibilität und Rechenleistung der öffentlichen Cloud für einfache und unsensible Datenverarbeitungsaufgaben, während sie geschäftskritische Anwendungen und Daten lokal und sicher hinter einer Unternehmensfirewall nutzen können.

Beim Einsatz einer Hybrid Cloud ist es nicht mehr notwendig, im Vorfeld Investitionen zu tätigen, um kurzfristige Bedarfsspitzen abzufedern. Es ermöglicht außerdem das flexible Bestimmen, welche Ressourcen lokal und welche in der Cloud verfügbar sind. Unternehmen zahlen nur für Ressourcen, die sie vorübergehend nutzen, anstatt zusätzliche Ressourcen und Betriebsmittel zu kaufen, zu programmieren und instand zu halten, die möglicherweise über einen längeren Zeitraum ungenutzt bleiben. Die Integration erfolgt in der Regel über ein sicheres VPN zwischen einem Cloudanbieter wie Azure und lokalen Rechenzentren.

Angenommen, Sie arbeiten in einem Unternehmen im Gesundheitswesen und haben eine Anwendung, in der Kunden auf ihre medizinischen Daten zugreifen können. Eine Vorschrift verlangt, dass die Daten an einem konkreten Ort aufbewahrt werden müssen. Die Kundenwebsite muss auf die Anforderungen vieler globaler Nutzer reagieren können.  Eine Lösung kann sein, die Datenbank in einem lokalen Rechenzentrum und die Website in der öffentlichen Cloud zu hosten. Ein VPN wird zwischen dem lokalen Rechenzentrum und der öffentlichen Cloud verwendet. Dieses Szenario eignet sich für eine Hybrid Cloud.

### <a name="why-hybrid-cloud"></a>Gründe für eine Hybrid Cloud

Mit einer Hybrid Cloud kann Ihr Unternehmen eine private Infrastruktur für vertrauliche Datenbestände steuern und verwalten. Sie bietet Ihnen auch die Flexibilität, zusätzliche Ressourcen in der öffentlichen Cloud in Anspruch zu nehmen, sobald Sie sie benötigen. Mit der Möglichkeit einer Skalierung mithilfe der öffentlichen Cloud zahlen Sie nur bei Bedarf für zusätzliche Rechenleistung. Auch der Übergang zur Cloud kann dadurch erleichtert werden. Sie können allmählich migrieren, indem Sie die Workloads mit der Zeit schrittweise verlagern.

Szenarios, in denen sich die Hybrid Cloud eignet:

- **Bereits erfolgte Investitionen in Hardware:** Aus geschäftlichen Gründen müssen Sie die vorhandene Betriebsumgebung und Hardware verwenden.
- **Gesetzliche Vorschriften:** Vorschriften setzen voraus, dass die Daten an einem physischen Ort gespeichert werden müssen.
- **Eindeutige Betriebsumgebung:** Eine ältere Betriebsumgebung kann nicht in der öffentlichen Cloud repliziert werden.
- **Migration:**: Verlagern Sie Workloads mit der Zeit in die Cloud.
