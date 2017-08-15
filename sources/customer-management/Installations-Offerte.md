![](1.png)\ ![](zhdk.png)


# Offerte Initiale Installation "leihs"

Im Folgenden unsere Offerte für eine initiale Installation der freien Ausleih- und Inventarverwaltungssoftware „leihs“.


## Umfang und Abgrenzung

Diese Offerte beinhaltet das initiale Aufsetzen und die Basis-Konfiguration einer "leihs"  Instanz auf einem vom Kunden bereitgestellten System. Nach Abschluss der installation ist die installierte Instanz via HTTP zugänglich und grundsätzlich betriebsbereit.

Diese Offerte beinhaltet insbesondere folgende Punkte nicht:

* Vor- oder nachgängige Beratung zur Anwendung und Funktion der Sofware leihs an sich.
* Die Netzwerkkonfiguration des Systems.
* Zusätzliche Absicherung des Systems (Firewall, Linux hardening etc.).
* Konfiguration eines von den gängigen Browser akzeptierten SSL Zertifikates.
* Anlegen, Einrichten und Konfiguration von Benutzerdaten, z.B. Inventar, Modelle, etc.
* Installation von Updates und Upgrades der Software "leihs".


## Kosten

Für die Basisinstallation berechnen wir 1200 CHF. Dies gilt für den Fall, dass die in diesem Dokument gestellten Anforderungen erfüllt sind. Abweichungen sind gegebenenfalls bezüglich Mehrkosten und Machbarkeit mit uns abzuklären.


## Anforderungen an das Zielsystem

Folgende Anforderungen an das System gelten für eine erfolgreiche Installation:

1.	Betriebssystem Debian GNU/Linux 8 oder Ubuntu LTS 16.04 in der jeweiligen gängigen Grundkonfiguration.
2.	Es sollen keine weiteren Services installiert sein und es dürfen keine grundlegenden Änderungen am System vorliegen (z.B. Init-System).
3.	Wir empfehlen mindestens 2GB RAM und Rechenleistung äquivalent zu 2 aktuellen CPU Cores.
4.	Erreichbarkeit des Systems via HTTP und HTTPS.
5.	Erreichbarkeit für Angestellte der ZHdK via SSH (für die Dauer der Installation).
6.	Zugriff auf das allgemeine Internet vom System insbesondere via HTTP und sonstiger gängiger Protokolle (z.B. rsync und git).
7.	Rootzugriff für die jeweiligen Angestellten der ZHdK via SSH-Key. Notwendige „public“-keys werden von uns zur Verfügung gestellt.


## Weitere Empfehlungen für das Zielsystem

Wir empfehlen sehr eine Virtualisierungsschicht (z.B. VMware oder LXD/LXC) mit Snapshotmöglichkeit einzusetzen. Jedoch muss sich das Zielsystem von „innen“ wie ein echtes Betriebssystem mit vollem Init-System usw verhalten. Eine Installation auf ein unvollständiges System (z.B. Docker-Container) bieten wir nicht an.

Nach der Installation ist das System via HTTP und HTTPS grundsätzlich zugänglich. HTTPS verwendet ein sogenanntes selbstsigniertes Zertifikat. Wir empfehlen den HTTP(S) Verkehr über ein von diesem System unterschiedlichen HTTPS-Proxy mit einem von den gängigen Browser akzeptieren Zertifikat zu leiten. Wir empfehlen das Zielsystem bis auf diesen Verkehr grundsätzlich abzuschotten (Firewall, privates Netzwerk, ...). Für vom generellen Internet zugänglichen leihs Instanzen empfehlen wir den Zugriff auf nur HTTPS einzuschränken.

Nach der Installation muss zunächst ein initialer Administrator über die Benutzerschnittstelle angelegt werden. Bis dies geschehen ist sollte die Instanz nicht generell via HTTP zugreifbar sein.
Dahingehende Massnahmen sind vom Kunden zu implementieren.

Um einige Features von leihs sinnvoll verwenden zu können verschickt eine leihs-Instanz E-Mails via SMTP. Die Angabe der notwendigen SMTP-Parameter kann über die Benutzerschnittstelle vorgenommen werden.


## Folgeaufwände: Verbesserungen, Fehlerbehebung und Sicherheitsrelevante Erneuerungen

Wir wollen hier darauf hinweisen, dass eine eigene Installation von leihs in der Regel Folgeaufwände und Folgekosten nach sich zieht. Wir liefern in der Regel alle 2 Wochen eine neue Version aus. Diese kann neben neuen Eigenschaften auch Problembehebungen und vor allem sicherheitsrelevante Massnahmen beinhalten. In der Regel sollte daher eine bestehende Installation regelmässig gewartet respektive erneuert werden.
