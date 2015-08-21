## Examples for small user exit ##

<br>
<h4>Filter email attachments</h4>
Some edi-partners send signatures etc in their email. Script does a simple check if incoming attachment starts with 'UNB'. (Note: Bots treats any text in the email body as another "attachment")<br>
<pre><code>def accept_incoming_attachment(channeldict,ta,charset,content,contenttype,*args,**kwargs):<br>
    if 'UNB' in content[0:50]:<br>
        return True   #attachments is OK<br>
    else:<br>
        return False  #skip this attachment<br>
</code></pre>

<br>
<h4>Set email subject</h4>
Some edi-partners send signatures etc in their email.<br>
By default bots uses a number for emails.<br>
Sometimes you want a more meaningfull subject.<br>
<pre><code>def subject(channeldict,ta,subjectstring,content,*args,**kwargs):<br>
    ta.synall()        #needed to get access to attributes of object ta (eg ta.frompartner)<br>
    return 'EDI messages from ' + ta.frompartner + '_' + subjectstring<br>
</code></pre>

<br>
<h4>Name archive file same as input file</h4>
Not needed for bots 3.<b>; do this via setting in bots.ini<br>
<pre><code>import os<br>
import bots.botslib as botslib<br>
<br>
def archivename(channeldict,idta,filename,*args,**kwargs):<br>
     taparent=botslib.OldTransaction(idta=idta)<br>
     ta_list = botslib.trace_origin(ta=taparent,where={'status':EXTERNIN})<br>
     archivename = os.path.basename(ta_list[0].filename)<br>
     return archivename <br>
</code></pre></b>

<br>
<h4>Set the archive path</h4>
Path root is set in channel.<br>
Add sub-dir per date, then sub-dir per channel under it.<br>
<pre><code>import time<br>
import bots.botslib as botslib<br>
<br>
def archivepath(channeldict,*args,**kwargs):<br>
    archivepath = botslib.join(channeldict['archivepath'],time.strftime('%Y%m%d'),channeldict['idchannel'])<br>
    return archivepath<br>
</code></pre>


<br>
<h4>Partners in the output file name</h4>
Not needed for bots 3.<b>; do this via file name in GUI<br>
<pre><code>def filename(channeldict,filename,ta,*args,**kwargs):<br>
    ta.synall()        #needed to get access to attributes of object ta (eg ta.frompartner)<br>
    return ta.frompartner + '_' + ta.topartner + '_' + filename<br>
</code></pre></b>


<br>
<h4>Name the output file from botskey</h4>
botskey can be set in grammar or mapping, eg. from customer's order number.<br>
If no botskey is found, the default file naming method will be used.<br>
Syntax must contain 'merge':False.<br>
Not needed for bots 3.<b>; do this via file name in GUI.<br>
<pre><code>def filename(channeldict,filename,ta,*args,**kwargs):<br>
    ta.synall()<br>
    if ta.botskey:<br>
        return filename + ta.botskey<br>
    else:<br>
        return filename<br>
</code></pre></b>

<br>
<h4>Name the output file same as input file</h4>
Syntax must contain 'merge':False.<br>
Not needed for bots 3.