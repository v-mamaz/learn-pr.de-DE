Viele Entwickler sollten Sie die Frameworks und Bibliotheken, die sie verwenden, um ihre Software mit zu erstellen, die in erster Linie von Features oder Geschmackssache beschlossen. Das Framework, das Sie auswählen, ist jedoch eine wichtige Entscheidung, nicht nur von einer Perspektive Designs und der Funktionen, sondern auch aus einer _Sicherheit_ Perspektive. Auswählen eines Frameworks mit modernen Sicherheitsfunktionen und die Aktualisierung auf dem neuesten Stand ist eine der besten Möglichkeiten, um sicherzustellen, dass Ihre apps sicher sind.

## <a name="choose-your-framework-carefully"></a>Wählen Sie sorgfältig die Framework-Komponente

Der wichtigste Faktor in Bezug auf Sicherheit, die beim Auswählen eines Frameworks wie gut unterstützt ist. Der besten Frameworks laut Sicherheitsvorkehrungen und von großen Communitys, die zu verbessern, und testen das Framework unterstützt werden. Keine Software ist 100 % fehlerfrei oder ganz sicher ein Sicherheitsrisiko identifiziert wurde, möchten wir sicher, dass es geschlossen wird oder eine problemumgehung, die schnell bereitgestellt haben.

Häufig "gut unterstützt" ist ein Synonym mit "moderne". Älteren Frameworks sind tendenziell ersetzt werden, oder schließlich Beliebtheit eingeblendet. Auch wenn Sie die umfassende Erfahrung mit der verfügen oder oder viele apps, die in einem älteren Framework geschrieben wurden, Sie werden besser, eine moderne-Bibliothek, die die Funktionen verfügt, Sie müssen, auswählen. Moderne Frameworks neigen dazu, um auf die von früheren Iterationen auswählen für neue apps eine Form der Verringerung der Bedrohung dadurch gewonnenen Erkenntnisse zu erstellen. Sie müssen weniger Gedanken, wenn eine Schwachstelle in älteren Framework ermittelt wird, die Ihre älteren Anwendungen, in geschrieben wurden eine app.

<!-- TODO: add link; Should we be pointing to other modules? -->
<!--
For more information on secure design and reducing threat surface, please see [Design For Security in Azure](../../design-for-security-in-azure/index.yml).
-->

## <a name="keep-your-framework-updated"></a>Halten Sie Ihr Framework aktualisiert

Software Development Frameworks, z. B. Java Spring und .NET Core release regelmäßig Updates und neue Versionen. Diese Updates enthalten neue Features, die zum Entfernen der alten Features und oft Sicherheitsupdates oder Verbesserungen. Wenn wir unsere Frameworks, dank derer Sie irgendwann veraltet sein kann, wird "technischen Schuld" erstellt. Die weiteren veraltet erhalten wir, die schwieriger und riskanter wird, unseren Code auf die neueste Version zu öffnen. Darüber hinaus ähnlich wie die erste Framework-Auswahl, bleiben in älteren Versionen des Frameworks öffnen Sie auf Weitere Sicherheitsrisiken, die in neueren Versionen des Frameworks behoben wurden.

