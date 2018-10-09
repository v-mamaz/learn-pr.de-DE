Viele Entwickler entscheiden sich in erster Linie aufgrund von Features oder persönlichen Vorlieben für die Frameworks und Bibliotheken, die sie verwenden, um ihre Software zu erstellen. Das gewählte Framework ist jedoch eine wichtige Entscheidung, nicht nur im Hinblick auf Design und Funktionalität, sondern auch aus einer _Sicherheitsperspektive_. Eine der besten Möglichkeiten, die Sicherheit von Apps zu gewährleisten, ist, ein Framework mit modernen Sicherheitsfeatures auszuwählen und auf dem neuesten Stand zu halten.

## <a name="choose-your-framework-carefully"></a>Sorgfältiges Auswählen des Frameworks

Bei der Auswahl eines Frameworks ist der wichtigste Faktor in Bezug auf Sicherheit, wie gut es unterstützt wird. Die besten Frameworks haben Sicherheitsvorkehrungen festgelegt und werden von großen Communitys unterstützt, die das Framework verbessern und testen. Keine Software ist vollkommen fehlerfrei oder sicher, aber wenn ein Sicherheitsrisiko identifiziert wurde, möchten wir darauf vertrauen können, dass es schnell behoben wird oder eine Problemumgehung bereitgestellt wird.

Häufig ist „gut unterstützt“ ein Synonym für „modern“. Ältere Frameworks werden entweder nach und nach ersetzt oder büßen an Beliebtheit ein. Auch wenn Sie über umfassende Erfahrung mit einem älteren Framework oder über viele Apps verfügen, die darin geschrieben wurden, profitieren Sie von einer modernen Bibliothek, die alle benötigten Features bietet. Moderne Frameworks nutzen die aus früheren Iterationen gewonnenen Erkenntnisse. Wenn sie für neue Apps ausgewählt werden, kann damit die Angriffsfläche verringert werden. Sie müssen sich um eine App mehr kümmern, wenn ein Sicherheitsrisiko im älteren Framework ermittelt wird, in dem Ihre älteren Anwendungen geschrieben wurden.

Informationen zu einem sicheren Entwurf und darüber, wie Sie die Angriffsfläche verringern können, finden Sie unter [Sicherheitsorientierter Entwurf in Azure](../../design-for-security-in-azure/index.yml).

## <a name="keep-your-framework-updated"></a>Aktualisieren Ihres Frameworks

Für Frameworks für die Softwareentwicklung wie Java Spring und .NET Core werden regelmäßig Updates und neue Versionen veröffentlicht. Diese Updates enthalten neue Features, entfernen alte Features und bieten oft Sicherheitsfixes oder Verbesserungen. Wenn wir unsere Frameworks nicht auf dem aktuellen Stand halten, entstehen „technische Schulden“. Je älter die Frameworks werden, desto schwieriger und riskanter wird es, unseren Code auf die neueste Version zu aktualisieren. Ähnlich wie durch die ursprüngliche Entscheidung für ein Framework entstehen durch die Nutzung älterer Versionen des Frameworks weitere Sicherheitsrisiken, die in neueren Versionen des Frameworks behoben wurden.

