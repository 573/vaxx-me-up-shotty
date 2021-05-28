# vaxx-me-up-shotty (tl;dr [impf.side runterladen](/../../raw/main/impf.side) und in Selenium IDE öffnen)
Tool to get vaccinated ASAP

## Voraussetzungen

Registrierung im Impfportal Sachsen [hier](https://sachsen.impfterminvergabe.de/) möglich. Möglicherweise wird dort auf der Website die folgende Meldung angezeigt

>Aufgrund der vielen Anfragen befinden Sie sich aktuell in der Warteschlange. Sie werden automatisch weitergeleitet, sobald Kapazitäten frei werden. Wir bitten um etwas Geduld.

Dann das Script noch zuende laufen lassen (falls das Impfportal innerhalb des Timeout-Intervalls noch die Loginseite lädt), dann bitte ggf. zu einem anderen Zeitpunkt ([Zeittafel beachten](https://drksachsen.de/)) erneut versuchen. Trifft auch für bereits registrierte Nutzer zu, wenn das Script mit dieser Portalseite blockiert wird.
![drktermine (https://drksachsen.de/)](https://user-images.githubusercontent.com/123878/119958123-063a7180-bfa3-11eb-8cee-fd10179c9306.png)

Das Script bzw. die Datei [impf.side](/../../raw/main/impf.side) wird in einer Browsererweiterung geladen und diese dann ausgeführt. Diese Browsererweiterung gibt es hier, bitte im Browser installieren:
* <a href="https://addons.mozilla.org/en-GB/firefox/addon/selenium-ide/" target="_blank" rel="noopener">Firefoxbrowser</a>
* <a href="https://chrome.google.com/webstore/detail/selenium-ide/mooikfkahbdckldjjndioackbalphokd" target="_blank" rel="noopener">Chromebrowser</a>

Die Vorgangskennung und das Passwort, das seitens des Impfportals vergeben wurde, vor Ausführen des Tests ersetzen, wie folgt:
In der *Selenium-IDE mit geladenem Script* in Spalte "Value" `hier Vorgangskennung eingeben` bzw. `hier Passwort eingeben` ersetzen durch Eure Daten.

## Script in der Selenium-IDE laden

Step 1 - [impf.side](/../../raw/main/impf.side) *öffnen* in der Browsererweiterung
![Im-Imp-Side-Datei-Laden](https://user-images.githubusercontent.com/123878/112589006-a7b91180-8e00-11eb-991d-19bda60a9730.png)

Step 2 - *Vorgangskennung* ändern
![Im-Vorgangskennung](https://user-images.githubusercontent.com/123878/112589074-c5867680-8e00-11eb-8438-db429c83bb46.png)

Step 3 - *Passwort* ändern
![Im-Passwort](https://user-images.githubusercontent.com/123878/112589104-cfa87500-8e00-11eb-9fb0-de78f3f712db.png)

Step 4 - Ausführung des Scripts via *Run current test* starten
![Im-Script-Ausführen](https://user-images.githubusercontent.com/123878/112589138-e18a1800-8e00-11eb-8e02-a68b0e005782.png)

## Alternativen

[Hier](https://impfee.ch/site/) gibt es Impfdosen, die sonst verfallen würden.

## Probleme / Anregungen
Nutzt bitte den [issues tracker](/../../issues) oder regt [eine Diskussion](/../../discussions) an.

## TROUBLESHOOTING
Falls es Probleme bei noch nicht vorhandenem Termin, d. h. ganz neu zu vereinbarendem, nicht nur zu änderndem Termin gibt, ggf. in der Selenium-IDE mit geladenem Script in Spalte "Target" die Zeile `xpath=(//span[@class='select2-selection__arrow'])[2]` ändern auf `xpath=(//span[@class='select2-selection__arrow'])[1]`.

Wenn der vereinbarte Termin doch nicht so recht passt, das Script neustarten, zuvor jedoch auf jeden fall die Zeile `xpath=(//span[@class='select2-selection__arrow'])[1]` (die 1 hier ist entscheidend) (wieder) auf `xpath=(//span[@class='select2-selection__arrow'])[2]` (zurück)setzen. Hintergrund: Es handelt sich nicht (mehr) um eine Neuvereinbarung, sondern um eine Änderungsvereinbarung.

Das Script muss by default im Vordergrund laufen, d. h. wenn vor dem Browserwindow mit der Impfterminseite andere Fenster liegen, kann es zu Verbindungsabbrüchen etc. kommen und ein Scriptneustart erforderlich werden. Um dies zu umgehen, kann der Headless-Modus (https://github.com/SeleniumHQ/selenium-ide/issues/300) probiert werden.

## Entwickler-Notes
Der Defaultwert von einer Minute Wartezeit zwischen den Anfragen sollte nicht unterschritten werden.
Bitte nutzt das Script verantwortungsbewusst.

Für Very-Basic Tests (statt `<click xpath>` bspw. `store xpath count <xpath>`) ist es auch mgl sich einen Zwischenstand der Portalseite also bis zu der Teilseite, bis zu der man sich durchgeklickt hat, zwischenzuspeichern (im Dateidialog "ganze Webseite" bzw. "komplett") und dann erst den Ordner und dann die Html-Datei jeweils in index bzw. index.html umzubenennen und dann via `python -m http.server 8000` bspw. lokal diese extrem basische Version zu hosten. In der IDE gehört dann localhost:8000 in das Baseurl-Feld bzw. das open-Command. Selenium IDE kann leider nicht mit file:///-Urls arbeiten, that's why. Die Console im Browser tut es aber meist auch (`$x("<xpath-expression>")`).

<!--
Referenzen:  
https://stackoverflow.com/a/35247980/3320256  
https://stackoverflow.com/a/3676557/3320256  
Web-Console (Ctrl-Shift-K) and start typing for tests:  
https://stackoverflow.com/a/13572682
-->

