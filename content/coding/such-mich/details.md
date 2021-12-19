---
title: "Such mich - Hintergründe"
draft: false
---

## Motivation

Such mich enstand als Referenzrpojekt für die Umsetzung einer WPF Anwendung. Aus meiner Leidenschaft für das bekannte Memory Spiel entschied ich mich daran anzulehnen. Im Zuge der Entwicklung dieser Anwendung enstand auch die WPF Fundamentals - Library. 

## Clean Code

Da der Code nach den Clean-Code-Prinzipien programmiert ist, sollte er hoffentlich eine hohe Lesbarkeit haben. Und wer will kann ihn auch gerne weiter entwickeln (Boyscout-rule applies: Always leave code better than you found it)

## Umsetzung

Beim ursprünglichen Design des Codes habe ich folgendes Klassendiagramm zurgrunde gelegt. Die Idee war, mit Hilfe der in Visual Studio mitgelieferten Code Generierung (Ultimate Edition only) das Prinzip der Model-Driven-Architekture umzusetzen. Hier das erste Klassendiagramm:

{{< figure src="/dotnet/such-mich/suchmich/ClassDiagram.png" >}}

Leider hat das UML-Tool einen kleinen, aber fatalen Haken: Einmal erzeugter Code kann zwar geändert werden, startet man nach einer Änderung aber wieder die Codegenerierung im Model werden alle bis dahin gemachten Änderungen im Code wieder überschrieben. Eine Möglichkeit, für z.B. im Model definierte Klassen bereits fertigen Code zu hinterlegen gibt es auch nicht [siehe dazu meinen Beitrag auf Stackoverflow.com](http://stackoverflow.com/questions/8644058/visual-studio-uml-2010-code-generation-for-methods-or-properties). Hier hat Microsoft meiner Meinung nach noch viel nachzuholen, denn diese Handicap macht produktives Arbeiten mit dem Tool fast schon unmöglich. 

Somit bin ich wieder auf die bewährte ["Test-First"](http://de.wikipedia.org/wiki/Testgetriebene_Entwicklung) Methodik umgeschwenkt. Also hiess es erst mal jede Menge Tests schreiben, und meine ganze Logik über Tests abzubilden. 

Aus den finalen Klassen habe ich wieder ein Klassendiagramm generieren lassen. Man vergleiche Original und Fälschung...

{{< figure src="/dotnet/such-mich/suchmich/ClassDiagramFinalScreenshot.png" >}}

Es sind doch ein paar mehr Klassen geworden als erwartet. Ich bezweifle stark, das ich mit Hilfe von Model-Driven-Development (sprich: Code aus Klassen erzeugen, programmieren, Klassen aus Code erzeugen, grafisch verändern, code aus Klassen erzeugen, programmieren, ...) jemals dorthin gekommen wäre. Test-First ist doch die wesentlich hilfreichere Programmiermethodik. 

## Ergebnis
Das fertige Spiel kann man hier einfach herunterladen und ausprobieren: (http://www.andreaslennartz.de/dotnet/such-mich)


## Open Source
Der komplette Code ist Open Source - abgelegt auf Codeplex GitHub unter (github.com/roadrunnerlenny/suchmich)

## WPF Fundamentals

WPF Fundamentals ist eine Bibliothek mit grundlegenden Funktionen für die WPF Programmierung, die von diesem Spiel benutzt wird. [Hier erfährt man mehr.](../wpf-fundamentals)