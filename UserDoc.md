# Benutzer Dokumentation

In diesem Dokument wird beschrieben, wo man was findet, damit der Benutzer mit der Seite umgehen kann. Dieses Dokument
wird in zwei Hauptteile aufgeteilt. Einmal Chatbot an sich selbst und den Adminbereich. Sie können die Dokumentation
jederzeit auch in Adminbereich öffnen.

## Inhaltsverzeichnis

### [Chatbot](#chatbot)<a name="tableofcontent-chatbot"></a>

1. [Einleitung](#chatbot-introduction)
2. [Funktionen](#funktionen)

### [Adminbereich](#adminbereich)<a name="tableofcontent-admintool"></a>

1. [Einleitung](#admintool-introduction)
2. [Anmelden](#anmelden)
3. [Übersicht](#übersicht)
4. [Antworten](#antworten)
5. [Tags](#tags)
6. [Matches](#matches)
7. [Blacklist](#blacklist)
8. [Dateien](#dateien)
9. [Fragen](#fragen)
10. [Einstellung](#einstellung)
11. [Ausloggen](#ausloggen)

## Chatbot

### Einleitung <a name="chatbot-introduction"></a>

In diesem Abschnitt des Dokumentes beschreiben wir, was alles der Chatbot an sich machen kann. Wir zählen die Funktionen
auf und wie man die benutzt.

### Funktionen

Wenn Sie Chatbot öffnen, sehen Sie dieses Bild.
![chatbot with function](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/chatbot.JPG)

#### Vorschläge

Als Erstes sehen Sie eine Begrüssung vom Chatbot mit Vorschlagfragen. Diese Vorschläge werden anhand von den meist
bewerteten Fragen dieses Monats. Die Fragestellung können Sie in Adminbereich ändern, dies werden Sie in einer späteren
Zeit sehen.

#### Chatverlauf

Oben rechts auf der Seite, sehen sie einen Pfeil, der nach unten zeigt. Mit einem Linksklick darauf laden Sie den
Chatverlauf in Textdatei herunter. Wenn Sie die Datei öffnen, sehen Sie das Datum mit den genaueren Uhrzeiten und wer
geschrieben hat und was geschrieben wurde.

#### Autovervollständigung

Wir haben die Autovervollständigung eingerichtet, wie es auf dem Bild zu erkennen ist. Wenn man in das Feld etwas hinein
schreibt, kommen Vorschläge unter dem Eingabefeld. Mit Tab und den Pfeiltasten oder mit einem Linksklick kann man einen
Vorschlag auswählen.

#### Upvotes und Downvotes

![upvotes-downvotes](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/upvotes_downvotes.JPG)

Nachdem Sie eine Frage gestellt haben, wird Ihnen eine Antwort geliefert. Falls die Antwort behilflich war, können Sie
einen Daumen hochdrücken. Wenn es die falsche Antwort gibt, können Sie einen Daumen runter klicken. Mit dieser Hilfe
können wir sehen, woran es liegt, dass es so schlecht bewertet wurde.

## Adminbereich

### Einleitung <a name="admintool-introduction"></a>

In diesem Abschnitt des Dokumentes beschreiben wir das Adminbereich. Damit Sie sich mit dem Adminbereich zurechtkommen.

### Anmelden

![logIn-site](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/anmeldung.JPG)

Zuerst einmal wie kommt man zum Adminbereich hin. Sie fragen den Chatbot nach Admintool oder Admin. Mit dem Klick auf
dem Link werden Sie dorthin gelangen. Bevor Sie mit Adminbereich arbeiten, melden Sie sich an, geben Sie ihre
E-Mail-Adresse und das Passwort ein.

### Übersicht

![statistik-2](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/statistik_2.JPG)

Im Admintool werden Sie direkt mit Statistiken begrüsst. Eine Statistik zeigt an, wie viele Antworten der Chatbot
zurückgegeben hat in Tagen, Wochen, Monate, Jahren und seit der letzten Anmeldung. Ebenfalls sehen Sie die Anzahl der
beantworteten Fragen und die Menge von unbeantwortet Fragen. Links davon sehen Sie die Menüleiste. Falls Sie nur die
beantwortete Fragen ansehen wollen, können Sie bei der Legende auf Anzahl unbeantworteter Fragen klicken. Somit
streichen Sie es durch, dasselbe können Sie mit den unbeantworteten Fragen machen. Wenn Sie mit der Maus durch die
Menüleiste durchstreifen, sehen Sie, was die Icons bedeuten. Das Erste ist Home die Übersicht mit Statistiken.

### Antworten

Die zweite Seite ist für die Antworten zuständig. Hier können Sie Antworten hinzufügen, bearbeiten und löschen. Wenn Sie
auf "Antworten Hinzufügen" klicken, zeigt es Ihnen das Eintragformular an. Hier kann man der Antwort einen Titel und
Antwort geben. Wenn Sie einen Link zur Antwort hinzufügen wollen, müssen Sie ein wenig <code>html</code> schreiben.
Wir nehmen als Beispiel den GTRS Link. Sie geben in Antwort diesen Link ein 
```  html
<a href="https://goto/gtrs">goto/gtrs</a>
``` 

href="xxx" beim xxx schreiben Sie den Link auf. Sobald < a > schliesst, können Sie den Text schrieben, welche verlinkt wird.
Falls Sie den Link auf einen neuen Tab öffnen wollen, schreiben Sie <code>target="_blank"</code> nach dem Link (href="xxx"). 
Damit es keine Verwirrung gibt, ist hier ein Beispiel dazu 
```   html
<a href="https://goto/gtrs" target="_blank">GTRS</a>
```
. 
Es gibt das Kästchen "Versteckt", damit werden für diese Antwort keine Statistiken erstellt. Das
bedeutet, dass diese Antwort nicht zu Bewertung mitgezählt werden. Diese Antworten werden auch nicht bei den Statistiken
vorkommen.

![answer-site](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/antwort_verstecken.JPG)

Bei Tags hinzufügen können Sie die Schlagwörter schreiben, die zur Antwort passen. Sie können Schlagwörter benutzen, die
es gibt. Wenn ihr Schlagwort nicht angezeigt wird, speichert es als ein neues Schlagwort.

![answer-typ](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/antwort_typ.JPG)
Es gibt drei Antworttypen, einmal der Typ Normal, den Typ Witz und den Typ Facts. Der Typ Witz werden alle Witze
gespeichert, der Typ Facts sind alle Informationen zum Chatbot. Der Typ Normal sind die restlichen üblichen Fragen.

Falls Sie ein Witz einfügen, müssen Sie die Schlagwörter nicht schreiben, es wird Ihnen automatisch hinzugefügt. Die
Witze haben immer die gleichen Schlagwörter, die bei der Antwort nach Zufall zugeschickt wird. Beim Facts funktioniert
es gleich, wenn Sie den Typ Facts auswählen, wird es automatische die dazugehörigen Schlagwörter hinzufügen.

Unter den Typen gibt es das Feld Datei hinzufügen. Es werden alle Dateien angezeigt, welche in der Datenbank gespeichert
wurde. Falls die Datei noch nicht da darauf ist, können Sie auf der Dateiseite hinzufügen, welches ich Ihnen später
zeigen werde. Wenn Sie die falsche Datei ausgewählt haben, können Sie jederzeit unten bei der Tabelle löschen und
ersetzen. Nachdem Sie hinzugefügt haben, leitet es Sie direkt zur Bearbeitungsseite, falls Sie Daten ändern müssen.
Sonst können Sie auf der Menüleiste auf Antworten klicken. Sie können auch die Daten löschen, indem Sie auf die Antwort
klicken und nach unten scrollt und es löschen.
![answer-statistik](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/antwort_statistik.JPG)

Die Daten können Sie bearbeiten, wenn Sie auf die Antwort klicken und Änderungen vornehmen. Sie können auch dort direkt
auf einen Tag klicken und dies bearbeiten. Bei der Bearbeitung von Antworten können Sie auch Statistik sehen, darin
stehen alle Fragen, die gestellt wurden, um diese Antworten zu bekommen.
![answer-sort](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/antwort_sortieren.jpg)
Nun kommen die Sortierfunktion, man kann nach Name, Bewertung und Aufrufe sortieren. Bei jeder Seite können Sie nach
Name aufsteigend und absteigend sortieren. Sie können auch Bewertung und Aufrufe gleich wie Name sortieren.

Bewertung wird ausgerechnet mit Downvotes und Upvotes. Wenn es kein Upvotes und Downvotes gab, ist es 50%. Sobald es ein
Upvotes gibt, wird es 100% und umgekehrt, wenn es Downvotes gibt, dann ist es 0%. Aufrufe sind, wie viel es aufgerufen wurde,
also wie viel Mal es gefragt wurde. Sie können auch filtern, ob Sie alle Typen anzeigen wollen oder ein Bestimmtes. Es
gibt auch eine Filterfunktion für die Bewertung. Wenn Sie jetzt die Bewertung auf vier schieben, wird alle Bewertung
unter 4 angezeigt. Falls Sie alle Bewertung über 4 anschauen wollen, klicken Sie einfach auf den darüber Knopf. Sie
sehen, der Knopf verändert Sie zu darunter.

Wenn Sie eine bestimmte Antwort brauchen, können Sie unsere Suchfunktion verwenden. Wenn Sie alle unvollständige
Antworten anzeigen wollen, können Sie auf Antwort ohne Tags ein Häkchen setzen. Das sind Antworten, die keine
Schlagwörter haben.
![answerpage](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/answerpage.JPG)
Wie Sie auf dem Bild sehen, wird Vouchen als Typ Normal beschrieben. Da es kein Facts und Witz ist. Darunter sehen Sie
die Schlagwörter, die zur Antwort Vouchen zurückgibt. Ebenfalls sehen Sie vouchen und bürgen wurde am meisten verwendet
bei der Suche. Dies erkennen anhand der Farbe. Rechts davon sehen Sie die Anzahl von Aufrufe und Bewertungen.

### Tags

Auf die dritte Seite werden Schlagwörter hinzugefügt, bearbeitet und gelöscht. Es ist gleich dargestellt wie die
Antwortseite. Wenn Sie oben rechts auf den Knopf Tag Hinzufügen klicken, sehen Sie ein Hinzufügen Formular. Sie geben
das Schlagwort ein und fügen es hinzu. Natürlich können Sie das Hinzufügen auch direkt auf der Antwortseite machen.
Dasselbe hier Sie können hier sortieren nach Name, Bewertung und Verwendung. Die Suchfunktion haben Sie für die
Schlagwörter auch.
![edit-tag](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/tag_bearbeiten.JPG)

Wenn Sie auf ein Schlagwort klicken, können Sie die bearbeiten. Dazu sehen Sie die dazugehörige Antwort. Sie können die
Antwort bearbeiten, indem Sie auf die Antwort klicken.

### Matches

Auf der Matches-Seite können Sie Matches zurücksetzen, nicht übersetzen, blacklisten. Was genau ist ein Match, wenn man
Feren schreibt anstatt Ferien wird es trotzdem verstehen, dass die Person nach Ferien sucht.
![matches](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/matches.JPG)
Doch wenn Wörter sind, die nicht richtig verstanden wird, können Sie auf nicht übersetzen klicken. Wie zum Beispiel Sie
suchen nach buchen, aber Chatbot gibt die Antwort zu vouchen. Dann können Sie auf nicht übersetzen drücken.

Wenn es Wörter sind, welche man nicht auf dem Chatbot speichern will, kann man es zur Blacklist hinzufügen.

Wenn Sie zurücksetzen, werden die Upvotes und Downvotes auf null gesetzt.

Hier können Sie ebenfalls nach Name und Bewertung aufsteigend oder absteigend sortieren. Die Suchfunktion ist beim
Matches auch verfügbar. Bei der Tabelle können Sie auf den Tag klicken und leitet Sie zum Tag bearbeiten.

### Blacklist

Auf der Blacklistseite können Sie Wörter eintragen, welche nicht als Frage oder Wort gespeichert werden soll. Sie können
Blacklist eintragen, bearbeiten und löschen. Sie sehen, wie viel Mal es verwendet wurde. Hier können Sie sortieren nach
Name aufsteigend und absteigend. Die Suchfunktion ist beim Blacklist verfügbar.

### Dateien

Auf der Dateiseite können Sie Dateien hochladen, die Sie für Antwort brauchen. Mit Klick können Sie eine Einsicht haben.
Sie können die Dateien löschen.

### Fragen

Auf der Frageseite können Sie Fragen hinzufügen, bearbeiten und löschen. Oben sehen Sie die momentanen vorgeschlagenen
Fragen. Sie können diese bearbeiten oder auch löschen. Unten sehen Sie benutzerdefinierte Fragen, die tauchen auf, wenn
es noch keine beliebten Fragen von heute gibt.
![answered-question](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/fragen_beantwortete_fragen.JPG)

Sie können ebenfalls die beantworteten Fragen ansehen. Wenn Sie auf die Frage klicken, können diese bearbeiten und
sehen, welche Antwort es liefert. Da sehen Sie, es wurde eingeteilt in Stunde, heute, Woche, Monat, Jahr, alle und seit
letztem Login. Dasselbe funktioniert es bei unbeantworteten Fragen.

### Einstellung

![change-password](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/passwort_aendern.JPG)
Wenn Sie keine Berechtigung zum Benutzer erstellen haben, sehen Sie nur die Funktion, um Passwort zu ändern. Bei den
Einstellungen können Sie Ihr Passwort ändern, Sie geben das gegebene Passwort und ändern mit Ihrem neuen Passwort. Sie
müssen wegen Sicherheit das Passwort ein zweites Mal eingeben für die Bestätigung.

Benutzer mit der Berechtigung "Kann neue Nutzer erstellen" können neue Benutzer erstellen, bearbeiten, löschen und das
Passwort von den Benutzern zurücksetzen. Sie können auch im nachhinein dem Benutzer die Rechte geben oder wieder
wegnehmen. Ganz unten sehen Sie alle Benutzer mit einigen Informationen. Zum Beispiel können Sie sehen, welche Benutzer
das Recht haben, andere Benutzer zu erstellen und Sie sehen auch, wann sich welcher Benutzer zuletzt angemeldet hat. Wenn
Sie auf einen Benutzer klicken, sehen Sie dieses Bild mit dem Namen. Hier haben wir der Benutzername ausgeblendet.
![setting-details](https://raw.githubusercontent.com/UBS-POf-Chatbot/Docs/main/images/userDoc/benutzer_bearbeiten.JPG)
Sie können Benutzer löschen oder auch das Passwort jenes Benutzers zurücksetzen. Sie können dem Benutzer das Recht zum
Erstellen weiterer Benutzer geben oder wegnehmen. Nur Benutzer mit der Berechtigung können auf diese Seite zugreifen.

Man muss noch beachten, dass man eingeschränkt ist, wenn es um die Bearbeitung von sich selbst geht. So können sie sich
selber zum Beispiel kein Recht geben oder nehmen und können sich selber nicht löschen.

### Ausloggen

Wenn Sie sich ausloggen, werden Sie direkt auf die Anmeldungsseite geleitet.

<sup>Autor: [Sarah Ambi](https://github.com/SarahAmbi) </sup>
<br>
<sup>Zuletzt bearbeitet: 07.10.2021</sup>