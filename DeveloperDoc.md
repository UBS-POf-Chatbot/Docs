# Entwickler Dokumentation
In diesem Dokument wird beschrieben wie der Chatbot funktioniert und wo was zu finden ist, damit zukünftige Entwickler ohne Probleme den Chatbot weiterentwickeln können.
Dieses Dokument wird in zwei Hauptteile aufgeteilt. Einmal der Chatbot an sich und einmal den Adminbereich.

## Inhaltsverzeichnis
### [Chatbot](#chatbot-section-start)<a name="tableofcontent-chatbot"></a>
 1. [Einleitung](#chatbot-introduction)
 2. [Den Status überprüfen](#check-state)
 3. [Char counter laden](#load-char-counter)
 4. [Den Chatbot initialisieren](#init-chatbot)

### [Adminbereich](#admintool-section-start)<a name="tableofcontent-admintool"></a>
1. [Einleitung](#admintool-introduction)

## Chatbot <a name="chatbot-section-start"></a>
### Einleitung <a name="chatbot-introduction"></a>
Der Chatbot ist die Hauptfunktion dieses Projektes. Es ist die erste Seite die ein Admin sieht und die einzige Seite die ein normaler Benutzer sehen soll.

Folgend wird beschrieben was beim laden der Seite in welcher Reihenfolge passiert.
1. [Den Status überprüfen](#check-state)
2. [Char counter laden](#load-char-counter)
3. [Den Chatbot initialisieren](#init-chatbot)

### Status überprüfen <a name="check-state"></a>
Wenn der Chatbot geöffnet wird wird als erstes eine Test Abfrage zum Server geschickt und auf seine Antwort gewartet. Solange auf die Antwort gewartet wird, zeigt der Chatbot eine Nachricht an mit der Information das die "Verbindung zum Server aufgebaut wird".
![Checking state of server](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/checkStatus.jpg)

Um den Status zu überprüfen verwenden wir unseren Service  <code>getStatus()</code> im package <code>com.ubs.backend.services.Get</code>. In dieser Methode werden zwei weitere Methoden überprüft.
1. <code>questionSuggestions(String amountQuestionsString)</code>, package <code>com.ubs.backend.services.Get</code>
2. <code>search(String input, boolean affectStatistics)</code>, package <code>com.ubs.backend.services.IntentFinderNew</code>

JavaDoc zu den erwähnten Methoden
3. [getStatus()](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#getStatus())
4. 

#### Guter Status


### Char counter laden<a name="load-char-counter"></a>
### Chatbot initialisieren<a name="init-chatbot"></a>

## Adminbereich <a name="admintool-section-start"></a>
### Einleitung <a name="admintool-introduction"></a>
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc5OTUwODI1OSwyMDU2NDU5MzM1LC0xND
M1MDA2NjM1LDMyMjk0Njg2MiwxNzYwNTk2NTYyLC0yMTk4Mzk3
NzMsLTE4MTI1MTM5MzUsNjkxMTg2Mzk2LDY1Njk4MTg2NywtNz
gzNDU2OTg2LDE2ODEyNTgwMTYsLTQ5MjA4NDY5OCw1MzA2Mjky
NzQsLTIwODg3NDY2MTJdfQ==
-->