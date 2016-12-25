SpecialJump
===========

Plugin zum schnellen manuellen �berspringen von Werbung (und mehr)
------------------------------------------------------------------
by Fischreiher

Algorithmus:
------------

Beim Topfield TF5000-PVR gab es ein geniales Plugin (QuickJump) zum schnellen �berspringen von Werbung, das nach dem Prinzip der "bin�ren Suche" funktionierte.  
Der Anwender musste dabei anhand des dargestellten Bildinhalts entscheiden, ob bereits zu weit gesprungen wurde (Sendung nach der Werbepause) oder noch nicht weit genug.  
Gesprungen wurde mit zwei Tasten vor und zur�ck, wobei sich der Sprungabstand ab dem ersten Richtungswechsel halbierte, z.B. bei einer Werbepause von 7:41:

>">"  springt +2:00  zu +2:00 vor  
>">"  springt +2:00  zu +4:00 vor  
>">"  springt +2:00  zu +6:00 vor  
>">"  springt +2:00  zu +8:00 vor - oops, zu weit ...  
>"<"  springt -1:00  zu +7:00 zur�ck  
>">"  springt +0:30  zu +7:30 vor  
>">"  springt +0:15  zu +7:45 vor - zu weit ..  
>"<"  springt -0:08  zu +7:37 zur�ck  
>">"  springt +0:04  zu +7:41 vor - Treffer

Aufgrund von Patenten auf �hnliche Algorithmen (Loewe Opta GmbH DE200410036013, DE102008055504) w�rde ich nie auf die Idee kommen, so etwas zu schreiben oder zu ver�ffentlichen.  
Patentiert u.a. ist ein Algorithmus, der bei jedem Richtungswechel die Sprungdistanz um einen konstanten Faktor �ndert.
W�hrend der patentierte Algorithmus die Sprungdistanz nur bei jedem Richtungswechel �ndert, geschieht dies bei SpecialJump bei jedem Sprung ab dem ersten Richtungswechsel. In dieser Hinsicht entspricht SpecialJump besser dem Prinzip der "bin�ren Suche" und ben�tigt weniger Tastendr�cke.  
Allerdings verwendet SpecialJump, abweichend vom Patent, programmierbare Eintr�ge einer Liste als Sprungdistanzen. Diese stehen per default in keinem konstanten Verh�ltnis zueinander, und die Sprungdistanz wird teils verringert, teils vergr��ert. Darunter leidet der Nutzen erheblich.  
Falls ein User in der Liste z.B. 2:00, 1:00, 0:30, 0:15, 0:08 und 0:04 eintragen w�rde, um das Plugin zur "bin�ren Suche" zu missbrauchen, k�nnte dies eine Patentverletzung darstellen.

Features Sprungfunktionen:
--------------------------

