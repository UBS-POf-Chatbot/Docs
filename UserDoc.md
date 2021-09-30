# Benutzer Dokumentation
In diesem Dokument wird beschrieben, wo man was findet, damit der Benutzer mit der Seite umgehen kann.
Dieses Dokument wird in zwei Hauptteile aufgeteilt. Einmal Chatbot an sich selbst und den Adminbereich.

## Inhaltsverzeichnis
### [Chatbot](#chatbot)<a name="tableofcontent-chatbot"></a>
1. [Einleitung](#chatbot-introduction)
2. [Funktionen](#chatbot-functions)

### [Adminbereich](#admintool)<a name="tableofcontent-admintool"></a>
1. [Einleitung](#admintool-introduction)
2. [Anmelden](#admintool-logIn)
3. [Übersicht](#admintool-home)
4. [Antworten](#admintool-answer)
5. [Tags](#admintool-tag)
6. [Matches](#admintool-match)
7. [Blacklist](#admintool-blacklist)
8. [Dateien](#admintool-file)
9. [Fragen](#admintool-question)
10. [Einstellung](#admintool-setting)
11. [Ausloggen](#admintool-exit)

## Chatbot<a name="chatbot"></a>
### Einleitung<a name="chatbot-introduction"></a>
In diesem Abschnitt des Dokumentes beschreiben wir, was alles der Chatbot an sich machen kann.
Wir zählen die Funktionen auf und wie man die benutzt.

### Funktionen<a name="chatbot-functions"></a>
Wenn Sie Chatbot öffnen, sehen Sie dieses Bild.
![chatbot with function](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/chatbot.JPG)

#### Vorschläge
Als Erstes sehen Sie eine Begrüssung von Chatbot mit Vorschlagfragen.
Diese Vorschläge werden anhand von den heute meist beliebte Fragen angezeigt.
Die Fragestellung können Sie in Adminbereich ändern, dies werden Sie in einer späteren Zeit sehen.

#### Chatverlauf
Rechts von Stima den Namen des Chatbots, sehen Sie ein Pfeil, der nach unten zeigt.
Mit dem Knopfklick laden Sie den Chatverlauf in Textdatei herunter.
Wenn Sie die Datei öffnen, sehen Sie das Datum mit den genaueren Uhrzeiten und 
wer geschrieben hat und was geschrieben wurde.

#### Autovervollständigung
Wir haben den Autovervollständigung eingerichtet wie es auf dem Bild zu erkennen ist.
Wenn man in das Feld "ab" schreibt, werden zwei Vorschläge angezeigt.
Sobald Sie auf das Eingabefeld anfangen zu schreiben, sehen Sie automatisch Fragen, die passen würden.
Sie können dies wählen und es gibt Ihnen eine Antwort dazu.
Falls ein Wort nicht da ist, können Sie es späteren in Adminbereich hinzufügen.

## Adminbereich<a name="admintool"></a>
### Einleitung<a name="admintool-introduction"></a>
In diesem Abschnitt des Dokumentes beschreiben, dass Adminbereich.
Damit Sie sich mit dem Adminbereich zurechtkommen.

### Anmelden<a name="admintool-logIn"></a>
Zuerst einmal wie kommt man zum Adminbereich hin.
Sie fragen den Chatbot nach Admintool oder Admin.
Mit dem Klick auf dem Link werden Sie dort gelangen.
Bevor Sie mit Adminbereich arbeiten, melden Sie sich an,
geben Sie ihre Email-Adresse und das Passwort ein.
![logIn-site](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/anmeldung.JPG)

### Übersicht<a name="admintool-home"></a>
Den Adminbereich begrüsst Sie mit Statistiken.
Eine Statistik zeigt an, wie viele Antworten der Chatbot zurückgegeben hat 
in Tagen, Wochen, Monate, Jahren und seit der letzten Anmeldung.
Ebenfalls sehen Sie die Anzahl der beantworteten Antworten und die Menge von unbeantwortet Antworten.
Links davon sehen Sie die Menüleiste.
Wenn Sie mit der Maus durch die Menüleiste durchstreifen, sehen Sie, was die Icons bedeuten.
Das erste ist Home die Übersicht mit Statistiken.

### Antworten<a name="admintool-tag"></a>
Bei der zweiten Seite ist für die Antworten zuständig.
Hier können Sie Antworten hinzufügen, bearbeiten und löschen.
Wenn Sie auf Antworten Hinzufügen klicken, zeigt es Ihnen das Eintragformular an.
Sie können den Titel und Antwort geben.
Es gibt ein Kästchen Versteckt, damit werden die Antworten versteckt.
Diese Antwort wird nicht zu Bewertung mitgezählt.

![answer-site](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/antwort_verstecken.JPG)

Bei Tags hinzufügen können Sie die Schlagwörter schreiben, die zur Antwort passt.
Sie können Schlagwörter benutzen, die es gibt.
Wenn ihr Schlagwort nicht angezeigt wird, speichert es als ein neues Schlagwort.

Es gibt drei Antworttypen, einmal der Typ Normal, den Typ Witz und den Typ Facts.
Der Typ Witz werden alle Witze gespeichert, der Typ Facts sind alle Informationen zum Chatbot.
Der Typ Normal sind die restlichen, üblichen Fragen.

Unter dem gibt es das Feld Datei hinzufügen.
Es werden alle Dateien angezeigt, welche in der Datenbank gespeichert wurde.
Falls die Datei noch nicht da darauf ist, können Sie auf der Dateiseite hinzufügen, welches ich Ihnen später zeigen werde.
Wenn Sie die falsche Datei ausgewählt haben, können Sie jederzeit unten bei der Tabelle löschen und ersetzen.
Nachdem Sie hinzugefügt haben, leitet es Sie direkt zur Bearbeitungsseite, falls Sie Daten ändern müssen.
Sonst können Sie auf der Menüleiste auf Antworten klicken.
Sie können auch die  Daten löschen, indem Sie auf die Antwort klicken und nach unten scrollt und es löschen.
Die Daten können Sie bearbeiten, wenn Sie auf die Antwort klicken und Änderungen vornehmen.

![answer-sort](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/antwort_sortieren.jpg)

Bei Antwortseite können Sie sortieren nach Name, Bewertung und Aufrufe.
Der Name wird aufsteigend und absteigend sortiert.
Bewertung wird ausgerechnet, wenn es kein Upvotes und Downvotes gab, ist es 50%.
Sobald es ein Upvotes gibt, wird es 100% und umgekehrt, wenn es Downvotes, gibt dann 0%.
Aufrufe ist, wie viel es aufgerufen wurde, also wie viel Mal es gefragt wurde.
Sie können auch filtern, ob Sie alle Typen anzeigen wollen, oder ein Bestimmtes.
Ebenfalls können Sie die Bewertung filtern.
Wenn Sie jetzt das Bewertungsfilter auf vier haben, wird alle Bewertung unter 4 angezeigt.
Falls Sie alle Bewertung über 4 anschauen wollen, klicken Sie einfach auf den darüber Knopf.
Sie sehen, der Knopf verändert Sie zu darunter.
Sie können auch nach Antworten suchen.
Wenn Sie alle unvollständige Antworten anzeigen wollen, können Sie auf Antwort ohne Tags ein Häkchen setzen.
Das sind Antworten, die keine Schlagwörter hat.
![answerpage](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/answerpage.JPG)
Wie Sie auf dem Bild sehen, wird Vouchen als Typ Normal beschrieben. Da es kein Facts und Witz ist.
Darunter sehen Sie die Schlagwörter, die dann die Antwort von Vouchen zurückgibt. 
Ebenfalls sehen Sie vouchen und bürgen wurde am meisten verwendet bei der Suche.
Rechts davon sehen Sie Anzahl Aufrufe und die Bewertung.

### Tags<a name="admintool-tag"></a>
Auf die dritte Seite werden Schlagwörter hinzugefügt, bearbeitet und gelöscht.
Es ist gleich dargestellt wie die Antwortseite. Wenn Sie oben rechts auf den Knopf Tag Hinzufügen klicken, sehen Sie ein Hinzufügen Formular.
Sie geben das Schlagwort ein und fügen es hinzu. Das Hinzufügen können Sie auch direkt auf der Antwortseite machen.
Dasselbe hier Sie können hier sortieren nach Name, Bewertung  und Verwendung.
Bewertung wie so dargestellt, wenn es kein Upvotes und Downvotes gab, ist es 50%;
Sobald es ein Upvotes gibt, wird es 100% und umgekehrt, wenn es Downvotes gibt dann 0%
Sie können auch nach Schlagwörter suchen.

### Matches<a name="admintool-match"></a>
Auf der Matches-Seite können Sie Matches zurücksetzen, nicht übersetzen, blacklisten.
Was genau ist ein Matches, wenn man Feren schreibt anstatt Ferien 
wird es trotzdem verstehen, dass die Person nach Ferien sucht.
![matches](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/matches.JPG)
Doch wenn Wörter sind, die nicht richtig verstanden wird, können Sie auf nicht übersetzen klicken.
Wie zum Beispiel Sie suchen nach buchen, aber Chatbot gibt die Antwort zu vouchen. Dann können Sie auf nicht übersetzen drücken.

Wenn es Wörter sind, welche man nicht auf dem Chatbot speichern will, kann man es zur Blacklist hinzufügen.

Wenn Sie zurücksetzen, werden die Upvotes und Downvotes auf null gesetzt.
Matches setzt man zurück, wenn es falsch Upvotes und Downvotes gezählt wurde.

Hier können Sie ebenfalls nach Name und Bewertung aufsteigend absteigend sortieren.
Die Suchfunktion ist beim Matches auch verfügbar.
 
### Blacklist<a name="admintool-blacklist"></a>
Auf der Blacklistseite können Sie Wörter eintragen, welche nicht eine Antwort liefern soll.
Sie können Blacklist eintragen, bearbeiten und löschen.
Sie sehen, wie viel Mal es verwendet wurde.
Hier können Sie sortieren nach Name aufsteigend und absteigend.
Die Suchfunktion ist beim Blacklist verfügbar.

### Dateien<a name="admintool-file"></a>
Auf der Dateiseite können Sie Dateien hochladen, die Sie für Antwort brauchen. Mit Klick können Sie eine Einsicht haben. Sie können die Dateien löschen.
 
### Fragen<a name="admintool-question"></a>
Auf der Frageseite können Sie Fragen hinzufügen, bearbeiten und löschen.
Oben sehen Sie die momentane vorgeschlagene Fragen. Sie können diese bearbeiten oder auch löschen.
Unten sehen Sie benutzerdefinierte Fragen, die tauchen auf, wenn es noch keine beliebten Fragen von heute gibt.
Sie können ebenfalls die beantworteten Fragen ansehen.
Da sehen Sie, es wurde eingeteilt in Stunde, heute, Woche, Monat, Jahr, alle und seit letztem Login.
Dasselbe bei unbeantwortete Fragen.

### Einstellung<a name="admintool-setting"></a>
Bei der Einstellungen können Sie Ihr Passwort ändern.  Wenn Sie die Berechtigung haben Benutzer zu erstellen, können Sie Benutzer erstellen.
Sie können auch ein Häkchen setzen, wenn die erstellte Benutzer auch das Recht zum Benutzer erstellen hat.
Ganz unten sehen Sie alle Benutzer mit Daten, ob er Nutzer erstellen kann, wann er zuletzt angemeldet war.
Wenn Sie auf eine Benutzer klicken, sehen Sie dieses Bild mit dem Namen. Hier haben wir es ausgeblendet.
![setting-details](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/benutzer_bearbeiten.JPG)
Sie können Benutzer löschen oder auch das Passwort zurücksetzen.
Das Recht zum Benutzer erstellen können Sie auch wegnehmen.
Dies können Sie nur machen, wenn Sie ein Admin sind.

Was man noch beachten muss, man ist eingeschränkt, wenn es um die Bearbeitung um sich selbst geht.
Sie können sich selber kein Recht geben oder nehmen und Ihr Passwort können Sie selber nicht zurücksetzen.

### Ausloggen<a name="admintool-exit"></a>
Wenn Sie ausloggen, werden Sie direkt auf der Anmeldungsseite geleitet.