---
title: "Programming SSIS"
draft: false
---

## Hintergrund

Das Arbeiten mit SSIS ist nicht immer einfach. Insbesondere scheint SSIS von Microsoft in den letzten Jahren vernachlässigt worden zu sein - die Oberflächen sind zwar seit Sql Server 2012 modern gestaltet, "unter der Haube" liegt aber immer noch die Technologie die mit Sql Server 2005 (für Datenflüsse) bzw. Sql Server 2008 (für Control Flows) eingeführt wurde. 
Schon damals hat man die Möglichkeit vorgesehen, nicht nur mit Hilfe von Visual Studio SSIS-Pakete zu erstellen, sondern auch Pakete über Code zu erzeugen. Mittel der Wahl sollte hier C# bzw. .NET sein, die Benötigten Bibliotheken finden sich bereits im SQL Server / Visual Studio. Leider ist die Schnittstelle nicht sehr umfassend dokumentiert, und gute Beispiele für die Programmierung gegen die Schnittstelle sind rar.

## SSISComponentWrap

Um diese Lücke zu schließen, habe ich eine Wrapper-Bibliothek geschrieben, um gegen die von Microsoft bereit gestellte Schnittstelle einfacher programmieren zu können. Dazu habe ich noch viele Snippets und Beispielcodings hinzugefügt, die das Benutzen der Wrapper-Bibiliothek "SSISComponentWrap" erklärt.

## Sources

Das komplette Projekt findet man hier: 
(https://github.com/roadrunnerlenny/programmingSSIS)