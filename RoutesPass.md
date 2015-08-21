Sometimes you want to pass an edi-file though bots without translation.<br>
In this case bots is only used to manage/register the sending or receiving of edi-files.<br>

<br>
<h3>for bots>=3.0</h3>
In route (<i>bots-monitor->Configuration->Routes</i>) use value 'Pass-through' for 'translate'.<br>
<br>
<br>
<h3>for bots<=2.2</h3>
Use a routescript:<br>
<ol><li>configure route the normal way (<i>bots-monitor->Configuration->Routes</i>)<br>
</li><li>make a routescript with the same name as the routeID<br>
</li><li>place the routescript in <i>bots/usersys/routescripts/routeid.py</i></li></ol>

Contents of routescript:<br>
<pre><code>from bots.botsconfig import *<br>
import bots.transform as transform<br>
<br>
def postincommunication(routedict,*args,**kwargs): <br>
    # postincommunication() is run after fromchannel communication.<br>
    # the status of incoming files is changed to outgoing. <br>
    # bots skips parsing and translation.<br>
    transform.addinfo(change={'status':MERGED},where={'status':FILEIN,'idroute':routedict['idroute']})<br>
</code></pre>