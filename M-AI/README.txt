/**************************************************************************************************************\
* README: Markov-AI			Version: 1.0
*
* Datum:01.02.2024 			Autor: Julian Brandhofer
\**************************************************************************************************************/

Dieses MAX-Gerät ermöglicht eine Echtzeit Improvisation mit einer KI (Markov-Modell) in Ableton. 
Zur Verwendung des Geräts muss dieses, als erstes Gerät, auf einen MIDI-Track hinzugefügt werden. 
Anschließend muss die Effekt-Reihe um ein MIDI-Instrument (Sampler, Synth, etc.) ergänzt werden. 
Ein Beispielprojekt mit diesem Setup ist beigelegt. 
Nachdem die empfohlenen Einstellungen (siehe unten) getroffen wurden, kann das Gerät verwendet werden.
Hierfür muss die Wiedergabe bzw. Aufnahme in Ableton gestartet werden. 
Nach einer Eingabe von 8 (Size) Noten beginnt das Programm eigenständig melodische Phrasen,
basierend auf den Pitch-Signalen der Eingabe, zu generieren.
Einstellungen können während der Laufzeit verändert werden. 
Auch Veränderungen des Tempos werden berücksichtigt.

---------------------------------------------------------------------------------------------------------------
Markov Model
---------------------------------------------------------------------------------------------------------------

Enable:	Aktiviert/Deaktiviert die Ausgabe von Markov-generierten Noten			Empfohlen: (Enable)

Learn: 	Aktiviert/Deaktiviert das periodische Lernen des Markov-Modells			Empfohlen: (Enable)

Size: 	Bestimmt alle wie viel Eingangsnoten ein neues Modell berechnet wird		Empfohlen: (8)

Dump: 	Leert alle Noten aus dem Zwischenspeicher 					Empfohlen: /

Reset: 	Setzt das Markov-Modell zurück							Empfohlen: /

---------------------------------------------------------------------------------------------------------------
Rhythm Generator
---------------------------------------------------------------------------------------------------------------

1/1: 	Es werden ganze Noten generiert 						Empfohlen: (Disabled)

1/2: 	Es werden halbe Noten generiert 						Empfohlen: (Disabled)

1/4: 	Es werden viertel Noten generiert 						Empfohlen: (Enable)

1/8: 	Es werden Achtel Noten generiert 						Empfohlen: (Enable)

Density:Bestimmt wie viel Prozent der Noten Pausen oder Töne sind			Empfohlen: (75)

---------------------------------------------------------------------------------------------------------------
Miscellaneous
---------------------------------------------------------------------------------------------------------------

Vel.: 		Bestimmt die Velocity der Ausgegebenen Noten				Empfohlen: (100)

8va. Shift: 	Transponiert die ausgegebenen Noten um n Oktaven nach oben bzw. unten	Empfohlen: (0)

Pass-Through: 	Aktiviert/Deaktiviert die Ausgebe des eingehenden MIDI-Signals		Empfohlen: (Enable)
