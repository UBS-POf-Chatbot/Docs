# Chatbot

## Dokumentation

1. [Algorithmus](#fragen-algorithmus-intentfinderjava)

## Fragen Algorithmus `IntentFinder.java`

Die `IntentFinder` hat folgende Funktionen:

1. [`search()`](#methode-searchstring-input-boolean-affectstatistics) Eine Methode um die Antwort auf einen String zu  
   Finden
2. [`findAnswer()`](#methode-findanswerqueryparamq-string-input) Ein WebService um die `search()` Methode in JavaScript
   zu fetchen

### Methode `search(String input, boolean affectStatistics)`

#### Parameter:

- **input**: Ist der String, für welchen die Antwort gesucht wird.
- **affectStatistics**: ein boolean, welcher bestimmt ob die Statistiken in der Datenbank beeinflusst werden sollen

#### Beschreibung:

In der `static` importierten Funktion `prepareString()` wird der input String auf die maximale Länge gekürzt und alle  
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

Als nächstes wird die beste Antwort gesucht, indem durch `possibleAnswers` geloopt wird und falls das Rating einer
Antwort besser ist als der Wert von `float maxRating` wird `bestAnswer` und `maxRating` überschrieben.

Danach wird überprüft, ob `bestAnswer == null` ist, falls dies zutrifft wird die Frage (`String input`) in der Datenbank
als `UnansweredQuestion` gespeichert, und mit dem JSON String einer Antwort returned, welche nur null Werte und als text
404 beinhaltet. Anderenfalls wird die Anzahl Views der `bestAnswer` und des `ResultParent` in der Datenbank erhöht.

<!-- @zwazel falls du das mit de Statistike nu genauer wetsch chasch gäre mache -->
Ausserdem werden falls `affectStatistics == true` ist, werden die alle Statistiken in der Datenbank erhöht;

Zum Schluss wird noch mit dem JSON String der `bestAnswer` returned.

### Methode `findAnswer(@QueryParam("q") String input)`

#### Parameter:

- **q**: Ein GET Parameter aus dem HTTP Request, welcher die Frage des Users enthält

#### Beschreibung:

Diese Methode ruft `search(input, true)` auf, um die Antwort auf die Frage des Users zu erhalten und die Statistiken
anzupassen. Der erhaltene JSON String wird in eine HTTP Response mit dem status 200 verpackt und zurückgeschickt.