Als Beispiel von 2016-2017 [mehr als 30 Sicherheitsrisiken](https://www.cvedetails.com/product/6117/Apache-Struts.html?vendor_id=45) in das Apache Struts Framework wurden gefunden. Diese umgehend vom Entwicklungsteam vertraulich behandelt wurden, ohne einige Unternehmen haben die Patches und [bezahlt den Preis in Form einer sicherheitsverletzung der Daten](https://www.zdnet.com/article/equifax-confirms-apache-struts-flaw-it-failed-to-patch-was-to-blame-for-data-breach/). **Achten Sie darauf, Ihre Frameworks und Bibliotheken auf dem neuesten Stand zu halten**.

### <a name="how-do-i-update-my-framework"></a>Wie aktualisiere ich mein Framework?

Einige Frameworks, z. B. Java oder .NET, eine Installation erforderlich und für eine rasche bekannte Version in der Regel. Es ist eine gute Idee, sehen Sie sich bei neuen Versionen und möchten, stellen eine Verzweigung des Codes zu probieren es aus, wann es freigegeben wird. Beispielsweise .NET Core verwaltet eine [Seite für versionsanmerkungen](https://github.com/dotnet/core/tree/master/release-notes) die Sie überprüfen können, finden Sie die neuesten Versionen verfügbar.

Spezialisierter Bibliotheken wie JavaScript-Frameworks oder .NET-Komponenten können über einen Paketmanager aktualisiert werden. **NPM** und **Bower** werden häufig verwendete Optionen für Webprojekte und werden von den meisten IDEs unterstützt oder build-Tools. In .NET verwenden wir **NuGet** komponentenabhängigkeiten zu verwalten. Wie aktualisieren das Core-Framework, ist Branchen Ihres Codes, aktualisieren die Komponenten aus, und Testen von viel für ein gutes Verfahren, um eine neue Version einer Abhängigkeit zu überprüfen.

> [!NOTE]
> Die `dotnet` Befehlszeilentool verfügt über eine `add package` und `remove package` Option zum Hinzufügen oder Entfernen von NuGet-Pakete, jedoch keine entsprechende `update package` Befehl. Allerdings herausstellt, können Sie ausführen, `dotnet add package <package-name>` in Ihr Projekt, und es wird automatisch _upgrade_ des Pakets auf die neueste Version. Dies ist eine einfache Möglichkeit, Abhängigkeiten zu aktualisieren, ohne die IDE zu öffnen.

## <a name="take-advantage-of-built-in-security"></a>Profitieren Sie von der integrierten Sicherheit

Überprüfen Sie immer, um festzustellen, welche Sicherheitsfeatures für Ihr Angebot Frameworks. **Nie** Ihre Sicherheit selbst zurücksetzen, wenn es eine Standardmethode oder integriert. Darüber hinaus basieren auf bewährten Algorithmen Workflows und da diese häufig von einer großen-Experten geprüft wurde critiqued und gestärkt werden, damit Sie sicher sein können, die sie zuverlässig und sicher sind.

Das .NET Core-Framework verfügt über zahlreiche Sicherheitsfunktionen, hier sind einige Core stellen in der Dokumentation zu starten.
* [Authentifizierung-Identitätsverwaltung](https://docs.microsoft.com/aspnet/core/security/authentication/index?view=aspnetcore-2.1)
* [Autorisierung](https://docs.microsoft.com/aspnet/core/security/authorization/index?view=aspnetcore-2.1)
* [Schutz von Daten](https://docs.microsoft.com/aspnet/core/security/data-protection/index?view=aspnetcore-2.1)
* [Sicherheitskonfiguration](https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/index?view=aspnetcore-2.1)
* [Security-Erweiterbarkeits-APIs](https://docs.microsoft.com/aspnet/core/security/data-protection/extensibility/index?view=aspnetcore-2.1)

Diese Features jeweils wurde von Experten auf Ihrem jeweiligen Gebiet geschrieben und dann battered mit Tests, um sicherzustellen, dass sie erwartungsgemäß funktioniert, und nur als beabsichtigt. Andere Frameworks Angebot ähnliche Features – Sie sich an den Hersteller, der bietet das Framework, um herauszufinden, was sie in jeder Kategorie aufweisen.

> [!WARNING]
> Schreiben Ihren eigenen Sicherheitskontrollen, anstatt die von Ihr Framework bereitgestellten ist nicht nur Zeitverschwendung, es ist weniger sicher.


## <a name="azure-security-center"></a>Azure Security Center

Bei Verwendung von Azure zum Hosten Ihrer Webanwendungen-Sicherheitscenter gewarnt, wenn Ihre Frameworks veraltet, als Teil der Registerkarte "Empfehlungen sind".  Vergessen Sie nicht, um festzustellen, ob im Zusammenhang mit Ihren apps Warnungen gibt es von Zeit zu Zeit suchen.

![Azure Security Center-Empfehlung ein Framework aktualisieren.](../media-draft/ASCFramework.png)


## <a name="summary"></a>Zusammenfassung

Wählen Sie nach Möglichkeit eine moderne Framework zum Erstellen von apps immer verwenden Sie die integrierten Sicherheitsfeatures und stellen Sie sicher, dass Sie es auf dem neuesten Stand halten. Um sicherzustellen, dass die Anwendung auf eine solide Grundlage gestartet wird, ist diese einfachen Regeln helfen.
