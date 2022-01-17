# Ontologie
## Author: Niklas Kiefer
## Begriffserklärung
Der Begriff **Ontologie** in der Informatik steht für die formale Beschreibung von Ausdrücken und daraus folgend deren Relation in bestimmten Fachbereichen. Der Anwendungsbereich von Ontologien erstreckt sich über das Sammeln von Wissensbeständen bis hin zum Aufdecken neuer verborgener Informationen in bestehenden Datenbeständen.
Als formale Sprache der Ontologien wird OWL verwendet. Als Referenz für die hier dargestellten Informationen dient die [W3C Spezifikation](https://www.w3.org/TR/owl-ref/)
## OWL
OWL steht für *Web Ontology Language* ist eine Sprache, die auf dem **Ressource Description Framework** aufbaut und wird zum Erstellen von Ontologien verwendet.
Der Name OWL wird mit dem englischen Wort für Eule in Verbindung gebracht und soll für Weisheit stehen. Dies impliziert die Zweck hinter OWL, Wissen zu sammeln und in einer formalen Sprache zu definieren. Ähnlich wie beim Programmieren wird mit Hilfe von Klassen eine Hierarchie abgebildet.  
  
OWL wurde in 3 verschiedenen Version erstellt, welche mit bestimmten Zielgruppen im Sinn entwickelt wurden:
* **OWL Lite** - Stellt eine eingeschränkte Untermenge von OWL dar, welche nur simple Klassifikationshierarchi erlaubt. Es wurde in erster Linie für simplere Projekte entwickelt.
* **OWL DL** - DL steht in diesem Fall für *"description logic"*. Diese Version wird verwendet für maximale Ausdrucksstärke mit zusätzlicher Möglichkeit der Schlussfolgerungen aus den Daten 
* **OWL Full** - Diese Version ermöglicht maximale Ausdrucksstärke, jedoch gibt es keine eindeutige Möglichkeit der Schlussfolgerungen.

OWL ermöglicht nun diverse Spezifikationen für Klassen und deren Properties. Hier werden nun wichtige Elemente gelistet:
| Name             | Syntax              | Beschreibung                                                      |
|------------------|---------------------|-------------------------------------------------------------------|
| Class            | owl:Class           | Erstellt eine Klasse                                              |
| Equivalent Class | owl:equivalentClass | Gibt an, dass eine Klasse equivalent zu einer anderen Klasse ist. |
| Disjoint with    | owl:disjointWith    | Gibt an, dass eine Klasse nicht gleich einer anderen Klasse ist.  |
| Inverse of       | ow:inverseOf        | Gibt an, dass eine Beziehung zwischen Properties invertiert ist.  |
| subClassOf       | owl:subPropertyOf   | Eine Property ist abgeleitet von einem anderen Property.          |


Dies sind natürlich bei weitem nicht alle Properties, die OWL ermöglicht. Sie sollen nur einen wichtigen Anteil der Möglichkeiten erläutern, die man mit OWL zur Erstellung einer Ontologie vorgegeben hat.

# Syntax
Um nun die Ontologie besser zu verstehen folgt nun ein kleines Beispiel, dass die Syntax erläutern soll.
Für die Darstellung von OWL gibt es mehrere Syntaxen:
* RDF/XML Syntax
* OWL2 Functional Syntax
* OWL2 XML Syntax
* RDF/Turtle Syntax
* Manchester Syntax

Für folgende Beispiele wird die RDF/XML Syntax verwendet. Andere Syntaxen werden in diesem Tutorial nicht weiter erläutert.  
Zuerst folgt nun die Erstellung einer neuen Ontologie:
```
<?xml version="1.0"?>
<rdf:RDF xmlns="http://www.semanticweb.org/TestOntologie"
     xml:base="http://www.semanticweb.org/TestOntologie"
     xmlns:owl="http://www.w3.org/2002/07/owl#"
     xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
     xmlns:xml="http://www.w3.org/XML/1998/namespace"
     xmlns:xsd="http://www.w3.org/2001/XMLSchema#"
     xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#">
    <owl:Ontology rdf:about="http://www.semanticweb.org/TestOntologie"/>
    ...
</rdf:RDF>

```

## Inferenz 
Der Begriff der Inferenz steht das explizit machen von verborgenen Informationen. Sie wird in einer Ontologie verwendet um Schlussfolgerungen aus bestehenden Daten zu ziehen.
## Semantic Reasoner
