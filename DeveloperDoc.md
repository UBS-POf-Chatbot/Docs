# Entwickler Dokumentation
In diesem Dokument wird beschrieben wie der Chatbot funktioniert und wo was zu finden ist, damit zukünftige Entwickler ohne Probleme den Chatbot weiterentwickeln können.
Dieses Dokument wird in zwei Hauptteile aufgeteilt. Einmal der Chatbot an sich und einmal den Adminbereich.

## Inhaltsverzeichnis
### [Chatbot](#chatbot-section-start)<a name="tableofcontent-chatbot"></a>
 1. [Einleitung](#chatbot-introduction)
 2. [Den Status überprüfen](#check-state)
 3. [Wörter Vorschläge laden](#load-tag-suggestions)
 4. [Char counter laden](#load-char-counter)
 5. [Den Chatbot initialisieren](#init-chatbot)

### [Adminbereich](#admintool-section-start)<a name="tableofcontent-admintool"></a>
1. [Einleitung](#admintool-introduction)

## Chatbot <a name="chatbot-section-start"></a>
### Einleitung <a name="chatbot-introduction"></a>
Der Chatbot ist die Hauptfunktion dieses Projektes. Es ist die erste Seite die ein Admin sieht und die einzige Seite die ein normaler Benutzer sehen soll.

Folgend wird beschrieben was beim laden der Seite in welcher Reihenfolge passiert.
1. [Den Status überprüfen](#check-state)
2. [Wörter Vorschläge laden](#load-tag-suggestions)
3. [Char counter laden](#load-char-counter)
4. [Den Chatbot initialisieren](#init-chatbot)

### Status überprüfen <a name="check-state"></a>
Wenn der Chatbot geöffnet wird wird als erstes eine Test Abfrage zum Server geschickt und auf seine Antwort gewartet. Solange auf die Antwort gewartet wird, zeigt der Chatbot eine Nachricht an mit der Information das die "Verbindung zum Server aufgebaut wird".
![Checking state of server](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/checkStatus.jpg)
#### Guter Status


### Wörter Vorschläge laden<a name="load-tag-suggestions"></a>
### Char counter laden<a name="load-char-counter"></a>
### Chatbot initialisieren<a name="init-chatbot"></a>

## Adminbereich <a name="admintool-section-start"></a>
### Einleitung <a name="admintool-introduction"></a>
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzIyOTQ2ODYyLDE3NjA1OTY1NjIsLTIxOT
gzOTc3MywtMTgxMjUxMzkzNSw2OTExODYzOTYsNjU2OTgxODY3
LC03ODM0NTY5ODYsMTY4MTI1ODAxNiwtNDkyMDg0Njk4LDUzMD
YyOTI3NCwtMjA4ODc0NjYxMl19
-->