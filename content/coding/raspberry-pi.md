---
title: "Raspberry PI"
draft: false
---

## MyCloud - die Idee

Zu meinem letzten Geburtstag bekam ich einen Raspberry PI geschenkt. Ein nettes Spielzeug. Nachdem ich die Grundbegriffe des Raspberry PI verstanden hatte, musste neben der Spielerei auch eine praktische Anwendung her. Hier meine großartige Idee: 

Auf meinem Laptop (ein schickes MacBook Pro) habe ich viele verschiedene private Daten liegen - verschiedenste Dokumente, selbgedrehte Videos, Eingescannte Dokumente u.v.m. Es gibt zwar eine Reihe von Cloud-Anbietern, aber dort bekommt man immer nur ein vergleichsweise kleine Menge an (kostenlosen) Speicherplatz. Obwohl ich Dropbox, Google Drive & Co auf  meinem Laptop nebenher laufen habe, verpasse ich es immer die Dokumente in die Cloud zu schieben, auf die ich auch zugreifen möchte. Am Ende sind die Dateien, die ich eigentlich wollte, doch auf meinem Laptop, und der Zugriff von einem anderen Rechner aus blieb mir meistens verwehrt. Und auch der Versuch, mich per VPN in mein Heimnetz einzuwählen, brachte keinen Erfolg, denn war ich nicht zuhause, war mein Laptop auch nicht erreichbar. Irgendwie waren alle Ansätze, alle meine zuhause erstellen Dateien bequem auch "Remote" verfügbar zu machen, nicht zufriedenstellend.

Doch was tun? Nachdem ich stolzer Besitzer einer Apple "TimeCapsule" bin, läuft schon seit einigen Jahren regelmäßig eine Sicherung aller meiner Dateien auf diese Festplatte im Netzwerk. Regelmäßig heißt: Sobald ich eine Datei ändere oder erstelle, merkt dies mein MacBook. Bei bestehender WLAN-Verbindung in meinem Heimnetzwerk wird diese Datei automatisch im Hintergrund auf der TimeCapsule gesichert (ohne dabei die Bandbreite des WLAN lahmzulegen). Dabei werden auch Änderungen an Dateien mitgesichert und alte Versionen der Dateien vorgehalten - bis die Festplatte in der TimeCapsule voll ist. Ab dann werden auch alte Datei-Versionen gelöscht. Wenn man eine komplette Sicherung oder eine bestimmte Datei zu einem bestimmten Zeitpunkt wiederherstellen will gibt es dafür die "TimeMachine" von Apple. 

Somit befinden sich alle meine Dokumente auf der Backup-Festplatte meiner TimeCapsule. Diese Festplatte läuft immer, die TimeCapsule ist ständig an und im Netzwerk erreichbar. Und da alle meine Dateien dort als Backup liegen, müsste es nun doch auch möglich sein, über das Web darauf zuzugreifen? So schwer kann das doch nicht sein, dachte ich. "Challenge accepted". Ich nannte das Projekt "MyCloud", da ich im Prinzip mein eigener Cloud-Anbieter werden wollte.

## MyCloud - Das Setup

Hier das Setup meines Heimnetzes

- Apple MacBook Pro (10th Generation)
- Apple TimeCapsule (2nd Generation)
- FritzBox 7362 SL
- Raspberry PI 2

Und hier ein Bild von meinem Netzwerk, ohne das MacBook:

{{< figure src="/dotnet/raspberry-pi/TheNetwork.jpg" >}}

## MyCloud - den RasPI konfigurieren

Die erste Hürde, die ich zu nehmen hatte, war es den Raspberry PI zu einem voll funktionsfähigen Webserver auszubauen. Klingt nach einer einfachen Übung, aber der Teufel steckt hier im Detail. Auch wenn erfahrene Linux-Administratoren einen vielleicht belächeln, aber als "gestandener" Microsoft-Entwickler musste ich doch kurz in mich gehen und meine Linux Kenntnisse nochmal auffrischen. Zum Glück habe ich zuhause OS X als Betriebssystem, welches immer noch ein weiter entwickeltes Unix-System ist - und man auch dort ab und an auf die Konsole zurückgreifen kann. Dort gibt es von Haus eine Shell, und Befehle wie SSH oder mount werden genauso entgegengenommen wie auf einer beliebigen Linux Distrubution. Noch schnell die Grundlagen über vi aufgefrischt (kein schlechter Editor, wenn man sich an die etwas eigene Bedienung gewöhnt hat), und dann ging es auch schon los.

Schnell hat man das Raspberry-PI installiert, welches meines Verständnis nach an die gängigen Debian-Distributionen angelehnt ist. Gute Tutorials dafür findet man reichlich, und über apt-get (der vorhandene Paketmanager) sind auch schnell ein Webserver und weitere Pakete installiert.

Als Konfiguration entschied ich mich für 

