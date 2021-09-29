# Entwickler Dokumentation

In diesem Dokument wird beschrieben wie der Chatbot funktioniert und wo was zu finden ist, damit zukünftige Entwickler
ohne Probleme den Chatbot weiterentwickeln können. Dieses Dokument wird in drei Hauptteile aufgeteilt. Einmal allgemein,
der Chatbot an sich und den Adminbereich.

---

## Inhaltsverzeichnis

### [Allgemein](#general-section-start)<a name="tableofcontent-general"></a>

1. [Einleitung](#general-introduction)
2. [Technologien](#technologies)

### [Chatbot](#chatbot-section-start)<a name="tableofcontent-chatbot"></a>

1. [Einleitung](#chatbot-introduction)
2. [Den Status überprüfen](#check-state)
3. [Char counter laden](#load-char-counter)
4. [Den Chatbot initialisieren](#init-chatbot)

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

In unserem Projekt verwenden wir [**Hibernate**](#hibernate-konfigurieren) für die Datenbank verbindung und alle
Abfragen. Für das connection pooling und sicherstellen das connections wieder geschlossen werden benutzen wir [**
C3PO**](#c3po-konfigurieren).

##### Hibernate konfigurieren <a name="hibernate-konfigurieren"></a>

Im POM haben wir Hibernate eingebunden, wir verwenden die Version 5.4.29.

```xml
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>5.4.29.Final</version>
</dependency>
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

Die nächsten zwei Linien konfiguriert man den Benutzer, mit welchem man die Datenbank verwenden will.
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

##### C3PO konfigurieren <a name="c3po-konfigurieren"></a>

##### Datenbank abfragen

TODO: DAOs erklären, kleiner einblick in createQuery()

### Ideen für weiterentwicklung

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
![Checking state of server](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/checkStatus.jpg)
Um den Status zu überprüfen verwenden wir unseren
Service  [<code>getStatus()</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#getStatus())
. Diese Methode rufen wir über eine Rest Schnittstelle auf. Der Path zu dieser Schnittstelle ist <code>
services/get/status</code>.

[<code>getStatus()</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#getStatus()) ruft
folgende weitere Methoden auf.

1. [<code>questionSuggestions(String amountQuestionsString)</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#questionSuggestions(java.lang.String))
2. [<code>search(String input, boolean affectStatistics)</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/IntentFinderNew.html#search(java.lang.String,boolean))

TODO ALLES DANACH

#### Guter Status

### Char counter laden<a name="load-char-counter"></a>

### Chatbot initialisieren<a name="init-chatbot"></a>

---

## Adminbereich <a name="admintool-section-start"></a>

### Einleitung <a name="admintool-introduction"></a>

In diesem Abschnitt des Dokumentes beschreiben wir wie der Adminbereich funktioniert.

<sup>Autor: Tim Irmler</sup>