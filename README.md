Chataigne Module for Live Cue List Show Creator v2.0.0 - T.Hyde c2026 www.casafrog.com
========================================================================================================
This file is a Chataigne Custom Module to scan a folder for audio files and creates 
Sequences, A State Machine and a Conductor for Use with a big GO button, intended 
for sequential cueing in live theatrical performances.

Although not required, if you like the idea of the legacy Dashboard, you can use the "baseline.noisette" project
file to start your own project and it will include a functional transport panel as a template. As the development
of the web-dashboard module is evolving, this legacy Dashboard will likely be depreciated, hence the reason for it
not being created programmatically.

This is a two-part workflow; the "Audio Master Controller" option will act as the audio master and
cueing source that will (optionally) trigger a secondary (or other multiple) Chataigne instances such that might
be distributed between departments. In a typical situation, lighting and projection may be running a secondary
Chataigne instance that is configured as a "Lighting Receiver".

It is not at all necessary to split up Chataigne in most cases, however it can make complex programming and 
operation much easier when that is done. 

In a live musical theatre setting, audio often leads the cueing, thus it follows that audio should be the master source.
This is not dissimilar to older methods where [tape] provided audio and timecode source for other devices.
The benefits here are that it is not limited to a single central controller; cues (states via Conductor) can be added
unique to the department after the initial generation to customize the show system; this script is meant to do the 
"heavy lifting" of getting the majority of the cues and framework built.

For example, sound effects that don't have triggers for other departments can be added to the audio master and not effect
the receivers in any way. Alternatively, in the event audio is not able to provide a trigger, a cue state can be added to 
a receiver's conductor and the local go button still used.

While this workflow will likely be acceptable to many circumstances, it isn't meant to be an all-encompassing solution to 
every situation. For example, your situation may routinely need projection as a third receiver - feel free to edit and customize
the script to handle your needs.

This script does NOT autocreate all of your lighting (receiver) cues for you (sorry!). In the Audio Master creation, it does create
a trigger layer that will trigger a secondary receiver via OSC (a single "go" trigger), so in many circumstances the Audio Master 
creation is a single-click situation.

For the (lighting) Receiver, however, you will need to add/copy and modify the OSC triggers specific to your lighting console. 
However for your convenience a sample trigger is placed at the start time of every cue state (which you can then copy paste 
at your leisure).

REQUIREMENTS PRIOR TO OPERATION: 

    1. You MUST have your show control trigger modules and audio output modules defined prior.
    
    2. Your primary Sound Card will be chosen for output automatically, however that is easily changable at the per-state level 
        in the audio track properties.
        
    3. Before running the script, select the BUILD TYPE in the module's properties inspector. The Lighting Receiver creates additional 
        parameters.
        
    4. Check and prefill both the (inbound/outbound) Trigger Module Names and Commands to match your scenario. If the modules cannot
        be found, you will receive an error. 
        
    5. For Audio Master Outbound Command and Lighting Receiver Inbound Command you can leave those defaults (/sequences/%/play) as defined
        since those must match between the Controller and the Receiver.
        
    6. Please place all your audio source files in a folder at the same level as your Chaitiagne project (.noisette) file. This will allow you
        to take advantage of relative file paths instead of having to deal with absolute file path corrections, especially if you want to 
        move/copy files between different PCs or operating systems. For example, all the sound files in a folder called "audio_assets" will suffice.
        
    7. Filename punctuation is IMPORTANT! For the "automatic" convenience, please avoid all the dangerous characters in a file name. Chataigne's internal
        object naming will typically get rid of spaces, auto-lowercase the first character, then sentence case the remaining word objects. You can safely
        use spaces and underscores, but other punctuation is best avoided. Additionally, some characters in OSC commands are prohibited, so stick with
        spaces and underscores.
        
    8. The script will numeric-alpha ascending sort the file names found in the folder and begin adding in that sequence. Thus, if you want an easy 
        way to have your cues in sequence, edit the filenames prior to include a sequence number at the beginning )1...02...03 etc) . This does NOT 
        have to be any particular cue number, just an arbitrary value. If your organizational skills permit and it is also the cue number, 
        that is perfectly fine.


A simple use case: audio has 15 full-length musical cues. They are named in a folder numerically. Running the Audio Master 
function will build the states with an audio layer, a trigger layer, a single OSC "go" command on that layer, the state machine, a conductor
and a dashboard with a GO/TRANSPORT section. For the most part, this is likely all the audio department needs.

If you are using a PC audio output (2ch stereo) then the primary sound card will get autoselected. IF you are using a more advanced USB- 
connected audio console with DAW-connect capability (such as an A&H Qu32 with multiple USB Audio devices), be sure to check the audio output
for each of your effected cue states. 

Secondary to that, the (lighting) Receiver function, being run on the (lighting) show controller computer (with same audio folder) 
will build a slightly different version of the above; the same states with audio and trigger layers, but will be configured with 
conditions to trigger from an external OSC command (from the Audio Master) and the trigger layer will have a single trigger
configured to send out to (your lighting console via an other OSC module). If you only have one lighting cue per song, then
this is pretty simple - edit the outbound OSC trigger command for your cue particulars and be done. However, we all know that
"more cues be gooder!" so you can copy the first trigger, and "beat mark" subsequent cue triggers by pasting that copy onto the 
trigger layer. What do you beat mark to? The audio layer on that cue state of course!

It should now be obvious why there is an audio layer in the states when there is (likely) no intent for the (lighting) receiver 
show controller to actually playback audio - the lighting designer can edit triggers to their liking simply by scrubbing the
audio track locally, which saves from having to run the audio from the top of each musical number every time. (Or have the audio 
mains system actually up and going.)

Need a manual cue sequence [state] but there is no audio trigger? Fine, simply add (or copy) a reference cue [state] and the 
same element for the Conductor, and edit away. Again, this script is a helper to mass-add and configure a whole performance's 
worth of cues in seconds instead of "probably 30-40 minutes of not-exciting labor". You then get to customize to your needs.

=========================================================================================
