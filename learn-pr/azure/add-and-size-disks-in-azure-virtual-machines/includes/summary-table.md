
Die folgende Tabelle zeigt, welche Datenträger als verwalteten und nicht verwalteten Datenträger verfügbar sind.

|Datenträgertyp  |Nicht verwaltete  | Verwaltet  | Storage-Konto für nicht verwaltete|
|---------|---------|---------|---------|
|[Standard HDD](https://docs.microsoft.com/azure/virtual-machines/windows/standard-storage)      |   Ja      |  Ja       |  Allgemeines Speicherkonto       |
|[Standard-SSD](https://docs.microsoft.com/azure/virtual-machines/windows/disks-standard-ssd)    |   no      |   Ja      |  Nicht zutreffend       |
|[Premium-SSD](https://docs.microsoft.com/azure/virtual-machines/windows/premium-storage)    |    Ja     |   Ja      |     Storage Premium-Konto    |

Hier ist ein Überblick über die vor-und Nachteile, die Sie vornehmen, wenn Sie einen Datenträgertyp für Ihre virtuellen Computer auswählen.

|Datenträgertyp  |Relative IOPS *  | Relative Kosten  | Szenarien|
|---------|---------|---------|---------|
|[Standard HDD](https://docs.microsoft.com/azure/virtual-machines/windows/standard-storage)      |   niedrigste      |  niedrigste       |  Verwenden Sie für Workloads mit Low-IOPS-Anforderungen, die eine konsistente Leistung und kostengünstige Entwicklung und Tests erfordern       |
|[Standard-SSD](https://docs.microsoft.com/azure/virtual-machines/windows/disks-standard-ssd)    |   Mittel|   Mittel      |  Verwenden Sie für Workloads mit Low-IOPS-Anforderungen, die eine konsistente Leistung und kostengünstige Entwicklung und Tests erfordern |
|[Premium-SSD](https://docs.microsoft.com/azure/virtual-machines/windows/premium-storage)    |    höchste     |   höchste      |     Verwenden Sie für die Produktion und leistungsorientierte Workloads, in denen geringe Latenz und hohem Durchsatz wichtig sind    |

* IOPS - e/a-Vorgänge pro Sekunde.