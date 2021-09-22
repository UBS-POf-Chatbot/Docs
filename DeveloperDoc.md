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

Um den Status zu überprüfen verwenden wir unseren Service  [<code>getStatus()</code>]() ([JavaDoc](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#getStatus())). Diese Methode ruft folgende Methoden auf.
1. <code>questionSuggestions(String amountQuestionsString)</code>, package <code>com.ubs.backend.services.Get</code>. ([JavaDoc](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/Get.html#questionSuggestions(java.lang.String)))
2. <code>search(String input, boolean affectStatistics)</code>, package <code>com.ubs.backend.services.IntentFinderNew</code>. ([JavaDoc](https://ubs-pof-chatbot.github.io/JavaDoc/com/ubs/backend/services/IntentFinderNew.html#search(java.lang.String,boolean)))

#### Guter Status


### Char counter laden<a name="load-char-counter"></a>
### Chatbot initialisieren<a name="init-chatbot"></a>

## Adminbereich <a name="admintool-section-start"></a>
### Einleitung <a name="admintool-introduction"></a>
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg1ODE2MTkwMywxNjA2MzM5NTc4LDIwNT
Y0NTkzMzUsLTE0MzUwMDY2MzUsMzIyOTQ2ODYyLDE3NjA1OTY1
NjIsLTIxOTgzOTc3MywtMTgxMjUxMzkzNSw2OTExODYzOTYsNj
U2OTgxODY3LC03ODM0NTY5ODYsMTY4MTI1ODAxNiwtNDkyMDg0
Njk4LDUzMDYyOTI3NCwtMjA4ODc0NjYxMl19
-->