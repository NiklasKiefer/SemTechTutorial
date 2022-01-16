# RDF
### Author: Niklas Kiefer
Als Referenz für diese Zusammenfassung dient W3C: https://www.w3.org/RDF/  
  
RDF steht für *Resource Description Framework* und ist ein Framework, welches vom World Wide Web Consortium **W3C** entwickelt wurde, um Informationen über verschiedenste Ressourcen zu sammeln und zu standardisieren. Als Ressource kann hierbei alles mögliche dienen, wie zum Beispiel Personen, Gegenstände, Gebäude, abstrakte Konzepte und vieles mehr. RDF bildet den Grundstein des Semantic Web und dient dazu, mit einer einheitlichen Schreibweise Informationen einfacher von Maschinen verwertbar zu machen, ohne dabei einen Verlust an Informationen zu erhalten.


## Triple
Um die Informationen dann zu vernetzen und zu standardisieren wird eine besondere Datenstruktur verwendet, die sich **Triple** nennt. Ein Triple enthält, wie der Name schon verrät, 3 Teile, die zusammen die Information ergeben:

* **Subjekt** - stellt eine Ressource dar (kann IRI oder blank node sein)
* **Prädikat** - stellt Subjekt in Relation zu Objekt (kann IRI sein)
* **Objekt** - stellt ein Objekt dar, dass in Relation zur Ressource gestellt wird. Kann ebenfalls eine Ressource sein (kann IRI, Literal oder blank node sein)

Ein Beispiel für ein Triple wäre folgendes: ***(Mount Everest) (isA) (Mountain)***

Die entstehende Information aus den Triples stellt einen gerichteten Graphen dar. Durch diese Struktur kann es außerdem ermöglicht werden, Zusammenhänge zwischen verschiedenen Triples zu erkennen. Die Daten innerhalb des Triples kann eine von 3 verschiedenen Typen sein:

* **IRI** - Ist eine Erweiterung einer URI (Uniform Ressource Identifier). Im Unterschied zu URI verwendet eine IRI auch Zeichen, die nicht Teil von ASCII sind, damit sie globale Anwendung finden kann. Beispiel: *http://example.org/FHWN* kann als IRI für die FH betrachtet werden.
* **Literal** - Sind Werte wie Zeichenketten, Datum oder Zahlenwerte 
* **Blank Node** - Wird verwendet, wenn keine offizielle IRI für eine Ressource vorhanden ist. Wird auch anonyme Ressource genannt.

## RDF Vokabular
Als ein Vokabular in RDF wird eine Sammlung an IRIs bezeichnet, welche in RDF Graphen verwendet werden können. Ein Beispiel hierfür ist RDF-Schema. Dieses Vokabular definiert verschiedene IRIs für die Modellierung von Datenstrukturen wie Klassen und Eigenschaften innerhalb von RDF:
| Name          | Syntax                  | Beschreibung                                                            |
|---------------|-------------------------|-------------------------------------------------------------------------|
| Resource      | rdfs:Resource           | Alles, was in RDF beschrieben wird, ist eine Ressource.                 |
| Class         | rdfs:Class              | Eine RDF Ressource ist eine Klasse.                                     |
| Property      | rdfs:Property           | Eine RDF Ressource ist eine Eigenschaft einer anderen Ressource.        |
| Type          | R rdfs:type C           | Eine Ressource R ist vom Typ einer Klasse C.                            |
| subClassOf    | C1 rdfs:subClassOf C2   | Eine Klasse C1 ist eine Subklasse von einer Klasse C2.                  |
| subPropertyOf | P1 rdf:subPropertyOf P2 | Eine Eigenschaft ist eine Subeigenschaft von einer Eigenschaft P2.      |
| Comment       | R rdfs:comment L        | Eine Ressource R erhält ein Literal L als Beschreibung für den Menschen |

Die Tabelle zeigt nur einen kleinen Teil von RDF Schema. Weitere Datentypen können hier nachgelesen werden: https://www.w3.org/TR/2014/REC-rdf-schema-20140225/  

Andere Beispiele für Vokabulare sind folgende:

* Friend of a Friend (FOAF) http://xmlns.com/foaf/spec/ - Kann für soziale Netze verwendet werden.
* schema.org https://schema.org/ - Wird bei Webseiten verwendet, damit Suchmaschinen den Inhalt der Seite verstehen können.
* Dublin Core https://www.w3.org/wiki/DublinCore - Wird für die Beschreibung elektronischer Ressourcen verwendet.
