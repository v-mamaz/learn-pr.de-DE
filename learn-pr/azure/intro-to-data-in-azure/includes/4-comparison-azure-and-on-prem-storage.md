Da Sie jetzt die Vorteile und Funktionen von Azure Storage kennengelernt haben, betrachten Sie nun die Unterschiede zwischen Azure Storage und einem lokalen Speicher.

## <a name="azure-storage-versus-on-premises-storage"></a>Azure Storage-Speicher und lokaler Speicher im Vergleich

Der Begriff „lokal“ bezieht sich auf die Speicherung und Verwaltung von Daten auf lokaler Hardware und lokalen Servern. Beim Vergleich eines lokalen Speichers mit Azure Storage sollten verschiedene Faktoren berücksichtigt werden.

### <a name="cost-effectiveness"></a>Kosteneffizienz
Bei einer Lösung mit lokalem Speicher muss speziell Hardware erworben, installiert, konfiguriert und gewartet werden. Dies kann mit erheblichen Vorlaufkosten (oder Kapitalkosten) verbunden sein. Wenn sich im Lauf der Zeit Anforderungen ändern, bedeutet dies häufig eine Investition in neue Hardware. Bei Bedarfsspitzen müssen Sie außerdem in Hardware investieren, die mit diesen Bedarfsspitzen umgehen kann, in Zeiten mit weniger Bedarf jedoch nicht ausgelastet ist.

Azure Storage bietet ein Preismodell mit nutzungsbasierter Bezahlung, was für Unternehmen häufig attraktiv ist, da anstelle von Investitionsvorlaufkosten Betriebsausgaben verbucht werden können. Ferner ist dieses Modell skalierbar, d.h. Sie können die Ressourcen je nach Bedarf zentral oder horizontal hochskalieren und bei geringer werdendem Bedarf auch wieder herunterskalieren. Dabei werden nur die tatsächlich beanspruchten Datendienste berechnet.

### <a name="reliability"></a>Zuverlässigkeit 
Für einen lokalen Speicher werden Datensicherungs-, Lastenausgleichs- und Notfallwiederherstellungsstrategien benötigt. Diese können eine Herausforderung darstellen und kostspielig sein, da hierfür häufig spezielle Server benötigt werden, die eine beachtliche Investition sowohl in die Hardware als auch in IT-Ressourcen erfordern.

Azure Storage stellt Datensicherung, Lastenausgleich, Notfallwiederherstellung und Datenreplikation zur Gewährleistung von Datensicherheit und Hochverfügbarkeit in Form von Diensten bereit.

### <a name="storage-types"></a>Speichertypen
Manchmal werden für eine Lösung mehrere verschiedene Speichertypen benötigt, beispielsweise ein Datei- und ein Datenbankspeicher. Bei einem lokalen Konzept sind für die einzelnen Speichertypen häufig zahlreiche Server und Verwaltungstools erforderlich.

Azure Storage bietet eine Vielzahl von verschiedenen Speicheroptionen, darunter Speicher mit verteiltem Zugriff und mehrstufige Speicher. Dadurch ist es möglich, eine Kombination von Speichertechnologien zu integrieren und für jeden Teil einer Lösung die besten Speicheroptionen bereitzustellen.

### <a name="agility"></a>Flexibilität
Anforderungen und Technologien ändern sich. Für eine lokale Bereitstellung kann dies bedeuten, dass neue Server und Infrastrukturbestandteile bereitgestellt werden müssen, was sehr zeitaufwändig und kostspielig ist.

Mit Azure Storage können Sie neue Dienste innerhalb von Minuten flexibel bereitstellen. Dank dieser Flexibilität können Sie Speicher-Back-Ends im Nu ohne nennenswerte Hardwareinvestitionen ändern.

In der folgenden Illustration werden die Unterschiede zwischen lokalem Speicher und Azure-Datenspeicher veranschaulicht.

![Illustration mit Vergleich von lokalem Speicher und Azure-Datenspeicher für mehrere häufig vertretene Geschäftsanforderungen.](../media/4-Comparison.png)
