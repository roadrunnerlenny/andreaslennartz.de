---
title: "WPF Fundamentals"
draft: false
---

# Allgemeine Infos

## Projektidee

Die Idee hinter Bibliothek ist relativ einfach - eine Sammlung grundlegender Funktionen die man bei der täglichen Arbeit mit WPF benötigt. 

## Übersicht

- Basisklassen zur Abbildung vom Model - View - ViewModel - Presenter Pattern
- DelegateCommand - eine Erweiterung der ICommand Schnittstelle
- SyncedList, eine Möglichkeit Listen zwischen Model und ViewModel synchron zu halten
- Verschiedene Converter (BooleanConverter, NullableConverters, ListToStringConverter, DebugConverter)
- Verschieden Hilfsklassen / Erweiterungsklassen (DispatcherExtensions, EnumerableExtensions, ExceptionHelper)
- DeferredAction, verzögert die Ausführung von beliebigen Code
- PopupButton, eine einfacher Weg um z.B. Hilfefenster anzuzeigen
- SelectionCombo, ein ComboBox die eine Mehrfachauswahl zulässt (auch hierarchische Strukturen werden unterstützt)
- SpinningControl, ein drehender Kreis als Warteanzeige

## Quellcode / Binaries

Der aktuelle Quellcode und die Binaries liegen auf GitHub: (github.com/roadrunnerlenny/wpffundamentals)

## Klassenübersicht

Eine grobe Übersicht über die verwendeten Klassen zeigt die nachfolgende Grafik.
{{< figure src="/dotnet/wpffundamentals/ClassOverview.png" >}}

# Details der einzelnen Elemente

## Model - View - ViewModel - Presenter und Commands

Um die volle Funktionalität von WPF nutzen zu können, empfiehlt es sich bei der Programmierung das Model - View - ViewModel - Presenter Pattern einzusetzen - auch bekannt als MVP. Dies leitet sich vom MVVM Pattern (Model - View - ViewModel) ab, und erweitert es um das Presenter-Objekt. 
Einer der bekanntesten Artiekl zum Thema MVVM findet sich auf den Seiten von Microsoft: 

(http://msdn.microsoft.com/de-de/magazine/dd419663.aspx)

Die Erweiterung um die Presenter-Logik hat sich in der Community inzwischen durchgesetzt und kann als de-facto Standard für die WPF Programmierung angesehen werden. 
Da es noch keine verbreiteten generischen Klassen zur Umsetzung dieses Patterns gibt, findet sich in der WPF Fundamentals Bibliothek Basisklassen für ViewModel, Presenter sowie das DelegateCommand. 

## SyncedList

Ein Hauptproblem bei der Umsetzung des MVVM oder MVP - Patterns ist die Synchronisation von Listen zwischen dem Model und dem ViewModel. Mit Hilfe der SyncedList synchronisiert sich das Model immer selbstständig mit dem ViewModel - d.h. Änderungen an der Oberflächen die an eine Liste im ViewModel gebunden sind werden auch direkt im Model sichtbar. 

## Converter-Bibliothek

Die in der Bibliothek vorhandenen Converter werden häufig in WPF Projekten benötigt.

### BooleanConverter

Konvertiert einen bool-Datentyp in einen beliebiegen String oder Objekt - sehr hilfreich  man z.B. die Visibility eines Frameworkelements an ein bool binden möchte.

### NullableConverter

Textboxen mit Bindungen an Nullable Basistypen sind problematisch, wenn die gebundene Textbox geleert wird. Der NullableConvert konvertiert einen leere Eingabe in Textbox in eine "richtige" null des entsprechenden BasisTypen, so dass die Bindung richtig funktioniert.

### ListToStringConverter

OneWayConverter - konvertiert eine beliebige List in einen langen String, bei dem man ein Trennzeichen sowie den Standardwert bei einer leeren Liste mit angeben kann. 

### DebugConverter

Kapselt einen System.Diagnostics.Debugger.Break() innerhalb des Converters - im Debug-Modus wird dies wie ein Breakpoint behandelt. 

## DeferredAction

Die Ausführung einer beliebiegen Action wird um eine vom Typ TimeSpan angegebene Zeit verlängert. Falls notwendig, kann die Wartezeit immer wieder erhöht werden, um so die Ausführung immer weiter nach hinten zu schieben. 

## PopupButton

Ein beliebieges XAML-Element kann (z.B. ein Bild) wird beim nutzen dieses CustomControls zu einer Art Button - beim Drücken des Buttons wird entsprechend ein Popup angezeigt, dessen Inhalt innerhalb dieses CustomControls ebenfalls definiert wird. 

## SelectionCombo

Dieses UserControl ist eine ComboBox, die aber Mehrfachauswahlen zulässt. Ausserdem können die Auswahlfelder auch hierarchisch verschachtelt werden. 

## SpinningControl

Dieses CustomControl zeigt einen sich drehenden Kreis, welches z.B. als Ersatz für die klassische Sanduhr als Warteanzeige benutzt werden kann.