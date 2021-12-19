---
title: "Hunt the nuts - Hintergründe"
draft: false
---

## Motivation

Mein erstes Spiel in Silverlight. 

## Klassenübersicht

Im folgenden Bild ist eine Übersicht über alle Klassen zu sehen. Hier kann man gut erkennen das der relevante Code für die Oberfläche durch Vererbung von der eigentlich Spielelogik getrennt wurde. Die Klassen, welche ausschließlich Code für die Oberfläche bereit halten, beginnen mit SL. 

{{< figure src="/dotnet/huntthenuts/huntthenuts/ClassDiagram.png" >}}
 
Im nachhinein vielleicht nicht der glücklichste Ansatz, um eine Kapselung der Spielelogik und der Oberfläche abzubilden, aber für ein Projekt dieser Größenordnung durchaus vertretbar.

## Unclean Code

Das Spiel habe ich programmiert noch bevor ich ein Code-Clean kannte. Das bedeutet jetzt nicht das es schlecht programmiert wurde - die Spiellogik an sich ist recht passabel. Aber als inzwischen überzeugter Clean-Code-Anhänger würde ich in Hinblick auf die Lesbarkeit des Codes für andere doch ein paar Dinge anders machen.

## Open Source

Der Code liegt auf GitHub unter (github.com/roadrunnerlenny/huntthenuts)
