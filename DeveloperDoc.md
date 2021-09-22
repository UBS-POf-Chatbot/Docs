# Entwickler Dokumentation
In diesem Dokument wird beschrieben wie der Chatbot funktioniert und wo was zu finden ist, damit zukünftige Entwickler ohne Probleme den Chatbot weiterentwickeln können.
Dieses Dokument wird in drei Hauptteile aufgeteilt. Einmal allgemein, der Chatbot an sich und den Adminbereich.

## Inhaltsverzeichnis
### [Allgemein](#general-section-start)
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
In diesem Abschnitt des Dokumentes beschreiben wir das Projekt allgemein.
Wir zählen auf was für Technologien wir verwenden, welche bekannte Probleme es noch gibt
### Technologien <a name="technologies"></a>

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

# NICHT FERTIG -@ZWAZEL

Um den Status zu überprüfen verwenden wir unseren Service  [<code>getStatus()</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#getStatus()). Diese Methode rufen wir über eine Rest Schnittstelle auf. Der Path zu dieser Schnittstelle ist <code>services/get/status</code>.

[<code>getStatus()</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#getStatus()) ruft folgende weitere Methoden auf.
1. [<code>questionSuggestions(String amountQuestionsString)</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#questionSuggestions(java.lang.String))
2. [<code>search(String input, boolean affectStatistics)</code>](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/IntentFinderNew.html#search(java.lang.String,boolean))



#### Guter Status


### Char counter laden<a name="load-char-counter"></a>
### Chatbot initialisieren<a name="init-chatbot"></a>

## Adminbereich <a name="admintool-section-start"></a>
### Einleitung <a name="admintool-introduction"></a>
In diesem Abschnitt des Dokumentes beschreiben wir wie der Adminbereich funktioniert.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNjY5NTUyMzgsLTY1MDAyNDY1LC02OT
E1MDA2MDEsMTYwNjMzOTU3OCwyMDU2NDU5MzM1LC0xNDM1MDA2
NjM1LDMyMjk0Njg2MiwxNzYwNTk2NTYyLC0yMTk4Mzk3NzMsLT
E4MTI1MTM5MzUsNjkxMTg2Mzk2LDY1Njk4MTg2NywtNzgzNDU2
OTg2LDE2ODEyNTgwMTYsLTQ5MjA4NDY5OCw1MzA2MjkyNzQsLT
IwODg3NDY2MTJdfQ==
-->