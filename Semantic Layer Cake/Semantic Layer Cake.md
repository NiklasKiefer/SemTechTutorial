# Semantic Layer Cake
## Author: Christoph Hofer

### Übersicht

Der Semantic Layer Cake soll den Aufbau und Architektur des Semantischen Webs darstellen. Der Layer Cake ist so aufgebaut, dass jede Schicht die darunterliegende Schicht(en) verwendet bzw. auf diese aufbaut. Die Illustration stellt eine Hierarchie von verschiedenen Sprachen / Technologien dar, die von unten nach oben aufeinander aufbauen. So bilden sozusagen die untersten Schichten des Layer Cakes das Fundament. 

![Semantic_web_stack svg](https://user-images.githubusercontent.com/91307869/149782138-f8ea30bd-d068-4e83-82fe-21eb9d2478fa.png)

### Semantic Web

Das Internet, so wie wir es kennen, ist zum Größtenteil eine Sammlung bzw. eine Bibliothek von Daten die vielleicht für den Menschen lesbar und interpretierbar ist, aber nicht für den Computer selber. Ein Mensch erkennt den Unterschied zwischen einem Apfel und einer Birne, ein Computer kann soetwas nicht.
Das Semantische Web ist eine Vision von einem Internet, wo der Inhalt semantisch (aussagend) ist und Informationen und Daten in Beziehung miteinander gestellt werden können. Das Internet soll so von einem umstruktiertem Haufen von Daten zu einem strukuriertem, organisiertem Netz von Daten und Informationen zusammengeschnürrt werden. Ziel ist es Informationen sowohl dem Menschen, als auch dem Computer lesbar und interpretierbar zu machen.
Auf dem ersten Blick scheint so etwas überflüssig, aber so ein Web könnte viele neue Möglichkeiten mit sich bringen: Ein gutes Beispiel ist eine Vergleichsplattform. Nehmen wir an Sie wollen eine neue Immobilienvergleichsplattform veröffentlichen, welche sämtliche Angebote von verschiedenen Seiten zusammensucht und dem User darstellt. Ein Weg nun die richtigen Informationen von einer Seite A zu extrahieren, ist es sich manuell den Aufbau der Seite anzusehen und sozusagen "per Hand" die relevanten Informationen herauszufischen und dem Computer dann mitzuteilen wo er die Daten auf dieser Seite findet.
Dieses Vorgehen ist extrem zeitintensiv und uneffizient und muss für jede neue Website wiederholt werden. Wenn man effektiv soviele Angebote wie möglich von diversen Seiten zusammensuchen möchte, muss das maschinell passieren. Aber wie kann ein
Computer eine Website selber interpretieren? Eine Lösung wäre es, wenn Entwickler der Seiten die relevante Information in einer Form bereitstellen die standardisiert überall im Web verfügbar ist. Nun kann die Vergleichsplattform von jeder Seite die Angebote herausfiltern, der Computer versteht Zusammenhänge und Informationen. Die jeweiligen Seiten haben semantischen Inhalt, dem Inhalt wurde Ausdruck verliehen, der Computer kann diese lesen und vorallem interpretieren. Das semantic Web kann aber nur funktionieren wenn es einheitlich funktioniert, d.h dass Technologien und Darstellungsformate standardisiert sind. Das semantische Web beruht auf einer Idee von Tim Berners-Lee, dem Begründer des WWW.

### Layers

#### Fundament

Wie bereits angesprochen bilden die unteren Schichten des Layercakes das Fundament des semantischen Webs. 

* UNICODE - Unicode ist ein Standard der festgibt wie Zahlen, Buchstaben und andere Zeichen elektronisch gespeichert werden. Damit sie auf dem Handy, Tablet oder Computer richtig wiedergeben kann. Um Unicode Zeichen in binär Zahlen umzuformen bedient man sich ***Unicode Transformation Format*** (UTF).
* XML - Eine Auszeichnungssprache um hierarchisch strukturierte Daten zu beschreiben. XML an sich tut nicht viel, ist aber für den Datenaustausch essentiell.
* URI - Ein Uri (Universal Resource Identifier) ist eine Bezeichnung bzw. ein Identifikator für eine bestimmte Resource im Web. Gebraucht wird dieser im semantischen Web um semantische Inhalte genau zu identifizieren / lokalisieren.

#### Mittelschicht

Die Mittelschicht des Layer Cakes besteht aus Technologien die von der ***W3C*** standardisiert wurden um semantische Inhalte zu generieren.

* RDF - Mittels RDF (Resource Description Framework) lassen sich Inhalte im Web mittels Tripeln verknüpfen und geben dem Inhalt eine Semantik.
* OWL - Die Web Ontology Language zielt darauf ab, das RDF Framework mit Constraints und ähnlichem zu erweitern.
* SPARQL - SPARQL wird als Query Language benutzt um Informationen aus RDF Inhalten zu bekommen.

#### Obereste Schicht

* Vertrauen - Um sicherzugehen, dass Inhalte aus dem Web aus einer vertrauenswürdigen Quelle kommen.
* Menschliches Interface - Eine Schnittstelle, über der es für den User möglich ist, auf das semantische Web zuzugreifen. (Computer, Bildschirm...)





