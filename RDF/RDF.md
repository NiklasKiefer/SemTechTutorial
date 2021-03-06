# RDF
### Author: Niklas Kiefer
Als Referenz für diese Zusammenfassung dient die [W3C Dokumentation](https://www.w3.org/RDF/)  und [RDF Primer](https://www.w3.org/TR/rdf11-primer/#bib-RDF11-MT)
  
RDF steht für *Resource Description Framework* und ist ein Framework, welches vom World Wide Web Consortium **W3C** entwickelt wurde, um Informationen über verschiedenste Ressourcen zu sammeln und zu standardisieren. Als Ressource kann hierbei alles mögliche dienen, wie zum Beispiel Personen, Gegenstände, Gebäude, abstrakte Konzepte und vieles mehr. RDF bildet den Grundstein des Semantic Web und dient dazu, mit einer einheitlichen Schreibweise Informationen einfacher von Maschinen verwertbar zu machen, ohne dabei einen Verlust an Informationen zu erhalten.


## Triple
Um die Informationen dann zu vernetzen und zu standardisieren wird eine besondere Datenstruktur verwendet, die sich **Triple** nennt. Ein Triple enthält, wie der Name schon verrät, 3 Teile, die zusammen die Information ergeben:

* **Subjekt** - stellt eine Ressource dar (kann IRI oder blank node sein)
* **Prädikat** - stellt Subjekt in Relation zu Objekt (kann IRI sein)
* **Objekt** - stellt ein Objekt dar, dass in Relation zur Ressource gestellt wird. Kann ebenfalls eine Ressource sein (kann IRI, Literal oder blank node sein)

Es folgt nun ein Beispiel für Triples programmiert in C# mit dotNetRDF. Dieses Beispiel wird im [RDF Primer](https://www.w3.org/TR/rdf11-primer/#section-triple) ebenfalls dargestellt.

```C#
using System;
using VDS.RDF;
using VDS.RDF.Writing;

namespace RDFExamples
{
    internal class Program
    {
        static void Main(string[] args)
        {
            IGraph graph = new Graph();

            // Triple <Bob> <is a> <person>
            IUriNode Subject = graph.CreateUriNode(UriFactory.Create("http://example.org/Bob"));
            IUriNode Predicate = graph.CreateUriNode(UriFactory.Create("http://example.org/isA"));
            IUriNode Object = graph.CreateUriNode(UriFactory.Create("http://example.org/person"));
            graph.Assert(new Triple(Subject, Predicate, Object));

            // Triple <Bob> <is a friend of> <Alice>
            Subject = graph.CreateUriNode(UriFactory.Create("http://example.org/Bob"));
            Predicate = graph.CreateUriNode(UriFactory.Create("http://example.org/isAFriendOf"));
            Object = graph.CreateUriNode(UriFactory.Create("http://example.org/Alice"));
            graph.Assert(new Triple(Subject, Predicate, Object));

            // Triple <Bob> <is born on> <the 4th of July 1990>. 
            Subject = graph.CreateUriNode(UriFactory.Create("http://example.org/Bob"));
            Predicate = graph.CreateUriNode(UriFactory.Create("http://example.org/isBornOn"));
            Object = graph.CreateUriNode(UriFactory.Create("http://example.org/The4thOfJuly1990"));
            graph.Assert(new Triple(Subject, Predicate, Object));

            // Triple <Bob> <is interested in> <the Mona Lisa>.
            Subject = graph.CreateUriNode(UriFactory.Create("http://example.org/Bob"));
            Predicate = graph.CreateUriNode(UriFactory.Create("http://example.org/isInterestedIn"));
            Object = graph.CreateUriNode(UriFactory.Create("http://example.org/theMonaLisa"));
            graph.Assert(new Triple(Subject, Predicate, Object));

            // Triple <the Mona Lisa> <was created by> <Leonardo da Vinci>.
            Subject = graph.CreateUriNode(UriFactory.Create("http://example.org/theMonaLisa"));
            Predicate = graph.CreateUriNode(UriFactory.Create("http://example.org/wasCreatedBy"));
            Object = graph.CreateUriNode(UriFactory.Create("http://example.org/LeonardoDaVinci"));
            graph.Assert(new Triple(Subject, Predicate, Object));

            // Triple <the video 'La Joconde à Washington'> <is about> <the Mona Lisa>
            Subject = graph.CreateUriNode(UriFactory.Create("http://example.org/video/LaJocondeÀWashington"));
            Predicate = graph.CreateUriNode(UriFactory.Create("http://example.org/isAbout"));
            Object = graph.CreateUriNode(UriFactory.Create("http://exampe.org/TheMonaLisa"));
            graph.Assert(new Triple(Subject, Predicate, Object));

            // Ausgeben des Triples in der Konsole
            foreach (Triple t in graph.Triples)
            {
                Console.WriteLine(t.ToString());
            }
        }
    }
}
```
Der daraus entstehende Output folgende Triples:
```
http://example.org/Bob , http://example.org/isA , http://example.org/person
http://example.org/Bob , http://example.org/isAFriendOf , http://example.org/Alice
http://example.org/Bob , http://example.org/isBornOn , http://example.org/The4thOfJuly1990
http://example.org/Bob , http://example.org/isInterestedIn , http://example.org/theMonaLisa
http://example.org/theMonaLisa , http://example.org/wasCreatedBy , http://example.org/LeonardoDaVinci
http://example.org/video/LaJoconde%C3%80Washington , http://example.org/isAbout , http://exampe.org/TheMonaLisa
```


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

## RDF Graphen
Wenn man eine Menge an Tripeln hat, kann man diese in einem gerichteten Graph speichern und auch darstellen.  
Für die Serialisierung dieser Graphen werden diverse Technologien von W3C im RDF Primer definiert:

* Turtle
* JSON-LD - JSON basiert
* RDFa - HTML basiert
* N-Triples
* RDF/XML - XML basiert

Zum Verständnis erfolgt nun eine simple Implementierung eines RDF Graphen mit Hilfe von dotNetRDF anschließend wird dieser serialisiert.  
Der folgende Code erstellt einen Graphen bestehend aus 2 Tripeln, die Informationen über den Mount Everset enthalten, und gibt den Graphen in Form einer Turtle Serialisierung aus.
```c#
using System;
using VDS.RDF;
using VDS.RDF.Writing;

namespace RDFExamples
{
    internal class Program
    {
        static void Main(string[] args)
        {
            // Erstellen des Graphen
            IGraph graph = new Graph();
            graph.BaseUri = new Uri("http://example.org/mountainGraph");

            // Erstellen eines Triples der Form <Mount Everest> <hasHeight> <8849 m>
            IUriNode mountEverest = graph.CreateUriNode(UriFactory.Create("http://example.org/mountains/Mount_Everest"));
            IUriNode hasHeight = graph.CreateUriNode(UriFactory.Create("http://example.org/hasHeight"));
            ILiteralNode height = graph.CreateLiteralNode("8849 m");

            // Einfügen des Triples 
            graph.Assert(new Triple(mountEverest, hasHeight, height));

            // Erstellen und Einfügen eines Tripels der Form <Mount Everest> <isA> <Mountain>
            IUriNode isA = graph.CreateUriNode(UriFactory.Create("http://example.org/isA"));
            IUriNode mountain = graph.CreateUriNode(UriFactory.Create("http://example.org/mountain"));

            graph.Assert(new Triple(mountEverest, isA, mountain));

            // Serialisieren des Graphen in Turtle
            TurtleWriter turtlewriter = new TurtleWriter();
            System.IO.StringWriter stringwriter = new System.IO.StringWriter();

            turtlewriter.Save(graph, stringwriter);

            String data = stringwriter.ToString();
            Console.WriteLine(data);
        }
    }
}
```
Die dabei erstellte Turtle-Serialisieren sieht folgendermaßen aus:

```turtle
@base <http://example.org/mountainGraph>.

@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

<http://example.org/mountains/Mount_Everest> <http://example.org/hasHeight> "8849 m";
                                             <http://example.org/isA> <http://example.org/mountain>.
```
Der selbe Graph kann nun auch in anderen Darstellungsformen serialisiert werden. In RDF/XML sieht er so aus:

```XML
<?xml version="1.0" encoding="utf-16"?>
<!DOCTYPE rdf:RDF [
        <!ENTITY rdf 'http://www.w3.org/1999/02/22-rdf-syntax-ns#'>
        <!ENTITY rdfs 'http://www.w3.org/2000/01/rdf-schema#'>
        <!ENTITY xsd 'http://www.w3.org/2001/XMLSchema#'>
]>
<rdf:RDF xml:base="http://example.org/mountainGraph" xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#" xmlns:xsd="http://www.w3.org/2001/XMLSchema#" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
  <rdf:Description rdf:about="http://example.org/mountains/Mount_Everest">
    <ns0:hasHeight xmlns:ns0="http://example.org/">8849 m</ns0:hasHeight>
    <ns1:isA rdf:resource="http://example.org/mountain" xmlns:ns1="http://example.org/" />
  </rdf:Description>
</rdf:RDF>
```

In JSON sieht der Graph nun so aus:
```JSON
{
  "http://example.org/mountains/Mount_Everest": {
    "http://example.org/hasHeight": [
      {
        "value": "8849 m",
        "type": "literal"
      }
    ],
    "http://example.org/isA": [
      {
        "value": "http://example.org/mountain",
        "type": "uri"
      }
    ]
  }
}
```
In HTML sieht der Graph so aus:
```HTML
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML+RDFa 1.0//EN" "http://www.w3.org/MarkUp/DTD/xhtml-rdfa-1.dtd">
<html>
        <head>
                <title>
                        RDF Graph - http://example.org/mountainGraph</title>
        </head>
        <body>
                <h3>
                        RDF Graph - http://example.org/mountainGraph</h3>
                <table width="100%">
                        <thead>
                                <tr>
                                        <th>
                                                Subject</th>
                                        <th>
                                                Predicate</th>
                                        <th>
                                                Object</th>

                                </tr>

                        </thead>
                        <tbody>
                                <tr valign="top">
                                        <td rowspan="2">

                                                <a class="uri" href="http://example.org/mountains/Mount_Everest">
                                                        http://example.org/mountains/Mount_Everest</a>
                                        </td>
                                        <td rowspan="1">
                                                <a class="uri" href="http://example.org/hasHeight">
                                                        http://example.org/hasHeight</a>
                                        </td>
                                        <td>
                                                <span about="http://example.org/mountains/Mount_Everest" xmlns:ns0="http://example.org/" property="ns0:hasHeight" class="literal">8849 m</span>
                                        </td>
                                </tr>
                                <tr valign="top">
                                        <td rowspan="1">
                                                <a class="uri" href="http://example.org/isA">
                                                        ns0:isA</a>
                                        </td>
                                        <td>
                                                <a about="http://example.org/mountains/Mount_Everest" xmlns:ns0="http://example.org/" rel="ns0:isA" class="uri" href="http://example.org/mountain">
                                                        ns0:mountain</a>
                                        </td>
                                </tr>
                        </tbody>
                </table>
        </body>
</html>
```
Es werden noch andere Darstellungsformen in dotNetRDF unterstützt, diese werden aber hier nicht mehr angeführt.

## SPARQL
SPARQL, wie auf [W3C](https://www.w3.org/TR/sparql11-overview/) definiert, ist eine Abfragesprache ähnlich wie SQL, mit der RDF Graphen nach Daten abgefragt werden können.
Im folgenden wird ein Beispiel Graph erstellt und mit SPARQL abgefragt, um die Syntax zu zeigen. Der Code kommt von der [SPARQL Definition](https://www.w3.org/TR/sparql11-overview/#sparql11-query) auf w3c.org  
  
Zuerst benötigen wir einen Graphen. Der Beispielgraph stellt eine Gruppe von Menschen dar, die sich kennen. Hierfür wird das [FOAF Vokabular](http://xmlns.com/foaf/spec/) verwendet.
```
 @prefix foaf: <http://xmlns.com/foaf/0.1/> .
 @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

 <http://example.org/alice#me> a foaf:Person .
 <http://example.org/alice#me> foaf:name "Alice" .
 <http://example.org/alice#me> foaf:mbox <mailto:alice@example.org> .
 <http://example.org/alice#me> foaf:knows <http://example.org/bob#me> .
 <http://example.org/bob#me> foaf:knows <http://example.org/alice#me> .
 <http://example.org/bob#me> foaf:name "Bob" .
 <http://example.org/alice#me> foaf:knows <http://example.org/charlie#me> .
 <http://example.org/charlie#me> foaf:knows <http://example.org/alice#me> .
 <http://example.org/charlie#me> foaf:name "Charlie" .
 <http://example.org/alice#me> foaf:knows <http://example.org/snoopy> .
 <http://example.org/snoopy> foaf:name "Snoopy"@en .
```
Nun können wir mit SPARQL diesen Graphen abgragen. Die folgende Abgrage liefert die Namen aller Personen und die Anzahl der Freunde von der jeweiligen Person.
```SPARQL
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
SELECT ?name (COUNT(?friend) AS ?count)
WHERE { 
    ?person foaf:name ?name . 
    ?person foaf:knows ?friend . 
} GROUP BY ?person ?name
```

Zur Demonstration folgt nun noch die Implementierung der gerade genannten SPARQL Abfrage in C# mit dotNetRDF:
```C#
using System;
using VDS.RDF;
using VDS.RDF.Parsing;
using VDS.RDF.Query;
using VDS.RDF.Writing;

namespace RDFExamples
{
    internal class Program
    {
        static void Main(string[] args)
        {
            IGraph graph = new Graph();

            // Erstellen des Graphen aus einem String (alternativ kann auch aus einer Datei gelesen werden)
            string data = "@prefix foaf: <http://xmlns.com/foaf/0.1/> . \n"
                        + "@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .\n\n"
                        + "<http://example.org/alice#me> a foaf:Person .\n"
                        + "<http://example.org/alice#me> foaf:name \"Alice\" .\n"
                        + "<http://example.org/alice#me> foaf:mbox <mailto:alice@example.org> .\n"
                        + "<http://example.org/alice#me> foaf:knows <http://example.org/bob#me> .\n"
                        + "<http://example.org/bob#me> foaf:knows <http://example.org/alice#me> .\n"
                        + "<http://example.org/bob#me> foaf:name \"Bob\" .\n"
                        + "<http://example.org/alice#me> foaf:knows <http://example.org/charlie#me> .\n"
                        + "<http://example.org/charlie#me> foaf:knows <http://example.org/alice#me> .\n"
                        + "<http://example.org/charlie#me> foaf:name \"Charlie\" .\n"
                        + "<http://example.org/alice#me> foaf:knows <http://example.org/snoopy> .\n"
                        + "<http://example.org/snoopy> foaf:name \"Snoopy\"@en .";

            // Parsen des Strings in den Graphen.
            StringParser.Parse(graph, data);

            // Erstellen des SPARQL Ausdrucks als String.
            string query = @"PREFIX foaf: <http://xmlns.com/foaf/0.1/>
                            SELECT ?name(COUNT(?friend) AS ?count)
                            WHERE {
                                ?person foaf:name ?name .
                                ?person foaf:knows ?friend .
                            }
                            GROUP BY ?person ?name";


            // Ausführen der Abfrage
            var results = graph.ExecuteQuery(query);

            // Auswerten des Ergebnisses (Typ des Results muss überprüft werden)
            if (results is SparqlResultSet)
            {
                SparqlResultSet rset = (SparqlResultSet)results;
                foreach (SparqlResult result in rset)
                {
                    Console.WriteLine(result.ToString());
                }
            }
        }
    }
}
```
Wenn man nun diese Abfrage ausführt, erhält man folgendes Ergebnis:

```
?name = Alice , ?count = 3^^http://www.w3.org/2001/XMLSchema#integer
?name = Charlie , ?count = 1^^http://www.w3.org/2001/XMLSchema#integer
?name = Bob , ?count = 1^^http://www.w3.org/2001/XMLSchema#integer
```
Im Ergebnis kann man nun erkennen, dass Alice 3 Freunde hat, und sowohl Charlie als auch Bob einen Freund hat.