- Lighttpd als Webserver (schlanker als Apache, und angeblich leichter zu konfigurieren)
- ShellInABox, um SSH auch via Webbrowser zugänglich zu machen
- Mono Framework - ASP.NET für meine zukünftige Anwendung

Ich erspare dem geneigten Leser jetzt die Details, diese Komponenten zum Laufen zu bringen. Meiner Meinung nach ist es manchmal etwas "fummelig", aber mit viel Ausdauer und dank doch zahlreichen Quellen im Internet ist es möglich. 

Als nächstes habe ich mich über die Fritzbox bei dem Dienst "myfritz" angemeldet, welches ein sehr einfach zu konfigurierender DynDNS-Dienst ist. Dort erhält man eine (etwas kryptische) URL (so wie "1xdfda34r3df.myfritz.net"), welche Anfragen auf die Fritzbox weiterleitet. In meiner Konfiguration habe ich mich dafür entschieden, nur Anfragen via https in der Fritzbox anzunehmen und diese dann auf meinen RasPI umzuleiten, wo der dort installierte Webserver Lighttpd eine Authentifizierung vornimmt und danach entsprechend die Anfrage beantwortet. 
Als Authentifizierung wählte ich Digest Access, und notwendige entsprechende Zertifikate stellt ich mir einfach selber aus. Digest Access sowie SSL sind zwar etwas schwieriger einzurichten, aber der etwas gehobenere Schutz meiner Daten war es mir wert. 

Nun war es mir möglich, mittels einer Webadresse sowie eines Username/Passworts meinen Webserver zuzugreifen. Auch ShellInABox brachte ich zum laufen, und war nun in der Lage nicht nur über SSH in meinem Heimnetzwerk auf meinen RasPI zuzugreifen, sondern auch von einem beliebigen Browser aus, der mit dem Internet verbunden ist. Wunderbar vernetzte Welt. 

Als nächstes musste ich mono zum laufen bringen. Auch einfacher gesagt als getan, aber nach dem lesen einiger (vieler) Quellen konnte ich erfolgreich meine erste Asp.net - Anwendung auf dem Raspberry PI zum Laufen bringen:

{{< figure src="/dotnet/raspberry-pi/HelloWorld.png" >}}

## MyCloud - die TimeCapsule verbinden

Der RaspberryPI lief und war im weltweiten Netz erreichbar, jetzt nur noch eben die Festplatte in der TimeCapsule mit meine RasPI verbinden, sodass man über diesen auf die Daten zugreifen kann. So einfach wäre das, dachte ich. Musste aber feststellen, das es doch etwas mehr zu tun gab.

Die erste Hürde ist, das ein einfaches "mount" nicht funktioniert - die TimeCapsule Festplatte hat als Dateiformat HFS+. Dafür gibt es zum Glück in Linux die CIFS-Utils, mit denen man auch eine HFS+ - HardDisk einbinden kann. Allerdings liegt das komplette Backup der TimeCapsule in einer einzigen .sparsebundle - Datei. Diese Sparsebundle ist eine Apple-eigenes Format, und der Zugriff darauf ist möglich mittels des Tools sparsebundlefs. Hinzu kommt aber noch, das sich dieses Sparsebundle auch noch von den anderen Sparsebundle unterscheidet, die Apple zum Beispiel auch für die Archivierung ihrer Foto-Bibliothekt nutzt. Denn nur das Sparsebundle mittels sparsebundlefs zugänglich zu machen, reicht nicht, da Apple bei der Sicherung mittels TimeMachine immer nur die geänderten Bänder sichert und mittels Software dann die eigentllichen Dateien rekonstruiert. DIes spart Platz, führt aber dazu das man diese Bandinformationen mit einem geeigneten Tool auslesen muss. Zum Glück gibt es schon andere Menschen, die genau das gleiche wie ich versucht haben. Und ein norwegischer Programmierer hat sich damit sehr intensiv auseingandersetzt und bietet ein Tool mit dem Namen tmfs an, mit dem man solch ein TimeMachine - sparsebundle so mounten kann, dass man auch eine vernünftige Dateistruktur sieht ( --> Siehe hier). Wenn man diese Hürde genommen hat, ist man tatsächlich in der Lage sich über den Raspberry PI mittels cd und ls auf das gemountete Verzeichnis zu begeben und dort sich die gesicherten Dateien anzusehen. Da verschiedene Versionen vorgehalten werden, kann man dort über den Ordner "Latest" auch immer auf die zuletzt aktuelle Version einer Datei zugreifen. 

{{< figure src="/dotnet/raspberry-pi/DirView.PNG" >}}

## MyCloud - das Webinterface

