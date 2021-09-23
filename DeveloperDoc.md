# Entwickler Dokumentation
In diesem Dokument wird beschrieben wie der Chatbot funktioniert und wo was zu finden ist, damit zukünftige Entwickler ohne Probleme den Chatbot weiterentwickeln können.
Dieses Dokument wird in drei Hauptteile aufgeteilt. Einmal allgemein, der Chatbot an sich und den Adminbereich.

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

## Allgemein <a name="general-section-start"></a>
### Einleitung <a name="general-introduction"></a>
In diesem Abschnitt des Dokumentes beschreiben wir das Projekt im allgemeinen.
Wir zählen auf was für Technologien wir verwenden und wie man verschiedene Dinge macht, wie zum Beispiel wie man eine Datenbankverbindung aufbaut. Zudem schreiben wir noch auf was wir machen wollten, aber wegen zu weniger Zeit nicht machen konnten.
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
##### Datenbank konfigurieren
TODO: persistence und c3po erklären
##### Verbindung mit Datenbank herstellen
TODO: entity manager open und close sachen
##### Datenbank abfragen
TODO: DAOs erklären, kleiner einblick in createQuery()

### Ideen für weiterentwicklung

## Chatbot <a name="chatbot-section-start"></a>
### Einleitung <a name="chatbot-introduction"></a>
In diesem Abschnitt des Dokumentes beschreiben wir wie der Chatbot funktioniert.
Der Chatbot ist die Hauptfunktion dieses Projektes. Es ist die erste Seite die ein Admin sieht und die einzige Seite die ein normaler Benutzer sehen soll.

Folgend wird beschrieben was beim laden der Seite in welcher Reihenfolge passiert.
1. [Den Status überprüfen](#check-state)
2. [Char counter laden](#load-char-counter)
3. [Den Chatbot initialisieren](#init-chatbot)

### Status überprüfen <a name="check-state"></a>
Wenn der Chatbot geöffnet wird wird als erstes eine Test Abfrage zum Server geschickt und auf seine Antwort gewartet. Solange auf die Antwort gewartet wird, zeigt der Chatbot eine Nachricht an mit der Information das die "Verbindung zum Server aufgebaut wird".
![Checking state of server](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/checkStatus.jpg)
Um den Status zu überprüfen verwenden wir unseren Service  [<code>getStatus()</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#getStatus()). Diese Methode rufen wir über eine Rest Schnittstelle auf. Der Path zu dieser Schnittstelle ist <code>services/get/status</code>.

[<code>getStatus()</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#getStatus()) ruft folgende weitere Methoden auf.
1. [<code>questionSuggestions(String amountQuestionsString)</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#questionSuggestions(java.lang.String))
2. [<code>search(String input, boolean affectStatistics)</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/IntentFinderNew.html#search(java.lang.String,boolean))

TODO ALLES DANACH

#### Guter Status


### Char counter laden<a name="load-char-counter"></a>
### Chatbot initialisieren<a name="init-chatbot"></a>

## Adminbereich <a name="admintool-section-start"></a>
### Einleitung <a name="admintool-introduction"></a>
In diesem Abschnitt des Dokumentes beschreiben wir wie der Adminbereich funktioniert.
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEVudHdpY2tsZXIgRG9rdW
1lbnRhdGlvbiAtIFNUSU1BXG5hdXRob3I6ICdUaW0gSXJtbGVy
LCBNYXJjIEFuZHJpIEZ1Y2hzJ1xuc3RhdHVzOiBkcmFmdFxuIi
wiaGlzdG9yeSI6WzYwMTM3OTQ1OCwxNDAwODU4NDc1LDcxNzg3
NzM2MSwtMTQ2MjE4NzQ1NiwtMjM3ODYzNDk5LC02NTAwMjQ2NS
wtNjkxNTAwNjAxLDE2MDYzMzk1NzgsMjA1NjQ1OTMzNSwtMTQz
NTAwNjYzNSwzMjI5NDY4NjIsMTc2MDU5NjU2MiwtMjE5ODM5Nz
czLC0xODEyNTEzOTM1LDY5MTE4NjM5Niw2NTY5ODE4NjcsLTc4
MzQ1Njk4NiwxNjgxMjU4MDE2LC00OTIwODQ2OTgsNTMwNjI5Mj
c0XX0=
-->