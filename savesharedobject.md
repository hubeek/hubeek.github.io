# saveSharedObject

_Status: Published_
_Created: 2014-09-04 07:32:21_
_Tags: Actionscript_

<code>var saveDataObject:SharedObject;</code>
<code>saveDataObject = SharedObject.getLocal("test");</code>
of
in 1en
<code>saveDataObject:SharedObject = SharedObject.getLocal("test");</code>

<code>saveDataObject.data.savedScore = currentScore;</code>

When you want the SharedObject to actually, immediately write its save data to its file on the playerâ€™s local hard drive you flush it:

<code>saveDataObject.flush();</code>

This is a very processor intensive action to call, so use it sparingly (never include it an a loop function).

To load â€œcurrentScoreâ€ from the â€œsavedScoreâ€, we would write:

<code>currentScore = saveDataObject.data.savedScore;</code>

