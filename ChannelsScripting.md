# Channel scripting (communicationscripts) #

When the standard communication of bots does not fit your needs, use communicationscripts.<br>

Instruction to make a channel script:<br>
<ol><li>there must be channel in bots-monitor (or make a new one)<br>
</li><li>make a communicationscript with the <b>same name</b> as the channelID<br>
</li><li>place the communicationscript in <i>bots/usersys/communicationscripts/channelid.py</i></li></ol>

<br>
Use cases:<br>
<ul><li>communication method not provided by bots<br>
</li><li>existing communication needs customization<br>
</li><li>call external program to write edi message to your ERP system.<br>
</li><li>additional requirements: Eg. use partner name or order number in output file name.<br>
</li><li>control archive file naming</li></ul>

<br>
There are 3 types of communication scripts:<br>
<ol><li>small user exits: at certain places in normal communication a user script is called. Examples of <a href='CommunicationScriptsExample.md'>small user exits</a>
</li><li>subclass: take-over of (parts of) communication script: user script subclasses existing communication type.<br>
</li><li>communication type 'communicationscript'. Bots tries to do the bots-handling of files, you provide the communication details. Examples of <a href='CommunicationScriptsType.md'>communication type 'communicationscript'</a>