Nachdem der RasPI Zugriff auf alle Verzeichnisse und Dateien auf meinem Backup bekommen hatte, musste ich nur noch eine Weboberfläche bauen, mit der man einfach durch diese Verzeichnisse browsen und sich die Dateien herunterladen konnte. Eine schlichte Oberfläche mit wenig Funktionalität würde mir genügen, und ich entschloss mich diese Oberfläche mit Mono und ASP.NET zu realisieren. Als langjähriger C#-Programmierer dachte ich, hier keiner großen Herausforderung entgegen treten zu müssen, aber hatte noch nicht mit Mono gerechnet.

Das Mono Projekt ist schon seit vielen Jahren der Versuch, das .NET Framework (welches grundsätzlich ähnlich wie Java plattformunabhängig entworfen wurde) auch auf anderen Plattformen wie Linux und Mac zum laufen zu bringen. Mehr Details dazu auf der [Mono Project Homepage](http://www.mono-project.com/). Die Firma Xamarin wiederum stellt eine Entwicklungsumgebung bereit, in der man neben Anwendungen für mobile Plattformen auch ASP.NET Anwendungen entwickeln kann. Für die Entwicklung meiner Oberfläche nutzte ich deswegen das Xamarin Studio in der kostenlosen Community Edition, und die darin integrierte Vorlage für ASP.NET Projekte. Diese wiederum nutzt das Mono-Framework, welches als OpenSource ebenfalls kostenlos erhältlich ist. 

Nach ersten Recherchen über die Entwicklung einer ASP.NET Anwendung in Verbindung mit Mono und Xamarin Studio gab es schon ein paar Hinweise, dass nicht alle Funktionalitäten des "richtigen" ASP.NET (sprich dem, was Microsoft ausliefert) vorhanden sind. Trotzdem wagte ich mich daran, in der Annahme das die Grundlagen schon ausgereift seien und eine meiner Ansicht nach doch recht einfache ASP.NET Anwendung auch ohne Probleme umsetzen lassen sollte.

Nachdem ich mich in Mono eingearbeitet hatte und anfing, mein Projekt nach und nach umzusetzen, musste ich aber traurig feststellen das so manch grundsätzliche Funktionalität entweder nicht implementiert, fehlerhaft implementiert oder nur sehr mühselig umsetzbar war. Auch die entsprechende Dokumentation war teilweise sehr spärlich mit Informationen. So sah man sich teilweise mit Code konfrontiert, der in Visual Studio funktionierte, aber in Mono immer wieder neue und andere Fehlermeldungen erzeugte. So konnte man z.B. keine URLs erzeugen, welche ein / - Zeichen als Wert beinhalteten - aufgrund eines Implementierungsfehler in einer internen Mono-Komponente. Auch die Verwendung von HTML-ActionLinks oder anderen Methodiken zur einfachen Erzeugung von Links gab ich aufgrund kryptischer Fehlermeldungen an einem gewissen Zeitpunkt auf. Später musste man sich noch mit den ausgelieferten .dll des Frameworks auseinandersetzen - so half es zum Beispiel, eine bestimmte .dll, auf die bei der Entwicklung noch referenziert wird, im Ausgabeordner einfach zu löschen (ersatzlos)...dies führte dann tatsächlich dazu, das ein bestimmter sporadisch auftretener Fehler beseitigt wurde. (Wofür war diese .dll überhaupt? Egal, hauptsach funktioniert)...

Insgesamt war die Programmiererfahrung, die ich in diesem kleine Projekt mit Mono sammelte, vorwiegend negativ, und ich würde Abstand nehmen beim nächsten mal nochmal etwas mit Mono zu programmieren - zumindest keine ASP.NET Anwendung. Noch eine Chance geben würde ich allerdings dem Xamarin Studio selbst, welches als Entwicklungswerkzeug grundsätzlich einen positiven Eindruck hinterließ. Das man hier (in der kostenpflichtigen Version) durchaus brauchbare iOS oder Android oder sogar WindowsPhone Anwendungen entwickeln soll, kann ich mir inzwischen vorstellen. Auch die Integration mit GIT schien in Ordnung, auch wenn man als einzelne Person selten einen merge vornehmen muss.

Nachdem ich trotz dieser Hürden endlich meine Weboberfläche fertig gestellt und erfolgreich auf meinem RasPI deployed habe, konnte ich endlich auf meine Backup-Dateien über das Web zuzugreifen. So sah das ganze dann aus:


{{< figure src="/dotnet/raspberry-pi/MyCloud-Screen1.PNG" >}}

{{< figure src="/dotnet/raspberry-pi/MyCloud-Screen2.PNG" >}}

{{< figure src="/dotnet/raspberry-pi/MyCloud-Screen3.PNG" >}}

{{< figure src="/dotnet/raspberry-pi/MyCloud-Screen4.PNG" >}}


Und für den, der sich für den Code dieser ASP.NET - Mono - Anwendung interessiert, [den SourceCode habe ich auf github hier hinterlegt.](https://github.com/roadrunnerlenny/mycloud)