Beispielsweise wurden von 2016 bis 2017 [mehr als 30 Sicherheitsrisiken](https://www.cvedetails.com/product/6117/Apache-Struts.html?vendor_id=45) im Apache Struts-Framework gefunden. Diese wurden umgehend vom Entwicklungsteam behandelt. Einige Unternehmen haben die Patches jedoch nicht angewendet und [haben den Preis in Form einer Datenpanne bezahlt](https://www.zdnet.com/article/equifax-confirms-apache-struts-flaw-it-failed-to-patch-was-to-blame-for-data-breach/). **Achten Sie darauf, dass Ihre Frameworks und Bibliotheken auf dem neuesten Stand bleiben**.

### <a name="how-do-i-update-my-framework"></a>Wie kann ich mein Framework aktualisieren?

Einige Frameworks, z.B. Java oder .NET, erfordern eine Installation und veröffentlichen in der Regel nach einem bekannten Zeitplan. Es ist eine gute Idee, auf neue Versionen zu achten und einen Branch des Codes zu erstellen, um sie auszuprobieren, sobald sie freigegeben wurden. Beispielsweise gibt es für .NET Core eine [Seite für Anmerkungen zu Versionen](https://github.com/dotnet/core/tree/master/release-notes), die Sie auf die neuesten verfügbaren Versionen überprüfen können.

Spezialisiertere Bibliotheken wie JavaScript-Frameworks oder .NET-Komponenten können über einen Paket-Manager aktualisiert werden. **NPM** und **Bower** sind häufig verwendete Optionen für Webprojekte und werden von den meisten IDEs oder Buildtools unterstützt. In .NET verwenden wir **NuGet**, um Komponentenabhängigkeiten zu verwalten. Wie das Aktualisieren des Kernframeworks sind das Branchen Ihres Codes, das Aktualisieren der Komponenten und das Testen ein gutes Verfahren, um eine neue Version einer Abhängigkeit zu überprüfen.

> [!NOTE]
> Das `dotnet`-Befehlszeilentool verfügt über die Optionen `add package` und `remove package` zum Hinzufügen oder Entfernen von NuGet-Paketen, jedoch nicht über einen entsprechenden `update package`-Befehl. Allerdings können Sie `dotnet add package <package-name>` in Ihrem Projekt ausführen, und das Paket wird automatisch auf die neueste Version _aktualisiert_. Dies ist eine einfache Möglichkeit, Abhängigkeiten zu aktualisieren, ohne die IDE zu öffnen.

## <a name="take-advantage-of-built-in-security"></a>Nutzen der integrierten Sicherheit

Überprüfen Sie immer, welche Sicherheitsfeatures Ihre Frameworks bieten. Setzen Sie **nie** eigene Sicherheitsfunktionen ein, wenn es ein Standardverfahren oder eine integrierte Funktion gibt. Vertrauen Sie zudem auf bewährte Algorithmen und Workflows, da diese häufig von vielen Experten geprüft und verbessert wurden. Dadurch können Sie darauf bauen, dass sie zuverlässig und sicher sind.

Das .NET Core-Framework verfügt über zahlreiche Sicherheitsfeatures, über die Sie sich beispielsweise in folgenden Abschnitten der Dokumentation informieren können.
* [Authentifizierung und Identitätsverwaltung](https://docs.microsoft.com/aspnet/core/security/authentication/index?view=aspnetcore-2.1)
* [Autorisierung](https://docs.microsoft.com/aspnet/core/security/authorization/index?view=aspnetcore-2.1)
* [Schutz von Daten](https://docs.microsoft.com/aspnet/core/security/data-protection/index?view=aspnetcore-2.1)
* [Sichere Konfiguration](https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/index?view=aspnetcore-2.1)
* [Erweiterbarkeits-APIs für Sicherheit](https://docs.microsoft.com/aspnet/core/security/data-protection/extensibility/index?view=aspnetcore-2.1)

Jedes dieser Features wurde von Experten auf dem jeweiligen Gebiet geschrieben und dann umfassend getestet, um sicherzustellen, dass es ausschließlich wie beabsichtigt funktioniert. Andere Frameworks bieten ähnliche Features. Informieren Sie sich beim Anbieter des Frameworks über die verfügbaren Funktionen in jeder Kategorie.

> [!WARNING]
> Wenn Sie Ihre eigenen Sicherheitskontrollen schreiben, statt die von Ihrem Framework bereitgestellten zu verwenden, verschwenden Sie Zeit und erreichen weniger Sicherheit.


## <a name="azure-security-center"></a>Azure Security Center

Wenn Sie Azure zum Hosten Ihrer Webanwendungen verwenden, werden Sie von Security Center auf der Registerkarte mit Empfehlungen gewarnt, wenn Ihre Frameworks veraltet sind.  Vergessen Sie nicht, diese Registerkarte von Zeit zu Zeit zu prüfen, um festzustellen, ob es Warnungen im Zusammenhang mit Ihren Apps gibt.

![Azure Security Center empfiehlt ein Frameworkupgrade.](../media/5-ASCFramework.png)


## <a name="summary"></a>Zusammenfassung

Wählen Sie nach Möglichkeit ein modernes Framework zum Erstellen von Apps aus, verwenden Sie immer die integrierten Sicherheitsfeatures, und halten Sie es auf dem neuesten Stand. Mit diesen einfachen Regeln können Sie sicherstellen, dass Ihre Anwendung auf einer soliden Grundlage gestartet wird.
