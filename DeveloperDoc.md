# Entwickler Dokumentation

In diesem Dokument wird beschrieben wie der Chatbot funktioniert und wo was zu finden ist, damit zukünftige Entwickler
ohne Probleme den Chatbot weiterentwickeln können. Dieses Dokument wird in drei Hauptteile aufgeteilt. Einmal allgemein,
der Chatbot an sich und den Adminbereich.

---

## Inhaltsverzeichnis

### [Allgemein](#general-section-start)<a name="tableofcontent-general"></a>

1. [Einleitung](#general-introduction)
2. [Technologien](#technologies)
    1. [Allgemein](#projekt-allgemein)
    2. [Backend](#backend)
    3. [Frontend](#frontend)
3. [Wichtige Klassen](#wichtige-klassen)
    1. [Datenbank Klassen](#datenbank-klassen)
    2. [Texte vorbereiten und reinigen](#texte-vorbereiten-und-reinigen)
        1. [prepareString](#preparestring)
        2. [shortenString](#shortenstring)
        3. [stringTooLong](#stringtoolong)
    3. [Datentypen Informationen](#datentypen-informationen)
4. [Allgemein wichtige Informationen](#allgemeine-wichtige-informationen)
    1. [Datenbank](#datenbank)
        1. [Hibernate konfigurieren](#hibernate-konfigurieren)
            1. [Verbindung zu Datenbank](#verbindung-zu-datenbank)
            2. [Weitere Konfigurationen](#weitere-konfigurationen)
        2. [C3PO konfigurieren](#c3po-konfigurieren)
            1. [Grösse des Pools](#die-grösse-des-pools-definieren)
            2. [Debug](#debug)
        3. [Datenbank Abfragen](#datenbank-abfragen)
    2. [Datenbank mit Testdaten befüllen](#datenbank-mit-testdaten-befüllen)
        1. [Testdaten ändern oder hinzufügen](#testdaten-ändern-oder-hinzufügen)
    3. [Chatbot Server Adresse definieren](#chatbot-server-adresse-definieren)
    4. [Antwort- und Tagtypen](#antwort--und-tagtypen)
        1. [Antworttypen](#antworttypen)
            1. [Default](#default)
            2. [Joke](#joke)
            3. [Facts](#facts)
            4. [Statistics](#statistic)
            5. [Error](#error)
        2. [Tagtypen](#tagtypen)
5. [Ideen für die Weiterentwicklung](#ideen-für-die-weiterentwicklung)

### [Chatbot](#chatbot-section-start)<a name="tableofcontent-chatbot"></a>

1. [Einleitung](#chatbot-introduction)
2. [Den Status überprüfen](#check-state)
    1. [Guter Status](#guter-status)
    2. [Schlechter Status](#schlechter-status)
3. [Vorschlage Fragen laden](#vorschlage-fragen-laden)
4. [Char counter laden](#load-char-counter)
5. [Passende Antwort finden](#suchen-nach-der-passenden-antwort)
   1. [Vorbereiten des Textes](#vorbereiten-des-textes)
   2. [Matches suchen](#suchen-nach-matches)
   3. [Suchen nach allen möglichen Antworten](#suchen-nach-allen-möglichen-antworten)
   4. [Suchen nach der besten Antwort](#suchen-nach-der-besten-antwort)

### [Adminbereich](#admintool-section-start)<a name="tableofcontent-admintool"></a>

1. [Einleitung](#admintool-introduction)

---

## Allgemein <a name="general-section-start"></a>

### Einleitung <a name="general-introduction"></a>

In diesem Abschnitt des Dokumentes beschreiben wir das Projekt im Allgemeinen. Wir zählen auf was für Technologien wir
verwenden und wie man verschiedene Dinge macht, wie zum Beispiel wie man eine Datenbankverbindung aufbaut. Zudem
schreiben wir noch auf was wir machen wollten, aber wegen zu weniger Zeit nicht machen konnten.

### Technologien <a name="technologies"></a>

In diesem Abschnitt zählen wir die einzelnen Technologien auf damit klar ist was benötigt wird um starten zu können.

#### Projekt allgemein

- GitHub
- Maven als build tool

#### Backend

- Java 16
- Hibernate für DB Connection und abfragen

#### Frontend

- TypeScript

### Wichtige Klassen

#### Datenbank Klassen

Für mehr Informationen zum Abschnitt [Datenbank Abfragen](#datenbank-abfragen) gehen.

#### Texte vorbereiten und reinigen

Wir haben die Java
Klasse [<code>com/ubs/backend/util/PrepareString.java</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/util/PrepareString.html)
erstellt. In ihr haben wir unterschiedliche Methoden für das vorbereiten von Strings damit sie korrekt und ohne Gefahren
in der Datenbank gespeichert werden können oder an den Benutzer geschickt werden können.

Folgende Methoden hat die Klasse:

- [<code>prepareString</code>](#preparestring)

##### [prepareString()](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/util/PrepareString.html#prepareString(java.lang.String,int,boolean,boolean))

Diese Methode bereitet den String vor. Sie akzeptiert folgende Parameter:

1. <code>String string</code>
2. <code>int maxStringlength</code>
3. <code>boolean removeAllSpecialChars</code>
4. <code>boolean toLowerCase</code>
5. <code>removeQuestionMark</code>

Der erste Parameter ist ganz einfach der String, also z.B. die Benutzereingabe beim Chatbot, welcher vorbereitet werden
soll.

Der zweite Parameter definiert wie lange (Anzahl Zeichen) der String maximal sein darf. Wenn der gegebene String länger
ist als dieser Parameter definiert, wird alles danach weggenommen. Für mehr Informationen gehe zu [shortenString](#shortenstring).


Der dritte Parameter ist ein boolean und definiert ob spezielle Charaktere entfernt werden sollen. Unter speziellen Charakteren meinen wir besonders HTML code. Dadurch verhindern wir Hackerangriffe.

Der vierte Parameter ist ein boolean und definiert ob der Text in Kleinbuchstaben umgewandelt werden soll. Wenn der boolean false ist bleibt der Text so wie er ist.

Der fünfte Parameter ist ein boolean und definiert ob alle vorkommenden Fragezeichen entfernt werden sollen oder nicht.

##### [shortenString](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/util/PrepareString.html#shortenString(java.lang.String,int))

Diese Methode verkürzt den angegebenen String auf die gegebene Länge.
<br>
Ein Beispiel:

```java
String text="Hallo";
String shortenedText=shortenString(text,3);
System.out.println(preparedText);
```

Die Ausgabe wäre dann <code>Hal</code>, die Länge des Textes wurde also von 5 auf 3 verkürzt da wir die maximale Länge auf 3 gesetzt haben.

##### [stringTooLong](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/util/PrepareString.html#stringTooLong(java.lang.String,int))

Diese Methode überprüft einfach ob der angegebene String länger ist als die angegebene maximale Länge.
Gibt <code>true</code> zurück wenn der String länger ist und <code>false</code> wenn der String kürzer oder gleich lang ist.

#### Datentypen Informationen

Wir haben eine Java Enum Datei namens [`com/ubs/backend/classes/enums/DataTypeInfo.java`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/DataTypeInfo.html).
In dieser Datei haben wir die unterschiedlichen Datentypen definiert, wie zum Beispiel [`ANSWER_TEXT`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/DataTypeInfo.html#ANSWER_TEXT).
Alle Enums in dieser Datei besitzen einmal eine [`maxLength`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/DataTypeInfo.html#maxLength) und einen [`name`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/DataTypeInfo.html#name).
<br>
`maxLength` definiert die maximale grösse des Types und `name` definiert einfach wie man es im Frontend anzeigen kann.

Als Beispiel kann man da den [Charcounter](#load-char-counter) nehmen. Dort wird über einen Service die maximale Anzahl an Zeichen pro Input Feld geladen.

### Allgemeine wichtige Informationen

#### Datenbank

In unserem Projekt verwenden wir **[Hibernate](#hibernate-konfigurieren)** für die Datenbank verbindung und alle
Abfragen. Für das connection pooling und die sicherstellung dass connections wieder geschlossen werden benutzen wir
**[C3PO](#c3po-konfigurieren)**.

##### Hibernate konfigurieren

Im **pom.xml** haben wir Hibernate eingebunden, wir verwenden die Version 5.4.29.

```xml

<dependencies>
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-core</artifactId>
        <version>5.4.29.Final</version>
    </dependency>
</dependencies>
```

---

Hibernate wird dazu verwendet in den verschiedenen Dialekten, ohne Probleme eine verbindung zur Datenbank zu
gewährleisten. Dies ermöglichte es, ohne viel Code zu ändern in verschiedenen Umgebungen zu arbeiten.

So konnten wir zum Beispiel lokal auf unseren Rechner **MySQL** verwenden während wir auf unserer
Testumgebung, [Heroku](https://www.heroku.com/),
**PostgreSQL** und auf unserer Production in der UBS Umgebung **Microsoft SQL Server** verwenden.

###### Verbindung zu Datenbank

Um die Verbindung zur Datenbank einzustellen, müssen folgende Stellen im Persistence abgeändert werden.

```xml

<properties>
    <property name="hibernate.dialect" value=""/>
    <property name="javax.persistence.jdbc.url" value=""/>
    <property name="javax.persistence.jdbc.user" value=""/>
    <property name="javax.persistence.jdbc.password" value=""/>
    <property name="javax.persistence.jdbc.driver" value=""/>
</properties>
```

---

In der ersten Linie konfiguriert man den Dialekt. Also welche Datenbank Sprache man verwendet. Eine Liste mit möglichen
Dialekten findet man
[hier](https://www.javatpoint.com/dialects-in-hibernate).

Ein Beispiel für MySQL 8 wäre folgend.

```xml

<property name="hibernate.dialect" value="org.hibernate.dialect.MySQL8Dialect"/>
```

---

In der zweiten Linie konfiguriert man die URL. Die URL erklärt Hibernate wo die Datenbank zu finden ist und noch einige
weitere optionale Informationen kann man hinzufügen. Eine URL ist immer ein wenig anders, abhängig von eurem gewählten
Dialekt. Euer Datenbank Anbieter sollte im Normalfall direkt die korrekte URL anzeigen, welche ihr nur noch kopieren
müsst.

Ein Beispiel für eine Verbindung zu einer lokalen MySQL Datenbank.

```XML

<property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/db"/>
```

---

In den nächsten zwei Linien konfiguriert man den Benutzer, mit welchem man die Datenbank verwenden will. Zuerst schreibt
man den Namen des Users und danach das Passwort. Falls der Benutzer kein Passwort hat, kann man es einfach leer lassen.

Bedenke das Hibernate nur sachen machen darf welche der Benutzer darf. Wenn also der Benutzer nur leserechte hat, kann
hibernate auch nur lesen.

Ein Beispiel für einen Benutzer ohne Passwort.

```xml

<property name="javax.persistence.jdbc.user" value="root"/>
<property name="javax.persistence.jdbc.password" value=""/>
```

---

In der letzten Linie definiert man den Treiber mit welchem Hibernate die Abfragen zur Datenbank macht. Im normalfall
gibt es für jede Datenbank einen offiziellen Treiber. Sobald ein geeigneter Treiber gefunden wurde diesen Herunterladen
und in das Projekt einbinden, bevorzugt ist es hier das über
**Maven** zu machen. Einfach ein Dependency in das **pom.xml** tun.

Ein Beispiel für das Einbinden eines MySQL Treibers.

```xml

<property name="javax.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver"/>
```

---

Das fertige Persistence würde jetzt also wie folgt aussehen.

```xml

<properties>
    <property name="hibernate.dialect" value="org.hibernate.dialect.MySQL8Dialect"/>
    <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/db"/>
    <property name="javax.persistence.jdbc.user" value="root"/>
    <property name="javax.persistence.jdbc.password" value=""/>
    <property name="javax.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver"/>
</properties>
```

---

###### Weitere Konfigurationen

Nach der Konfiguration der Verbindung zur Datenbank haben wir noch zwei weitere Linien

```xml

<property name="hibernate.show_sql" value=""/>
<property name="hibernate.hbm2ddl.auto" value=""/>
```

---

<code>show_sql</code> kann einen Wert von entweder <code>true</code> oder
<code>false</code> nehmen.

Wenn man diesen auf <code>true</code> setzt, gibt Hibernate alle SQL Befehle in die Konsole aus.

---

<code>hbm2ddl.auto</code> definiert die Art und Weise wie Hibernate mit Änderungen in der Datenbank umgehen soll.
Folgende Werte können verwendet werden.

- <code>validate</code>: Validiert das Schema, macht keine Änderungen an der Datenbank
- <code>update</code>: Fügt neue Tabellen und Spalten hinzu, löscht aber nie etwas.
- <code>create</code>: Löscht immer das ganze Schema zuerst und erstellt es dann neu.
- <code>create-drop</code>: Zuerst gleich wie <code>create</code>, danach löscht es das ganze Schema sobald das <code>
  SessionFactory</code> Objekt geschlossen wurde. Typischerweise, sobald das Programm beendet wird.
- <code>none</code>: Macht nichts.

Es wird empfohlen in einer Testumgebung <code>update</code> zu verwenden und in der Production <code>none</code> zu
verwenden.

---

Mehr zu Hibernate allgemein kann man
[hier](https://hibernate.org/orm/documentation/) finden.

---

##### C3PO konfigurieren

C3PO ist ein Tool, mit welchem man Connection-pooling besser unterstützen kann als mit Hibernate selber.

###### Die Grösse des pools definieren

Mit den Linien 21 - 23 können wir den pool konfigurieren.

```xml

<property name="hibernate.c3po.min_size" value="10"/>
<property name="hibernate.c3p0.max_size" value="100"/>
<property name="hibernate.c3p0.acquire_increment" value="5"/>
```

Die erste Linie definiert wie viele connections es im pool mindestens hat, die zweite wie viele es maximal haben kann.
Mit der dritten Linie geben wir an um wie viel sich die aktuelle grösse des pools erhöht.

Beispiel. <br> Wir haben im Moment 10 verbundene connections und eine weitere möchte sich verbinden, increment ist auf 5
gestellt, das bedeutet die aktuelle grösse des pools wäre jetzt 15.

###### Debug

```xml

<property name="hibernate.c3p0.unreturnedConnectionTimeout" value="30"/>
<property name="hibernate.c3po.debugUnreturnedConnectionStackTraces" value="true"/>
```

Die erste Linie definiert, wie lange eine Connection im Ganzen am Leben sein kann. In der aktuellen Konfiguration heisst
das also das jede Verbindung maximal 30 Sekunden überlebt. <br> Wenn man also eine Methode oder eine Abfrage ausführt,
die länger braucht, kann es sein das diese nicht vollendet werden kann, in diesem Fall die Zeit höher stellen.

---

##### Verbindung zur Datenbank aufbauen

Bevor man etwas mit der Datenbank machen kann brauchen wir eine Verbindung zu ihr. Hier ist wichtig das zuerst die
Persistence richtig konfiguriert wurde damit wir auch die korrekte Datenbank ansprechen. Mehr dazu 
[hier](#verbindung-zu-datenbank).

Danach müssen wir dort wo wir eine Verbindung brauchen (z.B um eine [Abfrage](#datenbank-abfragen) zu machen) folgenden
Code schreiben:

```java
EntityManager em = Connector.getInstance().open();
em.getTransaction().begin();
```

Dadurch öffnen wir eine Verbindung zur Datenbank und mit der gerade geholten Instanz (bei uns heisst sie `em`) können 
wir nun [Abfragen bei der Datenbank](#datenbank-abfragen) machen.

Sehr wichtig ist das diese Verbindung auch wieder geschlossen wird! Und zwar direkt dann wenn man sie nicht mehr braucht. 
Falls die Verbindung nicht geschlossen wird oder einfach zu lange offen ist können wir andere Anfragen blockieren da 
irgendwann unser Pool an Connections voll ist.
<br>
Um die Verbindung wieder zu schliessen brauchen wir einfach folgende zwei Zeilen code.

```java
em.getTransaction().commit();
em.close();
```

##### Datenbank abfragen

Wir haben für Interaktionen mit der Datenbank eine generische Java Klasse namens
<code>DAO</code>, zu finden in
[<code>src/main/java/com/ubs/backend/classes/database/dao/DAO.java</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/dao/DAO.html)
. Diese Klasse wird für standard Befehle in der Datenbank wie z.B.
[<code>select</code>](<https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/dao/DAO.html#select()>)
,
[<code>insert</code>](<https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/dao/DAO.html#insert(T)>)
und
[<code>remove</code>](<https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/dao/DAO.html#remove(long)>)
.
<br> Für weitere Befehle, welche Klassenspezifisch sind haben wir jeweils ein eigenes DAO für die Datenklasse erstellt.

Wenn man eine Abfrage mit der Tabelle <code>Answers</code> interagieren möchte erstellt man eine Instanz der Klasse
[<code>AnswerDao</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/dao/AnswerDAO.html)
und verwendet ihre Methoden. Als Beispiel, wenn man alle Antworten aus der Datenbank holen möchte würde das wie folgt
aussehen.

```java
AnswerDAO answerDAO=new AnswerDAO();
List<Answer> answersFromDB=answerDAO.select();
```



---

#### Datenbank mit Testdaten befüllen

Um das Programm zu Testen möchte man vermutlich eine Datenbank mit Testdaten haben. Für diesen Zweck haben wir die Datei
<code>com/ubs/backend/demo/CreateDB.java</code> für das tatsächliche befüllen der Datenbank und die Datei <code>
com/ubs/backend/demo/DBData.java</code> mit den Daten die wir in die Datenbank laden wollen.

Wir empfehlen vor dem Ausführen der Datei <code>CreateDB</code> die
**Persistence** konfiguration zu überprüfen und womöglich zu ändern. Auf folgendes sollte geachtet werden.

- Ist **Persistence** mit der _richtigen_ Datenbank verbunden?
- Ist <code>hbm2ddl.auto</code> auf <code>update</code> oder </code> create? [1]
- Ist die Datenbank lokal oder online? [2]

<sup>[1] Wir empfehlen es auf <code>create</code> zu stellen, da es zuerst alles löscht und danach neu erstellt.
Mit <code>update</code> kriegt man doppelte Daten.</sup>

<sup>[2] In C3PO haben wir eine Zeit definiert mit welcher wir bestimmen wie lange eine einzelne Verbindung zur
Datenbank bestehen kann. Bei Online Datenbanken kann es teilweise länger dauern diese zu befüllen, als was wir der
Verbindung Zeit geben. Falls das der Fall ist, müssen wir C3PO kurz anpassen. Gehe dazu zum
Abschnitt [C3PO konfigurieren - Debug](#debug).</sup>

Wenn das **Persistence** entsprechend angepasst wurde, kann man jetzt
<code>CreateDB</code> ausführen und warten bis es fertig ist mit dem befüllen der Datenbank.

---

##### Testdaten ändern oder hinzufügen

In der Datei <code>com/ubs/backend/demo/DBData.java</code> sind alle Testdaten welche nachher in die Datenbank
gespeichert werden. In dieser Datei müssen jetzt nur noch Inhalte gelöscht, bearbeitet oder hinzugefügt werden.

#### Chatbot Server Adresse definieren

Ein Beispiel, die Adresse zum Chatbot sieht wie folgt aus:
<code>http://localhost:8080/chatbot/ </code>. In diesem Fall ist
<code>chatbot</code> die Adresse des Servers.

Um den Server zu ändern, muss einmal in JavaScript sowie in Java bei jeweils einer Datei etwas geändert werden.

##### JavaScript

In der Datei <code>src/main/webapp/assets/js/utilities/variables.ts</code> einfach die Variable <code>server</code>
abändern.

Im Beispiel von vorhin würde es so aussehen:
<br>
Vorher:

```javascript
const server = window.location.origin;
```

Nachher:

```javascript
const server = window.location.origin + "/chatbot";
```

##### Java

In der
Datei [<code>com/ubs/backend/util/Variables.java</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/util/Variables.html)
einfach den
String [<code>serverDirectory</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/util/Variables.html#serverDirectory)
anpassen.

Im Beispiel von vorhin würde es wie folgt aussehen:
<br>
Vorher:

```java
public class Variables {
    public static String serverDirectory = "";
}

```

Nachher:

```java
public class Variables {
    public static String serverDirectory = "/chatbot";
}

```

Nachdem die Anpassungen vorgenommen wurde, sollte der Chatbot ohne Probleme laufen.

---

#### Antwort- und Tagtypen

Im Chatbot gibt es verschiedene Antworttypen sowie 2 verschiedene Tagtypen. In diesem Abschnitt erklären wir was der
Unterschied zwischen diesen Typen ist und wie sie funktionieren.

##### Antworttypen

Wir haben unterschiedliche Typen von Antworten für unterschiedliche Zwecke.
<br>
Einige Typen werden durch Code generiert und sind dadurch dynamisch, während andere von der Datenbank geholt werden.
Einige Typen teilen sich tags pro Antwort während andere Typen pro Antwort andere Tags haben.

Im Chatbot verwenden wir folgende Antworttypen:

- [Default](#default)
- [Joke](#joke)
- [Facts](#facts)
- [Statistics](#statistic)
- [Error](#error)

Eine kurze Zusammenfassung der Typen:

|  | [Default](#default) | [Joke](#joke) | [Facts](#facts) | [Statistics](#statistics) | [Error](#error) |
| :--- | --- | --- | --- | --- | --- |
| Generierte Antworten | Nein | Nein | Nein | Ja | Ja |
| Antworten aus der Datenbank | Ja | Ja | Ja | Nein | Nein | 
| [Gruppierte Tags](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#groupedTags) | Nein | Ja | Ja | Ja | Nein |
| [Nutzer kann bearbeiten](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#canBeUserMade) | Ja | Ja | Ja | Nein | Nein |
| [Ist standard versteckt](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#hidden) | Nein | Ja | Ja | Ja | Ja |
| [Ist erzwungen versteckt](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#forceHidden) | Nein | Ja | Ja | Ja | Ja | 

###### [Default](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#DEFAULT)

| Was | Ist so |
| :--- | ---: |
| Generierte Antworten | Nein |
| Antworten aus der Datenbank | Ja |
| [Gruppierte Tags](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#groupedTags) | Nein |
| [Nutzer kann bearbeiten](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#canBeUserMade) | Ja |
| [Ist standard versteckt](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#hidden) | Nein |
| [Ist erzwungen versteckt](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#forceHidden) | Nein |

Der [<code>Default</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#DEFAULT)
Typ ist der normale/standard Typ. Alle Antworten mit diesem Typen haben ihre eigenen Tags.
<br>
Weitere Antworten können von Administratoren hinzugefügt werden.
<br>
Antworten mit diesem Typen sind standardmässig nicht versteckt, können aber versteckt werden.

###### [Joke](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#JOKE)

| Was | Ist so |
| :--- | ---: |
| Generierte Antworten | Nein |
| Antworten aus der Datenbank | Ja |
| [Gruppierte Tags](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#groupedTags) | Ja |
| [Nutzer kann bearbeiten](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#canBeUserMade) | Ja |
| [Ist standard versteckt](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#hidden) | Ja |
| [Ist erzwungen versteckt](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#forceHidden) | Ja |

Der [<code>Joke</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#JOKE)
Typ ist gedacht für Witze. Alle Antworten mit diesem Typen teilen sich die Tags.
<br>
Alle Antworten mit diesem Typen sind standardmässig versteckt und müssen versteckt bleiben.
<br>
Weitere Antworten können von Administratoren hinzugefügt werden.

###### [Facts](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#FACTS)

| Was | Ist so |
| :--- | ---: |
| Generierte Antworten | Nein |
| Antworten aus der Datenbank | Ja |
| [Gruppierte Tags](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#groupedTags) | Ja |
| [Nutzer kann bearbeiten](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#canBeUserMade) | Ja |
| [Ist standard versteckt](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#hidden) | Ja |
| [Ist erzwungen versteckt](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#forceHidden) | Ja |

Der [<code>Facts</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#FACTS)
Typ ist gedacht für Fakten über den Chatbot, kann aber auch für andere Arten von Fakten verwendet werden. Alle Antworten
mit diesem Typen teilen sich die Tags.
<br>
Alle Antworten mit diesem Typen sind standardmässig versteckt und müssen versteckt bleiben.
<br>
Weitere Antworten können von Administratoren hinzugefügt werden.

###### [Statistics](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#STATISTICS)

| Was | Ist so |
| :--- | ---: |
| Generierte Antworten | Ja |
| Antworten aus der Datenbank | Nein |
| [Gruppierte Tags](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#groupedTags) | Ja |
| [Nutzer kann bearbeiten](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#canBeUserMade) | Nein |
| [Ist standard versteckt](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#hidden) | Ja |
| [Ist erzwungen versteckt](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#forceHidden) | Ja |

Der [<code>Statistics</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#STATISTICS)
Typ ist gedacht für Statistiken über den Chatbot, kann aber auch für andere Arten von Statistiken verwendet werden. Alle
Antworten mit diesem Typen teilen sich die Tags.
<br>
Alle Antworten mit diesem Typen sind standardmässig versteckt und müssen versteckt bleiben.
<br>
Alle Antworten mit diesem Typen werden vom Chatbot selber generiert.
<br>
Es können keine weiteren Antworten von Administratoren über das Admintool hinzugefügt werden. Um weitere Antworten
generieren zu können, muss man weitere Antwortmöglichkeiten zum Code hinzufügen. Dazu muss
der ['handler'](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#handler) der
Antwort angepasst und bearbeitet werden.

Im Moment generieren wir zwei Arten von Statistiken:

- Seit wann ist der Chatbot aktiv
- Wie viele Fragen wurden in {Zeitraum} beantwortet

Für jede generierte Antwort holen wir die entsprechenden Daten aus der Datenbank und generieren daraus eine Antwort.

###### [Error](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#ERROR)

| Was | Ist so |
| :--- | ---: |
| Generierte Antworten | Ja |
| Antworten aus der Datenbank | Nein |
| [Gruppierte Tags](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#groupedTags) | Nein |
| [Nutzer kann bearbeiten](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#canBeUserMade) | Nein |
| [Ist standard versteckt](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#hidden) | Ja |
| [Ist erzwungen versteckt](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#forceHidden) | Ja |

Der [<code>Error</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#ERROR)
Typ ist gedacht für Fehler beim Versenden oder suchen einer passenden Antwort. Diese Antwort sollte keine Tags besitzen
da diese nie gebraucht werden. Dieser Typ wird nur zum Benutzer zurückgeschickt, wenn der Chatbot keine passende Antwort
findet oder es einen Fehler gibt.
<br>
Diese Antwort generiert keine Statistiken
<br>
Alle Antworten mit diesem Typen werden vom Chatbot selber generiert.
<br>
Es können keine weiteren Antworten von Administratoren über das Admintool hinzugefügt werden. Um weitere Antworten
generieren zu können, muss man weitere Antwortmöglichkeiten zum Code hinzufügen.

##### Tagtypen

Unsere Tags werden in zwei Arten aufgeteilt.

- [Result](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/Result.html)
- [TypeTag](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/TypeTag.html)

Der Unterschied zwischen den beiden Typen ist einfach: Gehört der Tag zu einer einzelnen Antwort ist er ein <code>
Result</code>, aber gehört der Tag zu einer Gruppe von Antworten so ist er ein <code>TypeTag</code>. Je nach Typ werden
die Tags in einer anderen Tabelle gespeichert.
<code>Result</code> wird in der Tabelle <code>results</code> gespeichert. <code>TypeTag</code> in <code>typetag</code>.

Antworten mit dem Typen [<code>Default</code>](#default)
haben Tags mit dem Typen <code>Result</code> weil die Antwort nicht gruppierte Tags hat. Allerdings Antworten mit zum
Beispiel dem Typen
[<code>Joke</code>](#joke) haben Tags mit dem Typen <code>TypeTag</code>

Der Unterschied in der Datenbank sieht wie folgt aus.

| | Result | TypeTag
| :--- | --- | --- |
| Upvotes | Ja | Ja |
| Downvotes | Ja | Ja |
| Anzahl Verwendungen | Ja | Ja |
| Referenz zu Tag | Ja | Ja |
| Referenz zu Antwort | Ja | Nein |
| AntwortTyp | Nein | Ja |

Wie man also sehen kann, <code>Result</code> braucht nicht zu wissen was für ein Typ die Antwort ist, da wir eine
direkte referenz zu der Antwort haben und direkt von ihr diese Information beziehen können.
<br>
<code>TypeTag</code> hat diese Referenz nicht weswegen wir den Typen abspeichern müssen. Dadurch können wir im Code alle
Antworten welche gruppierte Tags haben nehmen und mit der Tabelle vergleichen. Dann nehmen wir alle Tags mit demselben
Typen und wissen genau welche Antwort welche Tags hat.

---

### Ideen für die Weiterentwicklung

Hier werden Ideen aufgelistet, welche wir noch für den Chatbot hatten aber nicht genug Zeit hatten sie zu realisieren.

- Statistiken
    - Den Typ des Charts bei den Statistiken ändern können (von Linie zu Säulen etc)
    - Gute vs schlechte Bewertungen pro Zeit
    - Die aktuellen vorgeschlagenen Fragen direkt auf der Startseite anzeigen lassen, wenn eine Frage neu vorgeschlagen
      wird hat die Frage ein "neu" label [1]
    - Bei den einzelnen Antworten in der Statistik noch mehr Statistiken anzeigen
        - Wie oft um welche Zeit wurde diese Antwort versendet
        - wie viele gute vs schlechte bewertungen
        - ...
    - Bei einem Tag alle matches anzeigen die zu diesem Tag übersetzt werden
    - Im Moment gibt es gerade mal zwei Arten von generierten Antworten mit dem Typen <code>Statistics</code>, dadurch
      ist es recht langweilig und oft werden dieselben Antworten noch einmal geschickt. Mehr unterschiedlich generierte
      Antworten währen von Vorteil. (Siehe [Statistics](#statistics)).
- Nach dem Löschen eines Tags checken, ob eine beantwortete Frage nicht mehr beantwortet werden kann und entsprechend
  als unbeantwortet markieren
- Im moment wird bei den vorschlage Fragen nicht verhindert, dass Fragen mit derselben Antwort angezeigt werden. Idee
  ist es die besten Fragen einer Antwort zu zeigen, so wird garantiert das man 3 unterschiedliche Fragen als Vorschlag
  hat
- Dateien, vor allem Bilder sind sehr gross und man kann leicht den Text der Nachricht übersehen. Man könnte es so
  machen das alle Dateien ausklappbar sind und anfangs zuerst eingeklappt sind.
- Ein Darkmode für das Admintool
- Wenn der Bot eine längere Nachricht schickt diese automatisch unterteilen in kleinere einzelne Nachrichten, sieht
  besser/übersichtlicher aus
- Alle ManyToMany Beziehungen in Hibernate von List<> zu Set<> ändern
- Stored Procedures verwenden, z.B. für Levenshtein direkt in der DB anstelle in Java. Wäre schneller
- Der Kunde wollte ursprünglich, dass der Benutzer die Möglichkeit hat, auf eine unbeantwortete Frage selber eine
  Antwort zu schreiben. Diese Antwort muss zunächst von einem Admin akzeptiert werden. Der Admin kann die Antwort selber
  aber auch bearbeiten und dann akzeptieren.
- Tags die zu einer versteckten (hidden) Antwort gehören sollten nicht in der Autocompletion des Benutzers vorkommen
- Eigene Konsole für DB Abfragen im Admintool. So könnte man als Admin ohne direkten Zugang auf die Datenbank im
  Admintool einige Abfragen machen und herausfinden was das Problem ist
- Benutzer Detail Seite Design anpassen, da es noch veraltet und unschön ist.

[1] neu = seit dem letzten login des jeweiligen Benutzers neu, davor wurde diese Frage noch nicht vorgeschlagen.

---

## Chatbot <a name="chatbot-section-start"></a>

### Einleitung <a name="chatbot-introduction"></a>

In diesem Abschnitt des Dokumentes beschreiben wir wie der Chatbot funktioniert. Der Chatbot ist die Hauptfunktion
dieses Projektes. Es ist die erste Seite die ein Admin sieht und die einzige Seite die ein normaler Benutzer sehen soll.

Folgend wird beschrieben was beim laden der Seite in welcher Reihenfolge passiert.

1. [Den Status überprüfen](#check-state)
2. [Vorschlage Fragen laden](#vorschlage-fragen-laden)
3. [Char counter laden](#load-char-counter)

### Status überprüfen <a name="check-state"></a>

Wenn der Chatbot geöffnet wird wird als erstes eine Test Abfrage zum Server geschickt und auf seine Antwort gewartet.
Solange auf die Antwort gewartet wird, zeigt der Chatbot eine Nachricht an mit der Information das die "Verbindung zum
Server aufgebaut wird".
![Checking state of server](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/developerDoc/chatbot/checkStatus.jpg)
Um den Status zu überprüfen verwenden wir unseren Service
[<code>getStatus()</code>](<https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#getStatus()>)
. Diese Methode rufen wir über eine Rest Schnittstelle auf. Der Path zu dieser Schnittstelle ist <code>
services/get/status</code>.

[<code>getStatus()</code>](<https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#getStatus()>)
ruft folgende weitere Methoden auf.

1. [<code>questionSuggestions(String amountQuestionsString)</code>](<https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#questionSuggestions(java.lang.String)>)
2. [<code>search(String input, boolean affectStatistics)</code>](<https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/IntentFinderNew.html#search(java.lang.String,boolean)>)

Der Aufruf der beiden Methoden ist in einem try catch Block. Sobald wir einen Fehler bekommen, wissen wir das wir ein
Problem haben und kriegen einen schlechten Status. Wenn wir kein Fehler haben kriegen wir einen guten Status-

#### Guter Status

Bei einem guten Status ändern wir die Nachricht des Bots zu einer Begrüssung.
![Good State message](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/developerDoc/chatbot/goodStateWelcome.jpg)
Danach geht es weiter.

#### Schlechter Status

Bei einem schlechten Status geben wir einen Fehler aus.
![Bad State message](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/developerDoc/chatbot/badStateError.jpg)
Das Textfeld bleibt deaktiviert und es passiert nichts mehr.

### Vorschlage Fragen laden

Wenn wir beim [überprüfen des Status](#check-state) keinen Fehler bekommen haben laden wir die drei vorschlage Fragen.
Diese holen wir über folgenden Fetch Befehl

```javascript
let response = await fetch(
    `${server}/services/get/questionSuggestions?amountQuestions=3`
);
```

Die Variable <code>server</code> ist unser gesetzter Servername. Mehr dazu im Abschnitt
[Chatbot Server Adresse definieren](#chatbot-server-adresse-definieren). Dieser Service, den wir hier aufrufen, erwartet
den Parameter <code>
amountQuestions</code>. Dieser Parameter definiert wie viele Fragen wir laden wollen, in diesem Fall sind es 3. Der
Service ist hier zu finden:
[<code>com.ubs.backend.services.Get#questionSuggestions</code>](<https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#questionSuggestions(java.lang.String)>)
. Im Service werden zuerst die aktuell im Monat best bewerteten Benutzer Fragen geholt.

```java
List<TempAnsweredQuestionTimesResult> answeredQuestions=answeredQuestionTimesResultDAO.selectMonthlyOrderedByUpvotes(new StatistikTimes(new Date()),amountQuestions);
```

Übergeben wird dabei eine
[<code>StatistikTimes</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/statistik/times/StatistikTimes.html)
welche dem jetzigen Datum entspricht und die vorab definierte Anzahl an Fragen. Der HQL Befehl für die Abfrage sieht wie
folgt aus:

```java
List<AnsweredQuestionTimesResult> answeredQuestionTimesResults=em.createQuery("select new AnsweredQuestionTimesResult(aqtr.answeredQuestionStatistik, aqtr.answeredQuestionResult, sum(aqtr.upvote), sum(aqtr.downvote)) from AnsweredQuestionTimesResult aqtr "+
        "where aqtr.answeredQuestionStatistik.statistikTimes.month.myDate = :month"+
        " and aqtr.answeredQuestionStatistik.statistikTimes.year.myDate = :year "+
        " and aqtr.answeredQuestionStatistik.answeredQuestion.isHidden = false"+
        " group by aqtr.answeredQuestionStatistik.answeredQuestion"+
        " order by sum(aqtr.upvote) desc",
        AnsweredQuestionTimesResult.class)
        .setParameter("month",month)
        .setParameter("year",year).setMaxResults(max).getResultList();
```

Einfach erklärt sagen wir hibernate es soll eine neue Instanz der Klasse
[<code>AnsweredQuestionTimesResult</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/questions/AnsweredQuestionTimesResult.html)
mit den aus der Datenbank geholten Daten erstellen. Die Daten bestehen einmal aus der
[<code>AnsweredQuestionStatistik</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/statistik/AnsweredQuestionStatistik.html)
, der
[<code>AnsweredQuestionResult</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/questions/AnsweredQuestionResult.html)
, der Summe der Upvotes (Daumen hoch) sowie der Summe der Downvotes (Daumen runter) der Frage. Wir selektieren also alle
[<code>AnsweredQuestionTimesResult</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/questions/AnsweredQuestionTimesResult.html)
bei welchen das Jahr und der Monat der selbe ist wie bei der
[<code>StatistikTimes</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/statistik/times/StatistikTimes.html)
die wir übergeben und gruppieren dann alle gefundene Einträge mit der Frage an sich und sortieren sie nach den Upvotes.
Wir müssen dann nur noch den Monat und das Jahr sowie die maximal zu findenden Einträge setzen und schon fertig.

Es kann sein das es in der Datenbank nicht genügend Fragen hat, bei denen die Kriterien zutreffen. In diesem Fall werden
die fehlenden Plätzen mit den
[<code>Standardfragen</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/questions/DefaultQuestion.html)
gefüllt.

**Beispiel**: In der Datenbank existiert nur eine passende Frage, wir wollen aber 3. In diesem Fall füllen wir die
restlichen 2 Plätze mit zufällig ausgewählten Standardfragen.

Am Ende konstruieren wir noch ein JSON und geben dieses zurück. In Typescript wandeln wir dieses JSON dann um in HTML
und zeigen es an.

Benutzer können jetzt auf die vorschlage Fragen drauf drücken und es wird als normale Frage behandelt.

### Char counter laden<a name="load-char-counter"></a>

Wenn wir beim [überprüfen des Status](#check-state) keinen Fehler bekommen haben laden wir den Char counter. Der Char
counter ist einfach ein kleines Tool welches durch ein Fetch Befehl die maximal erlaubten Charakter für ein Eingabe Feld
lädt. Beim Chatbot sehen wir so wieviele Zeichen der Benutzer als Frage eingeben kann.
![char counter userinput](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/developerDoc/chatbot/charCounterUserInputChatbot.jpg)

Der Fetch Befehl sieht wie folgt aus:

```javascript
const response = await fetch(`${server}/services/get/maxInputLength`);
```

Der Service ist hier zu finden:
[<code>com.ubs.backend.services.Get#getMaxLength</code>](<https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#getMaxLength()>)
.

Hier ist wie der Service funktioniert. Wir haben die Java Klasse
[<code>com/ubs/backend/classes/enums/DataTypeInfo.java</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/DataTypeInfo.html)
definiert. Diese Java Klasse ist ein Enum in welchem wir die verschiedenen Typen an Daten definiert haben. Zum Beispiel
haben wir
[<code>USER_QUESTION_INPUT</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/DataTypeInfo.html#USER_QUESTION_INPUT)
welcher wir für das Eingabe Feld des Chatbots verwenden. Jedes Enum hat zwei Werte. Einmal
[<code>maxLength</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/DataTypeInfo.html#maxLength)
, welcher die maximale länge in Charakteren definiert und einmal
[<code>name</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/DataTypeInfo.html#name)
welches in TypeScript verwendet wird um herauszufinden wo diese Information gebraucht wird.

Im Service konstruieren wir jetzt noch ein JSON und geben dieses zurück. In TypeScript wird das JSON ausgelesen und in
HTML umgewandelt.

---

### Suchen nach der passenden Antwort

Wenn ein Nutzer eine Nachricht abschickt, rufen wir einen Service auf welcher nach der am besten passenden Antwort
sucht.
<br>
Der Service findet man
hier: [<code>com.ubs.backend.services.IntentFinderNew#findAnswer</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/IntentFinderNew.html#findAnswer(java.lang.String))
.
<br>
Der Service gibt ein Objekt des
Types [<code>Response</code>](https://docs.oracle.com/javaee/7/api/javax/ws/rs/core/Response.html) zurück.
<br>

---

#### Vorbereiten des Textes

Im Service bereiten wir zuerst den Text den wir vom Benutzer bekommen vor. Dadurch verwenden wir unsere Methode 
[<code>prepareString()</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/util/PrepareString.html#prepareString(java.lang.String,int,boolean,boolean))
bei welcher wir den Text übergeben. Das sieht dann wie folgt aus:
```java
input = prepareString(input, DataTypeInfo.USER_QUESTION_INPUT.getMaxLength(), true, false, false);
```

Beim Input des Benutzers entfernen wir also alle speziellen Zeichen, er wird nicht to lowercase gemacht und das 
Fragezeichen wird auch nicht entfernt. Zudem wurde die Maximalgrösse auf den Wert des Datentypes 
[`DataTypeInfo.USER_QUESTION_INPUT`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/DataTypeInfo.html#USER_QUESTION_INPUT) 
gesetzt.
Danach nehmen wir alle Wörter aus dem Input und speichern diese in ein Array namens `words`.

```java
String[] words = input.split("\\s");
```

Das Problem jetzt ist, in dem Text könnten doppelte Wörter vorkommen. Diese sind für uns unnötig und würden nur die Zeit
erhöhen die wir brauchen würden, um eine passende Antwort zu finden. Deswegen nehmen wir diese durch die folgende Zeile
Code raus.

```java
words = new HashSet<>(Arrays.asList(words)).toArray(new String[0]);
```

Durch diese Schwarze Magie werden doppelte Wörter aus dem Array entfernt.
Nachdem wir den Text vorbereitet, in einzelne Wörter aufgeteilt und doppelte Wörter entfernt haben machen wir weiter mit
dem Entfernen von Wörtern auf der Blacklist.

Zuerst öffnen wir eine Verbindung zur Datenbank. [Hier](#verbindung-zur-datenbank-aufbauen) wird erklärt wie das geht.
<br>
Um jetzt die Wörter zu finden, die vollständig ignoriert werden sollen, gehen wir mit einer `for` loop durch alle Wörter
durch und vergleichen diese mit der Datenbank.
Falls wir in der Datenbank ein gleiches Wort finden entfernen wir dieses aus dem Text des Benutzers.
<br>
Falls es in der Datenbank nicht dasselbe Wort gibt fügen wir dieses Wort zu einer neuen ArrayList hinzu und entfernen 
dort das Fragezeichen, falls es eines hat. In dieser Liste werden am Ende alle zu benutzenden Wörter sein.
<br>
Der Grund dafür das wir die Fragezeichen hier entfernen und nicht vorhin schon ist relativ einfach:
Wir wollen die Eingabe des Benutzers so normal wie nur möglich behalten da diese Frage später ein Vorschlag werden 
könnte. Da soll diese Frage einigermassen Sinn ergeben. Allerdings müssen wir das Fragezeichen aus dem Wort entfernen da
es sonst die Suche verfälschen könnte da wir keine Tags haben mit Fragezeichen.

Das ganze sieht wie folgt aus:
```java
ArrayList<String> filteredWords = new ArrayList<>();
for (String word : words) {
    if (isBlacklisted(word, blacklistEntryDAO, em)) {
        BlacklistEntry blacklistEntryFromDB = blacklistEntryDAO.selectByWord(word, em);
        input = input.replaceAll(blacklistEntryFromDB.getWord() + " ", ""); // replace the blacklist entry and its following space
        input = input.replaceAll(blacklistEntryFromDB.getWord(), ""); // if the blacklist entry doesn't have a space afterwards, replace just the blacklist entry
    } else {
        filteredWords.add(word.replace("?", ""));
    }
}
```

Die Methode [`isBlacklisted`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/IntentFinderNew.html#isBlacklisted(java.lang.String,com.ubs.backend.classes.database.dao.BlacklistEntryDAO,javax.persistence.EntityManager))
nimmt ein String als Parameter und überprüft ob dieser String bereits in der Datenbank Tabelle mit den Blacklists 
existiert, wenn ja erhöhen wir die Verwendung dieses Eintrages und geben den Wert `true` zurück. Wenn dieser String 
nicht bereits in der Datenbank existiert geben wir den Wert `false` zurück.

---

#### Suchen nach Matches

Nach dem Rausfiltern der zu ignorierenden Wörter holen wir uns alle Tags aus der Datenbank.
Zudem erstellen wir eine 
ArrayList< [AnswerType](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html) >, 
`foundAnswerTypes`, in welcher wir alle verschiedenen Antworttypen speichern, mehr dazu später.
Als drittes brauchen wir eine ArrayList< [WordLevenshteinDistance](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/WordLevenshteinDistance.html) >,
`wordLevenshteinDistances`.

```java
List<Tag> tags = tagDAO.select(em);
ArrayList<AnswerType> foundAnswerTypes = new ArrayList<>();
ArrayList<WordLevenshteinDistance> wordLevenshteinDistances = new ArrayList<>();
```

Jetzt kommen wir dazu mögliche Antworten zu finden.

Wir gehen durch alle Wörter, welche wir am schluss noch haben, durch und dann durch alle gefundenen Tags.

```java
for (String word : filteredWords){
    for(Tag tag : tags){
    }
}
```

Wir berechnen jetzt immer die Distanz (`dist`), also der Unterschied in der Länge und der Schreibweise zwischen dem 
aktuellen Wort und dem aktuellen Tag.
Dazu verwenden wir in unserer Klasse 
[`com/ubs/backend/util/CalculateRating.java`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/util/CalculateRating.html)
die Methode 
[`getLevenshteinDistance()`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/util/CalculateRating.html#getLevenshteinDistance(int,int)).
<br>
Diese Methode erwartet zwei Werte, einmal `distanceRaw` und `stringLengthDifference`.
Der erste Parameter berechnen wir durch die Methode 
[`calculate`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/util/Levenshtein.html#calculate(java.lang.String,java.lang.String,boolean)) 
in der Klasse [`Levenshtein`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/util/Levenshtein.html).
Um den Levenshtein Algorithmus zu verstehen sieh [hier](https://de.wikipedia.org/wiki/Levenshtein-Distanz)
Der zweite Parameter ist ganz einfach die länge des längeren Wortes.
Wir vergleichen ja das aktuelle Wort mit dem aktuellen Tag, der zweite Parameter ist einfach die Länge des längeren.

```java
Math.max(tag.getTag().length(), word.length());
```

[`getLevenshteinDistance()`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/util/CalculateRating.html#getLevenshteinDistance(int,int)) 
gibt dann einen Wert zwischen 0 und 1 zurück. Wir wissen jetzt also die Distanz zwischen Wort und Tag.

Als Nächstes überprüfen wir, ob diese Distanz innerhalb unserer Werte liegen.
<br>
Falls die Distanz zu weit weg von unseren Werten ist, passt der aktuelle Tag nicht zu diesem Wort und wir gehen weiter 
zum nächsten Tag.
<br>
Falls die Distanz innerhalb unserer Werte ist holen wir alle 
[Results](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/Result.html) mit diesem Tag.
Wir gehen durch alle gefundenen Results und erstellen ein neues 
[WordLevenshteinDistance](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/WordLevenshteinDistance.html) 
mit dem aktuellen Wort, dem aktuellen Result, der Distanz und 
[`levenshteinCertain`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/IntentFinderNew.html#levenshteinCertain). 
Zu letzteres kommen wir gleich. Zudem übergeben wir noch den aktuellen EntityManager da wir im Konstruktor noch eine Datenbank Abfrage machen müssen.

Im Konstruktor des gerade erstellten `WordLevenshteinDistance` überprüfen wir, ob die Distanz die wir übergeben kleiner 
ist als `levenshteinCertain`. `levenshteinCertain` definiert einfach wie gross die Distanz maximal sein darf damit das 
Wort als 'absolut korrekt' gilt.
<br>
Falls die Distanz kleiner ist als `levenshteinCertain` definieren wir das aktuelle Wort als 
[`Match`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/Match.html).
Wenn es ein Match ist, müssen wir einen neuen Match erstellen und wenn nötig in der Datenbank speichern.
Dafür rufen wir 
[`newMatch`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/WordLevenshteinDistance.html#newMatch(com.ubs.backend.classes.database.Tag,java.lang.String,javax.persistence.EntityManager))
auf. In dieser Methode überprüfen wir, ob es bereits dieser Match in der Datenbank gibt, wenn ja geben wir diesen zurück, wenn nein erstellen wir einen neuen in der Datenbank und geben diesen zurück.

Nachdem wir durch alle Results dieses Tags durch sind, müssen wir noch kurz alle 
[`TypeTags`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/TypeTag.html) überprüfen.
Wir suchen also in der Tabelle mit den TypeTags nach demselben Tag bei dem wir gerade sind.
Jeder Tag kann nur einmal pro TypeTag vorkommen, aber da wir verschiedene Typen haben könnte der Tag öfters in der Tabelle vorkommen, weswegen wir eine Liste zurückbekommen.

Wir gehen nun durch diese Liste durch und machen eigentlich dasselbe wie vorhin. Wir erstellen ein
[WordLevenshteinDistance](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/WordLevenshteinDistance.html)
und übergeben die verschiedenen Parameter.
<br>
Jetzt überprüfen wir aber noch zusätzlich, ob der aktuelle Typ schon in unserer am Anfang erstellten ArrayList `wordLevenshteinDistances` existiert. Falls nicht fügen wir den Typen hinzu.

Das Ganze wird jetzt wiederholt bis wir durch alle Wörter durch sind.

---

#### Suchen nach allen möglichen Antworten
Nachdem wir alle möglichkeiten gefunden haben, geht es darum sich jetzt für die Beste zu entscheiden.
<br>
Im Moment haben wir aber noch das Problem, das wir nicht wirklich wissen welche Antwort wir von den gruppierten Typen schicken sollen.
Alle Antworten mit einem 
[AntwortTypen](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html) wie zum Beispiel
den Typen 
[`JOKE`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#JOKE) haben alle 
dieselben Tags. Dadurch ist es für uns in diesem Bereich unmöglich herauszufinden welche jetzt die beste Antwort wär. 
Deswegen nehmen wir einfach eine zufällige Antwort.

Dazu gehen wir durch alle gefundenen Antworttypen und lassen eine zufällige Antwort finden und speichern diese zusammen 
mit dem Typen der Antwort in einer 
Hashmap< [AnswerType](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html), [Answer](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/Answer.html) >.

```java
HashMap<AnswerType, Answer> answerTypeAnswerHashMap = new HashMap<>();
for (AnswerType answerType : foundAnswerTypes) {
    answerTypeAnswerHashMap.put(answerType, answerType.handle(null));
}
```

Jetzt wissen wir welche Antwort wir pro Typ schicken würden.

Als Nächstes geht es darum alle möglichen Antworten zu finden. Denn bis jetzt haben wir zwar die unterschiedlichen 
Results mit den Tags und den Bewertungen, aber diese sind nicht pro Antwort kombiniert. Also fügen wir jetzt alle 
zusammen.

Dafür erstellen wir zuerst eine neue ArrayList in welcher wir Instanzen der Klasse 
[`PossibleAnswer`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/PossibleAnswer.html) speichern. 
Danach gehen wir durch alle vorhin gefundenen `WordLevenshteinDistance` in unserer ArrayList `wordLevenshteinDistances`.
Wir holen die aktuellen Up- sowie Downvotes von der aktuellen `WordLevenshteinDistance` Instanz und schauen welche Art
das Result ist.

Wenn es vom Typ `Result` ist nehmen wir einfach die aktuelle Antwort dieses Results und erstellen eine neue Instanz
von `PossibleAnswer`.
<br>
Wenn es vom Typ `TypeTag` ist nehmen wir zwar die aktuellen up- und downvotes, aber wir können nicht die Antwort davon
nehmen da `TypeTag` keine Referenz zu dieser hat. Aber genau aus diesem Grund haben wir vorhin zu den einzelnen 
Antworttypen eine zufällige Antwort gesucht. Jetzt nehmen wir aus der Hashmap diese Antwort und erstellen eine neue 
Instanz von `PossibleAnswer`.

Als Nächstes wollen wir diese Instanz in unsere ArrayList speichern.
<br>
Dafür überprüfen wir zuerst, ob die Antwort schon in der Liste existiert. Falls ja erhöhen wir die up- und downvotes
der bereits existierenden Antwort mit den Up- und Downvotes der aktuellen Antwort. 
<br>
Falls nein fügen wir die aktuelle Antwort zur Liste hinzu.

#### Suchen nach der besten Antwort

Jetzt gehen wir durch alle gefundenen möglichen Antworten und berechnen deren einzelnen Bewertungen.
```java
for (PossibleAnswer possibleAnswer : possibleAnswers) {
    possibleAnswer.setRating();
}
```

Die Methode 
[`setRating()`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/PossibleAnswer.html#setRating())
wird dafür verwendet.
In dieser Methode gehen wir durch alle `WorldLevenshteinDistance` durch, welche die aktuelle Antwort besitzt. Dabei
addieren wir immer die aktuelle Distanz zu einer einzelnen Variable.
Dadurch haben wir am Ende die gesamte Distanz. Mit diesem Wert berechnen wir nun die Bewertung in dem wir
[`com.ubs.backend.util.CalculateRating#getRating(int, int, float)`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/util/CalculateRating.html#getRating(int,int,float))
aufrufen.

Nachdem wir bei allen möglichen Antworten die Bewertung gesetzt haben gehen wir weiter und suchen die beste Antwort.
<br>
Dafür erstellen wir ein float namens `maxRating` und setzen den Wert auf -1f.
dann gehen wir durch alle möglichen Antworten und schauen, ob deren Bewertung besser ist als das aktuelle `maxRating`.
<br>
Falls dies der Fall wäre, setzen wir das aktuelle `maxRating` auf diese Bewertung und die aktuelle `bestAnswer`setzen 
wir auf die momentane Antwort.
<br>
Das machen wir dann so lange bis wir durch alle Antworten durch sind.

Falls wir am Ende keine Antwort gefunden haben, erstellen wir selber eine Antwort mit dem Typen 
[`ERROR`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/enums/AnswerType.html#ERROR) und 
konstruieren daraus ein JSON welches wir zurückgeben.
Gleichzeitig fügen wir eine neue
[UnansweredQuestion](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/questions/UnansweredQuestion.html)
in die Datenbank ein.

Falls wir am Ende eine Antwort gefunden haben überprüfen wir, ob diese versteckt ist, falls dies der Fall ist wollen wir 
keine Statistiken generieren.
<br>
Falls wir Statistiken generieren, erhöhen wir die Aufrufe der gefundenen Antwort um 1.
Zusätzlich, unabhängig davon, ob wir Statistiken generieren oder nicht, erhöhen wir die Aufrufe jedes in der Antwort vorkommenden `Results`.
<br>
Danach, falls wir Statistiken generieren wollen, fügen wir eine neue 
[`AnsweredQuestion`](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/questions/AnsweredQuestion.html)
zur Datenbank hinzu mit all den nötigen Informationen.

Am Ende schliessen wir die Verbindung zur Datenbank und erstellen ein JSON mit unserer gefundenen Antwort, welche wir 
dann an den Benutzer zurückschicken.
Der Browser bekommt dann diese Antwort und zeigt sie dem Benutzer an.

---

## Adminbereich <a name="admintool-section-start"></a>

### Einleitung <a name="admintool-introduction"></a>

In diesem Abschnitt des Dokumentes beschreiben wir wie der Adminbereich funktioniert.

Das Admintool ist dazu da, alles mögliche am Chatbot zu verwalten z.B. dem Hinzufügen von Antworten

### Seiten Laden

Unser Admintool ist als eine Seite aufgebaut. Das bedeutet das wir ein Hauptfile, `src/main/webapp/pages/adminTool/adminTool.jsp`, 
haben und bei diesem laden wir alle Seiten einfach rein.
<br>
Der Vorteil davon ist es das wir bei Javascript unterschiedliche Variablen und "states" zwischen den verschiedenen Seiten 
behalten können. 
<br>
So haben wir z.B. ein HTML file, `src/main/webapp/pages/adminTool/adminToolNavigation.html`, in welchem wir ganz einfach
die linke Leiste, die Navigation, beschrieben haben.

<img src="https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/developerDoc/adminTool/navigationShowcase.jpg" alt="adminTool Navigation" style="height:300px;"/>

Per Javascript legen wir dann fest welche dieser Knöpfe aktiv ist und welche Seite wir laden sollen.

Um Seiten zu Laden haben wir die Methode `loadPage()`, sie hat folgende Parameter:

- fileName: der Name der Datei, welche geladen werden soll
- newActiveButtonID: die ID des Buttons in der Navigation welcher highlighted werden soll
- specificDataNeeded: Ob zusätzliche daten aus der Datenbank gelesen werden müssen
- dataID: die ID des Eintrags in der Datenbank, falls `specificDataNeeded = true` ist
- forcecReload: ob die Seite neu geladen werden soll

Mit dem folgenden Code Beispiel kann man zum Beispiel die Antwort Details zur Antwort mit der ID 1 in der Datenbank
anzeigen:

```typescript
    await loadPage("answersDetails.html", "answersButton", true, 1);
```

Dabei wird auch der Knop mit der ID "answersButton" als aktiv gesetzt.

---

<sup>Autor: [Tim Irmler](https://github.com/zwazel) </sup>
<br>
<sup>Zuletzt bearbeitet: 08.10.2021</sup>