- SpecialJump zum schnellen �berspringen von Werbung mit 2 Tasten
- 8 programmierbare feste Spr�nge
- Audio Stummschaltung f�r programmierbare Zeit nach jedem Sprung (angenehme Ruhe beim �berspringen der Werbung)
- feste Spr�nge erlauben gleichzeitige Umschaltung auf einen einstellbaren Audio-Track ("sag das nochmal auf Deutsch")
- feste Spr�nge erlauben gleichzeitige Umschaltung auf einen einstellbaren Subtitle-Track ("sag das nochmal mit Untertiteln")
- Tastenfunktion zum schnellen Toggeln des Audio- oder Subtitle-Tracks mit einer Taste (ohne sich durch Men�s zu hangeln)
- Tastenfunktion zum Dunkelschalten des Displays (f�r puristische Cineasten)
- Optional verschiedene feste Lautst�rkewerte f�r TV-Betrieb und die einzelnen Tracks von Videos (Angleichen der Lautst�rke verschiedener Tracks, nur sinnvoll, wenn die Fernbedienung die Lautst�rke des Fernsehers steuert)
- Tastenbelegung aller Funktionen �ber die keymap (/usr/lib/enigma2/python/Plugins/Extensions/SpecialJump/keymap_user.xml bzw. /usr/share/enigma2/keymap.usr)
- Neu: Einige vordefinierte keymaps zur Auswahl im Men�, Beschreibung der Tastenfunktionen (siehe Beitrag #147 http://www.opena.tv/plugins/6240-spe...tml#post247369)

Verbesserungen im Bedienkomfort:
--------------------------------

- Fast Zap Mode (beschleunigte Umschaltzeiten durch vorausschauendes Vorladen des n�chsten Senders auf einem weiteren Tuner) - siehe Beitrag #15 http://www.opena.tv/plugins/6240-spe...tml#post130140 - jetzt auch ohne Verbiegen der Tastenbelegung (bei Auswahl der "keymap_FastZap_only.xml")
- Direktes Zur�ckspringen in den Timeshift-Buffer aus dem Live-TV-Betrieb m�glich (ohne SpecialJump nur �ber Pause oder Rewind m�glich)
- Mehrfachspr�nge im pausierten Zustand m�glich (ohne SpecialJump wird bei mehreren Spr�ngen nicht um die Summe der Spr�nge gesprungen, sondern nur um die Distanz des jeweils letzten Sprunges)
- Nach dem Wegzappen aus dem Timeshift ist ein erneutes Zappen sofort m�glich (ohne SpecialJump erst nach 3 Sekunden).

Doppelbelegung der P+ und P- Tasten (KEY\_CHANNELUP und KEY\_CHANNELDOWN):
------------------------------------------------------------------------

- Zappen im Live-TV-Betrieb
- Pause (P-) / Play (P+) bei der Wiedergabe von Videos
- Pause (P-) / Play (P+) w�hrend Timeshift
- Schutz des Timeshift-Buffers im Live-TV-Betrieb:
  - ab einer einstellbaren Buffer-Gr��e kein Zappen, sondern Pause/Play mit Warnung
  - Zappen ist dann durch Doppelbet�tigung P+ / P- m�glich
  - empfohlene Einstellung: 5s f�r P- (zum bequemen Pausieren des live-TV mit P- auch recht kurz nach dem Senderwechsel) / 30min f�r P+ (Zappen klappt fast immer, nur ein gro�er Timeshift-Buffer wird gesch�tzt)

Status:
-------

- Prinzipiell funktioniert alles auf Gigablue Quad unter openATV. Andere Boxen habe ich nicht, andere Images werde ich erst einmal nicht testen, aber auf Zuruf getestete Patches einbauen, um Problem mit anderen Boxen und Images zu beheben.
- Die Infoboxen, die den Audio- und Untertitel-Track anzeigen, haben manchmal einen d�nnen hellen Rahmen, manchmal nicht. Ursache unbekannt. Wen st�rt's?
- Wird im pausierten Zustand drei mal der Audio-Track getoggelt (bei einem Video mit 2 Audiotracks), gibt's einen Spinner.
- Das Konzept der Doppelbelegung von P+/P- ist nicht optimal. Der User wei� nicht, wann P- pausiert und wann P- zappt. P+ ist klar. Daher sind f�r den Schutz von "P-" nur kleine Werte sinnvoll. 
- F�r den Schutz des Timeshift-Buffers kann die Gr��e des Buffers nur in kByte, nicht in Sekunden ermittelt werden, da die timeshift position am EOF (live TV) ist. Ich rechne mit gesch�tzter Datenrate um (1kB=1ms).
- Statt die SpecialJumpInfoBar in jeder Skin individuell zu skinnen, k�nnte es sinnvoller sein, die einzig neue Information (SJJumpTime) in die vorhandenen Infobars "einzublenden".


Build (das macht nur der Autor):
--------------------------------

> cd /tmp; chmod 755 /usr/lib/enigma2/python/Plugins/Extensions/SpecialJump/ipkg-build ; /usr/lib/enigma2/python/Plugins/Extensions/SpecialJump/ipkg-build

Installation:
-------------

Das Plugin ist auf dem normalen openATV Feed verf�gbar.

Alternative manuelle Installation:

> cd /tmp  
> opkg install /tmp/enigma2-plugin-extensions-specialjump\_0.7-20140502-r0\_mips32el.ipk  
> reboot

FAQ:
----

1. Warum SpecialJump? Ich habe doch die Zifferntasten zum Springen?  
      Das Springen mit nur zwei Tasten ist wesentlich komfortabler und kann deutlich schneller und genauer zum Ziel f�hren. Dies ist abh�ngig von den eingestellten Sprungwerten: Ideal w�re die (leider patentierte) "bin�re Suche", f�r die das Plugin rein theoretisch missbraucht werden k�nnte.

2. Warum kann die Tastenbelegung nicht im Konfigurationsmen� des Plugins eingestellt werden?  
      Es gibt Plugins, die diesen Komfort f�r wenige Tasten bieten, z.B. Multiquickbutton. Ein Plugin, das viele Tasten auf diese Weise verwaltet, wird aber schnell gro�, langsam und inkompatibel mit anderen Plugins.  
      Unter /usr/lib/enigma2/python/Plugins/Extensions/SpecialJump/keymap_instructions.txt befindet sich eine Anleitung, die beschreibt, wie man eigene Keymaps erstellen kann, und im gleichen Verzeichnis stehen einige vordefinierte Keymaps bereit, die im Konfigurationsmen� von SpecialJump ausgew�hlt werden k�nnen.  
      Ich empfehle, die ben�tigten Funktionen in die /usr/lib/enigma2/python/Plugins/Extensions/SpecialJump/keymap_user.xml einzutragen, dann bleiben die �nderungen nach einem Update von SpecialJump erhalten.  
      Tipp: Unerw�nschte Doppel-Aktionen k�nnen entstehen, wenn z.B. die gew�nschte neue Tastenfunktion beim Dr�cken (flags="m") und die bisherige Tastenfunktion beim Loslassen (flags="b") ausgel�st wird.  
      In diesem Fall kann die bisherige Tastenfunktion durch den folgenden Eintrag "ausgeschaltet" werden:  
      `<key id="KEY_XXXX"   mapto="specialjump_doNothing"   flags="b" />`

3. Und warum wird in dieses Anleitung nicht die default-Tastenbelegung beschrieben?  
      SpecialJump ist in dieser Hinsicht kein "ready to use"-Plugin. Ich m�chte die User motivieren, selbst in die lokale keymap.xml zu gucken und sie an die eigenen Bed�rfnisse anzupassen. Meine private Version der keymap ist im gleichen Verzeichnis abgelegt, die enth�lt aber mehr, als die meisen User brauchen, und sie erfordert ein paar �nderungen der globalen keymap, das ist darin beschrieben.

4. Wozu dient das "Zap speed limit"?  
      Die Begrenzung der Zap-Geschwindigkeit macht nur Sinn, wenn die keymap.xml so eingestellt ist, dass ein langer Tastendruck auf P+ bzw. P- zum fortlaufenden Kanalwechsel f�hrt:  
      `<key id="KEY_CHANNELDOWN" mapto="specialjump_channelDown" flags="mr" />`  
      `<key id="KEY_CHANNELUP"   mapto="specialjump_channelUp"   flags="mr" />`  
      `<key id="KEY_CHANNELDOWN" mapto="specialjump_doNothing"   flags="bl" />`  
      `<key id="KEY_CHANNELUP"   mapto="specialjump_doNothing"   flags="bl" />`  

      Die Begrenzung verhindert, dass dabei Kan�le �bersprungen werden. Allerdings geht durch diese keymap-Variante die Doppelbelegung der Tasten (PIP zap) verloren.
      
5. Warum die Doppelbelegung von P+/P-?  
      Bei manchen Universal-Fernbedienungen (z.B. Sony RM-VLZ620T) sind P+ und P- wesentlich besser zug�nglich als PLAY und PAUSE.  
      Mindestens im MoviePlayer ist es daher sehr komfortabel, den Film mit P- pausieren und mit P+ fortsetzen zu k�nnen.
      Die Funktion, auch das live-TV mit P- pausieren zu k�nnen, wenn der Timeshift-Buffer eine gewisse Gr��e erreicht hat, ist sicher nicht jedermanns Sache und l�sst sich daher deaktivieren.

6. Wird die Sprungzeit (z.B. "jump +0:15") immer korrekt angezeigt?  
      Angezeigt wird die Summe der Sprungzeiten seit dem letzten Timeout, also seit die Infobar sichtbar ist.
      Wird innerhalb einer Aufnahme oder innerhalb des Timeshift-Buffers gesprungen, ist diese Zeitangabe korrekt und gibt z.B. am Ende an, wie lang die Werbepause war, die man �bersprungen hat.  
      An den Dateigrenzen (SOF, EOF) k�nnen Spr�nge aber evtl. nicht voll ausgef�hrt werden. In diesem Fall wird die gewollte, nicht die tats�chliche Sprungdistanz weiter aufsummiert, ebenso bei nicht ausgef�hrten Spr�ngen nach vorn beim live-TV.

7. Wie kann ich die SpecialJump-Infobar skinnen?  
      Die Skins aller Screens sind in plugin.py eingebettet, k�nnen aber durch Eintr�ge in anderen skins, z.B. der skin\_user.xml, �berschrieben werden.  
      Ein Template daf�r, das auch die richtigen Screen-Namen enth�lt, liegt unter /usr/lib/enigma2/python/Plugins/Extensions/SpecialJump/skin.xml - Diese Datei wird aber an dieser Stelle nicht verwendet und dient nur als Vorlage f�r Zus�tze zur eigenen skin\_user.xml.

8. Wie lassen sich die Farbtasten mit den neuen Funktionen belegen?  
      Hierzu ist es erforderlich, die Normalbelegung der Farbtasten zu deaktivieren:  
      menu - system - settings - button setup - use image color buttons - no (bzw. in den settings: config.plisettings.ColouredButtons=false)  
      Au�erdem kann es noch weitere Funktionen im Image geben, die in der keymap deaktiviert werden m�ssen (vgl. Q2). Daraus ergibt sich z.B. ein keymap-Eintrag wie folgt:  
      `<map context="SpecialJumpActions">`  
      ` <key id="KEY_RED" mapto="specialjump_jump1" flags="m" />`  
      `  <key id="KEY_RED" mapto="specialjump_doNothing" flags="brl" />`  
      `</map>`  
      `<map context="SpecialJumpMoviePlayerActions">`  
      `  <key id="KEY_RED" mapto="specialjump_jump1" flags="m" />`  
      `  <key id="KEY_RED" mapto="specialjump_doNothing" flags="brl" />`  
      `</map>`

9. Wer hat Dir geholfen, dieses Plugin zu schreiben?  
      So direkt eigentlich niemand. Die meisten Fragen, die ich in diversen Foren gestellt habe, waren leider so speziell, dass ich sie mir nur selbst durch Suchen und Probieren beantworten konnte. "Print" und Google waren meine besten Freunde.
      Die wertvollste Hilfe kam aus dem Quellcode anderer Plugins, ich danke insbesondere Dr.Best (Quickbutton), Emanuel (MultiQuickButton) und vlamo (Record Infobar), bei denen ich Anleihen genommen habe.




Revision History:
-----------------

Please see the commit messages at https://github.com/openatv/SpecialJump/commits/master
