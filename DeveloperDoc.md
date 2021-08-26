# Chatbot  
  
## Dokumentation  
  
1. [Algorithmus](#fragen-algorithmus-intentfinderjava)  
  
## Fragen Algorithmus `IntentFinder.java`  
  
Die `IntentFinder` Klasse hat folgende Funktionen:  
  
1. [`search()`](#methode-searchstring-input-boolean-affectstatistics) Eine Methode um die Antwort auf einen String zu  
   Finden  
2. `findAnswer()` Ein WebService um die `search()` Methode in JavaScript zu fetchen  
  
### Methode `search(String input, boolean affectStatistics)`  
  
#### Parameter:  
  
1. **input**: Ist der String, für welchen die Antwort gesucht wird.  
2. **affectStatistics**: ein boolean, welcher bestimmt ob die Statistiken in der Datenbank beeinflusst werden sollen.
Zu den Statistiken gehören beantwortete und unbeantwortete Fragen und der Zähler wie viele Antworten geschickt w
  
#### Beschreibung:  
  
In der `static` importierten Funktion `printDebug()` wird der input String auf die maximale Länge gekürzt und alle  
speziellen chars werden entfernt.  
  
Am Anfang werden alle geblacklisteten Wörter im String ignoriert. Danach Loopen wird durch alle Wörter im input und alle  
Tags in der Datenbank. Um die beiden Wörter (Wort, Tag) zu vergleichen benutzen wir den Levenshtein Algorithmus. Dieser  
findet heraus, wie viele Änderungen an einem String gemacht werden müssen, um einen anderen zu erhalten. In der  
Funktion `CalculateRaing.getLevenshteinDistance()` teilen wir die erhaltene Levenshtein Distanz dann durch die grössere  
Länge der beiden Strings, wie hier im Beispiel zu sehen ist.  
  
Falls der erhaltene Wert über dem Wert der Variable `levenshteinMatch` (im Moment 0.6) liegt, haben wir ein ähnliches  
Wort gefunden. Für alle Resultate, welche den übersetzten Tag erhalten wird ein `WordLevenShteinDistance` Objekt  
erstellt. Diese Klasse enthält das gefundene Wort, den `ResultParent` und die levenshtein Distanz. Im Konstruktor wird  
ausserdem geschaut, ob es für dieses Wort und Tag bereits ein `Match`gibt. Falls noch keins vorhanden wird, wird es  
erstellt.  
  
# @zwazel chasch du Zeile 133 - 183 beschriebe?




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI4MDg1MTQ5MSw5NTE5ODUwNzQsNzM3OT
QzODA0LDM4MzIzMTYyMCwtMzIzNTA0NjgyLC0xNzA5Mjc1NDgz
XX0=
-->