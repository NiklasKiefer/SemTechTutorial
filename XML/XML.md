# XML
## Author: Christoph Hofer
### Übersicht
XML (**E**xtensible **M**arkup **L**anguage) ist eine genormte, erweiterbare Auszeichnungssprache um hierarchisch unterteile Strukturen in Form von Text sowohl Menschen als auch Maschinen lesbar zu machen. Sie wurde vom **World Wide Web Consortium** am 10. Februar 1998 veröffentlicht. Ein XML Dokument ist ein *self-describing document*, d.h der Inhalt des Dokuments dient nur dazu, dem Leser zu beschreiben was der Inhalt ist. XML ist keine Programmiersprache oder ähnliches, der alleinige Zweck ist es, Daten strukturiert und anschaulich zu beschreiben / darzustellen. XML ist erweiterbar - daher ***Extendable***.

### Aufbau
XML verwendet Tags. Ein Tag muss immer geöffnet und danach auch wieder geschlossen werden (Starttag, EndTag). Der Name des Tags, ist bis auf ein paar Ausnahmen, frei wählbar. Sehr empfehlenswert ist es aber, Namen zu wählen die auch zum Inhalt passen bzw. den Inhalt beschreiben. Zwischen den Tags kann man nun den Wert für den jeweiligen Tag angeben. Um eine hierarchische Struktur zu erzeugen, kann man Tags innerhalb von Tags eingeben. 

### Attribute
Ein Element kann ein oder mehrere Attribute haben, so kann ein Buch-Element z.B ein Attribut "Kategorie" haben, oder noch zusätzlich andere. Es wird aber nicht vorgeschrieben, ob oder wann man Attribute verwenden sollte, die gleiche Information lässt sich im Element oder Attribut speichern. Attribute haben den Nachteil, dass sie nicht mehrere Werte beinhalten können, bzw. sie lassen sich schlecht erweitern und können keine Struktur beschreiben.

### Document Type Definition

Ein **DTD** (Document Type Definition) gibt valide Elemente und Attribute innerhalb eines XML Dokuments an. Mittels DTD kann z.B eine Software erkennen, ob ein XML valide ist. Es wird auch verwendet um die Kommunikation zwischen 2 Gruppen zu standardisieren, indem man das DTD entsprechend setzt.

``` XML
<!ELEMENT note (to,from,heading,body)>
<!ELEMENT to (#PCDATA)>
<!ELEMENT from (#PCDATA)>
<!ELEMENT heading (#PCDATA)>
<!ELEMENT body (#PCDATA)>
```
---
Beispiel eines XML-Dokuments:
```XML
<?xml version="1.0" encoding="ISO-8859-1"?>
<bookstore>
  <book category="cooking">
    <title lang="en">Everyday Italian</title>
    <author>Giada De Laurentiis</author>
    <year>2005</year>
    <price>30.00</price>
  </book>
  <book category="children">
    <title lang="en">Harry Potter</title>
    <author>J K. Rowling</author>
    <year>2005</year>
    <price>29.99</price>
  </book>
  <book category="web">
    <title lang="en">Learning XML</title>
    <author>Erik T. Ray</author>
    <year>2003</year>
    <price>39.95</price>
  </book>
</bookstore>
```

#### Das Dokument als Graph:
![graph1](https://user-images.githubusercontent.com/91307869/150149049-1b024be2-31b1-439d-8b93-e18707daa9a7.png)

Es lässt sich also erkennen, dass die Struktur / Syntax von XML auch für den Menschen leicht zu lesen ist, selbst komplexere Strukturen lassen sich mit der Sprache klar darstellen. 

### Well Formed XML

Ein XML Dokument ist ***well formed*** wenn es folgende Regeln einbehält:

* Es muss für jeden Start-Tag ein End-Tag geben.
* Richtiges verschachteln der Tags: 

 ``` XML
 <tag1><tag2>Test</tag1></tag2>
```

Wäre falsch, richtig wäre es so:

 ``` XML
 <tag1><tag2>Test</tag2></tag1>
```


* In einem Element darf es nicht mehr als ein Attribut mit den gleichen Name geben.
* Es darf nur ein Root Element geben.

### XML im Web Layer Cake

XML wird benutzt um Beziehungen und Strukturen darzustellen. Eine Semantik bekommt die Struktur aber erst mittels [RDF](https://www.google.com). Vorteil ist es, eigene Tags zu definieren.
XML wird im Semantischen Web als standardisierte Syntax verwendet, noch dazu wird XML wird für den Datenaustausch zwischen Maschinen verwendet. Für den Fall, dass 2 verschiedene Domains für Elemente denselben Namen verwenden, lassen sich per XML Namespaces die einzelnen Elemente direkt ansprechen.  


