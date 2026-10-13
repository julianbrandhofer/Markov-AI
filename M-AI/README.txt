/**************************************************************************************************************\
* README: Markov-AI			Version: 1.0
*
* Date: 01.02.2024 			Author: Julian Brandhofer
\**************************************************************************************************************/

This MAX device enables real-time improvisation with an AI (Markov model) in Ableton.
To use the device, it must be added as the first device on a MIDI track.
After that, a MIDI instrument (Sampler, synth, etc.) must be added to the device chain.
An example project with this setup is included.
Once the recommended settings (see below) have been applied, the device is ready to use.
To do so, start playback or recording in Ableton.
After 8 (Size) notes have been played, the program starts to generate melodic phrases on its own,
based on the pitches of the input.
Settings can be changed at runtime.
Tempo changes are also taken into account.

---------------------------------------------------------------------------------------------------------------
Markov Model
---------------------------------------------------------------------------------------------------------------

Enable:	Enables/disables the output of Markov-generated notes				  Recommended: (Enable)

Learn: 	Enables/disables periodic learning of the Markov model				Recommended: (Enable)

Size: 	Sets after how many input notes a new model is computed		  	Recommended: (8)

Dump: 	Clears all notes from the buffer				                   		Recommended: /

Reset: 	Resets the Markov model								                        Recommended: /

---------------------------------------------------------------------------------------------------------------
Rhythm Generator
---------------------------------------------------------------------------------------------------------------

1/1: 	Generates whole notes							  	                        Recommended: (Disabled)

1/2: 	Generates half notes							                          	Recommended: (Disabled)

1/4: 	Generates quarter notes						                        		Recommended: (Enable)

1/8: 	Generates eighth notes								                        Recommended: (Enable)

Density:Sets the percentage of notes that are sounding notes rather than rests	Recommended: (75)

---------------------------------------------------------------------------------------------------------------
Miscellaneous
---------------------------------------------------------------------------------------------------------------

Vel.: 		Sets the velocity of the output notes			              	Recommended: (100)

8va. Shift: 	Transposes the output notes up or down by n octaves		Recommended: (0)

Pass-Through: 	Enables/disables the output of the incoming MIDI signal		Recommended: (Enable)
