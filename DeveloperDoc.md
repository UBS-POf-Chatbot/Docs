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
3. [Allgemein wichtige Informationen](#allgemeine-wichtige-informationen)
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
   3. [Ideen für die Weiterentwicklung](#ideen-für-weiterentwicklung)

---

### [Chatbot](#chatbot-section-start)<a name="tableofcontent-chatbot"></a>

 1. [Einleitung](#chatbot-introduction)
 2. [Den Status überprüfen](#check-state)
	 1. [Guter Status](#guter-status)
	 2. [Schlechter Status](#schlechter-status)
4. [Char counter laden](#load-char-counter)
5. [Den Chatbot initialisieren](#init-chatbot)

---

### [Adminbereich](#admintool-section-start)<a name="tableofcontent-admintool"></a>

1. [Einleitung](#admintool-introduction)

---

## Allgemein <a name="general-section-start"></a>

### Einleitung <a name="general-introduction"></a>

In diesem Abschnitt des Dokumentes beschreiben wir das Projekt im allgemeinen. Wir zählen auf was für Technologien wir
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

- Typescript

### Allgemeine wichtige Informationen

#### Datenbank

In unserem Projekt verwenden wir **[Hibernate](#hibernate-konfigurieren)** für die Datenbank verbindung und alle
Abfragen. Für das connection pooling und die sicherstellung dass connections wieder geschlossen werden benutzen wir **[C3PO](#c3po-konfigurieren)**.

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
Testumgebung, [Heroku](https://www.heroku.com/), **PostgreSQL** und auf unserer Production in der UBS Umgebung
**Microsoft SQL Server** verwenden.

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
In der ersten Linie konfiguriert man den Dialekt. Also welche Datenbank Sprache man verwendet.
Eine Liste mit möglichen Dialekten findet man [hier](https://www.javatpoint.com/dialects-in-hibernate).

Ein Beispiel für MySQL 8 wäre folgend.

```xml
<property name="hibernate.dialect" value="org.hibernate.dialect.MySQL8Dialect"/>
```
---

In der zweiten Linie konfiguriert man die URL. Die URL erklärt Hibernate wo die Datenbank zu finden ist und noch einige weitere optionale Informationen kann man hinzufügen.
Eine URL ist immer ein wenig anders, abhängig von eurem gewählten Dialekt. Euer Datenbank Anbieter sollte im Normalfall direkt die korrekte URL anzeigen, 
welche ihr nur noch kopieren müsst.

Ein Beispiel für eine Verbindung zu einer lokalen MySQL Datenbank.
```XML
<property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/db"/>
```

---

In den nächsten zwei Linien konfiguriert man den Benutzer, mit welchem man die Datenbank verwenden will.
Zuerst schreibt man den Namen des Users und danach das Passwort. Falls der Benutzer kein Passwort hat, kann man es einfach leer lassen.

Bedenke das Hibernate nur sachen machen darf welche der Benutzer darf. Wenn also der Benutzer nur leserechte hat, kann hibernate auch nur lesen.

Ein Beispiel für einen Benutzer ohne Passwort.
```xml
<property name="javax.persistence.jdbc.user" value="root"/>
<property name="javax.persistence.jdbc.password" value=""/>
```

---

In der letzten Linie definiert man den Treiber mit welchem Hibernate die Abfragen zur Datenbank macht. Im normalfall gibt es für jede Datenbank einen offiziellen Treiber. 
Sobald ein geeigneter Treiber gefunden wurde diesen Herunterladen und in das Projekt einbinden, bevorzugt ist es hier das über **Maven** zu machen. Einfach ein Dependency in das **pom.xml** tun.

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

<code>show_sql</code> kann einen Wert von entweder <code>true</code> oder <code>false</code> nehmen.

Wenn man diesen auf <code>true</code> setzt, gibt Hibernate alle SQL Befehle in die Konsole aus.

---
<code>hbm2ddl.auto</code> definiert die Art und Weise wie Hibernate mit Änderungen in der Datenbank umgehen soll.
Folgende Werte können verwendet werden.
- <code>validate</code>: Validiert das Schema, macht keine Änderungen an der Datenbank
- <code>update</code>: Fügt neue Tabellen und Spalten hinzu, löscht aber nie etwas.
- <code>create</code>: Löscht immer das ganze Schema zuerst und erstellt es dann neu.
- <code>create-drop</code>: Zuerst gleich wie <code>create</code>, danach löscht es das ganze Schema sobald das <code>SessionFactory</code> Objekt geschlossen wurde. Typischerweise, sobald das Programm beendet wird.
- <code>none</code>: Macht nichts.

Es wird empfohlen in einer Testumgebung <code>update</code> zu verwenden und in der Production <code>none</code> zu verwenden.

---

Mehr zu Hibernate allgemein kann man [hier](https://hibernate.org/orm/documentation/) finden.

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

Beispiel. <br>
Wir haben im Moment 10 verbundene connections und eine weitere möchte sich verbinden, increment ist auf 5 gestellt, das bedeutet die aktuelle grösse des pools wäre jetzt 15.

###### Debug
```xml
<property name="hibernate.c3p0.unreturnedConnectionTimeout" value="30"/>
<property name="hibernate.c3po.debugUnreturnedConnectionStackTraces" value="true"/>
```

Die erste Linie definiert, wie lange eine Connection im Ganzen am Leben sein kann. In der aktuellen Konfiguration heisst das also das jede Verbindung maximal 30 Sekunden überlebt.
<br>
Wenn man also eine Methode oder eine Abfrage ausführt, die länger braucht, kann es sein das diese nicht vollendet werden kann, in diesem Fall die Zeit höher stellen.

---

##### Datenbank abfragen

Wir haben für Interaktionen mit der Datenbank eine generische Java Klasse namens <code>DAO</code>, zu finden in [<code>src/main/java/com/ubs/backend/classes/database/dao/DAO.java</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/dao/DAO.html).
Diese Klasse wird für standard Befehle in der Datenbank wie z.B. [<code>select</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/dao/DAO.html#select()), [<code>insert</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/dao/DAO.html#insert(T)) und [<code>remove</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/dao/DAO.html#remove(long)).
<br>
Für weitere Befehle, welche Klassenspezifisch sind haben wir jeweils ein eigenes DAO für die Datenklasse erstellt.

Wenn man eine Abfrage mit der Tabelle <code>Answers</code> interagieren möchte erstellt man eine Instanz der Klasse [<code>AnswerDao</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/classes/database/dao/AnswerDAO.html) und verwendet ihre Methoden.
Als Beispiel, wenn man alle Antworten aus der Datenbank holen möchte würde das wie folgt aussehen.
```java
AnswerDAO answerDAO = new AnswerDAO();
List<Answer> answersFromDB = answerDAO.select();
```

---

#### Datenbank mit Testdaten befüllen
Um das Programm zu Testen möchte man vermutlich eine Datenbank mit Testdaten haben. Für diesen Zweck haben wir die Datei 
<code>com/ubs/backend/demo/CreateDB.java</code> für das tatsächliche befüllen der Datenbank und die Datei <code>com/ubs/backend/demo/DBData.java</code> mit den Daten die wir in die Datenbank laden wollen.

Wir empfehlen vor dem Ausführen der Datei <code>CreateDB</code> die **Persistence** konfiguration zu überprüfen und womöglich zu ändern.
Auf folgendes sollte geachtet werden.
- Ist **Persistence** mit der *richtigen* Datenbank verbunden?
- Ist <code>hbm2ddl.auto</code> auf <code>update</code> oder </code> create? [1]
- Ist die Datenbank lokal oder online? [2]

<sup>[1] Wir empfehlen es auf <code>create</code> zu stellen, da es zuerst alles löscht und danach neu erstellt. Mit <code>update</code> kriegt man doppelte Daten.</sup>

<sup>[2] In C3PO haben wir eine Zeit definiert mit welcher wir bestimmen wie lange eine einzelne Verbindung zur Datenbank bestehen kann.
Bei Online Datenbanken kann es teilweise länger dauern diese zu befüllen, als was wir der Verbindung Zeit geben. Falls das der Fall ist, müssen wir C3PO kurz anpassen.
Gehe dazu zum Abschnitt [C3PO konfigurieren - Debug](#debug).</sup>

Wenn das **Persistence** entsprechend angepasst wurde, kann man jetzt <code>CreateDB</code> ausführen und warten bis es fertig ist mit dem befüllen der Datenbank.

---

##### Testdaten ändern oder hinzufügen
In der Datei <code>com/ubs/backend/demo/DBData.java</code> sind alle Testdaten welche nachher in die Datenbank gespeichert werden.
In dieser Datei müssen jetzt nur noch Inhalte gelöscht, bearbeitet oder hinzugefügt werden.

#### Ideen für die Weiterentwicklung
Hier werden Ideen aufgelistet welche wir noch für den Chatbot hatten aber nicht genug Zeit hatten sie zu realisieren.

- Statistiken
	- Den Typ des Charts bei den Statistiken ändern können (von Linie zu Säulen etc)
	- Gute vs schlechte Bewertungen pro Zeit
	- Die aktuellen vorgeschlagenen Fragen direkt auf der Startseite anzeigen lassen, wenn eine Frage neu vorgeschlagen wird (neu = seit dem letzten login) hat die Frage ein "neu" label
	- Bei den einzelnen Antworten in der Statistik noch mehr Statistiken anzeigen
		- Wie oft um welche zeit wurde diese Antwort versendet
		- wie viele gute vs schlechte bewertungen
		- ...
- Nach dem löschen eines Tags checken ob eine beantwortete Frage nicht mehr beantwortet werden kann und entsprechend als unbeantwortet markieren
- Im moment wird bei den vorschlage Fragen nicht verhindert das Fragen mit der selben Antwort angezeigt werden. Idee ist es die besten Fragen einer Antwort zu zeigen, so wird garantiert das man 3 unterschiedliche Fragen als Vorschlag hat
- Dateien, vorallem Bilder sind sehr gross und man kann leicht den Text der Nachricht übersehen. Man könnte es so machen das alle Dateien ausklapbar sind und anfangs zuerst eingeklappt sind.
- Ein Darkmode für das Admintool
- Wenn der Bot eine längere Nachricht schickt diese automatisch unterteilen in kleinere einzelne Nachrichten, sieht besser/übersichtlicher aus
- Alle ManyToMany Beziehungen in Hibernate von List<> zu Set<> ändern
- Stored Procedures verwenden, z.B. für Levenshtein direkt in der DB anstelle in Java. Wäre schneller
- Der Kunde wollte ursprünglich das der Benutzer die Möglichkeit hat, auf eine unbeantwortete Frage selber eine Antwort zu schreiben. Diese Antwort muss zunächst von einem Admin akzeptiert werden. Der Admin kann die Antwort selber aber auch bearbeiten und dann akzeptieren.
- Tags die zu einer versteckten (hidden) Antwort gehören sollten nicht in der Autocompletion des Benutzers vorkommen
- Eigene Konsole für DB Abfragen im Admintool. So könnte man als Admin ohne direkten Zugang auf die Datenbank im Admintool einige Abfragen machen und herausfinden was das Problem ist

---

## Chatbot <a name="chatbot-section-start"></a>

### Einleitung <a name="chatbot-introduction"></a>

In diesem Abschnitt des Dokumentes beschreiben wir wie der Chatbot funktioniert. Der Chatbot ist die Hauptfunktion
dieses Projektes. Es ist die erste Seite die ein Admin sieht und die einzige Seite die ein normaler Benutzer sehen soll.

Folgend wird beschrieben was beim laden der Seite in welcher Reihenfolge passiert.

1. [Den Status überprüfen](#check-state)
2. [Char counter laden](#load-char-counter)
3. [Den Chatbot initialisieren](#init-chatbot)

### Status überprüfen <a name="check-state"></a>

Wenn der Chatbot geöffnet wird wird als erstes eine Test Abfrage zum Server geschickt und auf seine Antwort gewartet.
Solange auf die Antwort gewartet wird, zeigt der Chatbot eine Nachricht an mit der Information das die "Verbindung zum
Server aufgebaut wird".
![Checking state of server](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/developerDoc/chatbot/checkStatus.jpg)
Um den Status zu überprüfen verwenden wir unseren
Service  [<code>getStatus()</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#getStatus())
. Diese Methode rufen wir über eine Rest Schnittstelle auf. Der Path zu dieser Schnittstelle ist <code>
services/get/status</code>.

[<code>getStatus()</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#getStatus()) ruft
folgende weitere Methoden auf.

1. [<code>questionSuggestions(String amountQuestionsString)</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#questionSuggestions(java.lang.String))
2. [<code>search(String input, boolean affectStatistics)</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/IntentFinderNew.html#search(java.lang.String,boolean))

Der Aufruf der beiden Methoden ist in einem try catch Block. Sobald wir einen Fehler bekommen, wissen wir das wir ein Problem haben und kriegen einen schlechten Status. Wenn wir kein Fehler haben kriegen wir einen guten Status-

#### Guter Status
Bei einem guten Status ändern wir die Nachricht des Bots zu einer Begrüssung.
![Good State welcome](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/developerDoc/chatbot/goodStateWelcome.jpg)
Danach geht es weiter.

#### Schlechter Status
Bei einem schlechten Status geben wir einen Fehler aus.
![Good State welcome](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/developerDoc/chatbot/badStateError.jpg)
Das Textfeld bleibt deaktiviert und es passiert nichts mehr.

### Char counter laden<a name="load-char-counter"></a>
Wenn wir beim [überprüfen des Status](#check-state) keinen Fehler bekommen haben laden wir den Char counter.


### Chatbot initialisieren<a name="init-chatbot"></a>

---

## Adminbereich <a name="admintool-section-start"></a>

### Einleitung <a name="admintool-introduction"></a>

In diesem Abschnitt des Dokumentes beschreiben wir wie der Adminbereich funktioniert.

---
<sup>Autor: [Tim Irmler](https://github.com/zwazel) </sup>
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEVudHdpY2tsZXIgRG9rdW
1lbnRhdGlvbiAtIFNUSU1BXG5hdXRob3I6ICdUaW0gSXJtbGVy
LCBNYXJjIEFuZHJpIEZ1Y2hzJ1xuc3RhdHVzOiBkcmFmdFxuIi
wiaGlzdG9yeSI6WzE1MTYzMzA5NzgsLTcyNTkyNTQ2MywtMTA0
OTgyMjk3NCw4NzAyNzY4MTEsLTM0Mzc0MzAyMiwtNDYxMDExMz
EwXX0=
-->