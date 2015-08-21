### sort(mpath) ###
Sorts the incoming message according to certain value.<br>
Sorts alphabetically.<br>
<pre><code>inn.sort({'BOTSID':'UNH'},{'BOTSID':'LIN','C212.7140':None}) <br>
#sort article lines by EAN article number (GTIN).<br>
</code></pre>

<h3>transform.useoneof(first get, second get, etc)</h3>
Use for default values or when data can be in different places in a message.<br>
<pre><code>value = transform.useoneof(inn.get({'BOTSID':'IMD','C960.4294':None}),inn.get({'BOTSID':'IMD','7078':None})) <br>
#returns the result of the first get() that is succesful.<br>
#remarked was that this is simular to:<br>
value = inn.get({'BOTSID':'IMD','C960.4294':None}) or inn.get({'BOTSID':'IMD','7078':None})<br>
#Usage for default values (if field not there, use default): <br>
value = inn.get({'BOTSID':'IMD','C960.4294':None}) or 'my value'<br>
</code></pre>

<h3>transform.datemask(value,frommask,tomask)</h3>
Does format conversions based upon pattern matching.<br>
Especially useful for date/time conversion.<br>
Note: only simple pattern matching, without 'intelligence' about date/time.<br>
<pre><code>transform.datemask('09/21/2011','MM/DD/CCYY','YY-MM-DD') <br>
#returns '11-09-21'<br>
</code></pre>
Funny trick with datamask:<br>
<pre><code>print transform.datemask('201512312359','YYYYmmDD0000','YYYYmmDD0000')<br>
print transform.datemask('201512310000','YYYYmmDD0000','YYYYmmDD0000')<br>
print transform.datemask('20151231','YYYYmmDD0000','YYYYmmDD0000')<br>
#returns date always in CCYYmmDDHHMM, if no tiem in original tiem is '0000'<br>
<br>
</code></pre>

<h3>transform.concat(<code>*</code>args)</h3>
do a save concatenate of string.<br>
If argument is None, nothing is concatenated.<br>
<pre><code>transform.concat('my',None','string') <br>
#returns 'mystring'<br>
</code></pre>

<h3>transform.sendbotsemail(partner,subject,reporttext)</h3>
Send a simple email message to any bots partner (in partner-table) from a mapping script.<br>
Mail is sent to all To: and cc: addresses for the partner (but send_mail does not support cc).<br>
Email parameters are in config/settings.py (EMAIL_HOST, etc).<br>
<pre><code>transform.sendbotsemail('buyerID1','error in messsge','There is an error in message blahblah') <br>
</code></pre>

<h3>transform.unique(domain)</h3>
Returns counter/unique number.<br>
For each 'domain' separate counters are used.<br>
Counter start at '1' (at first time you use counter).<br>
The counter can be changed in <i>bots-monitor->SysTasks->view/edit counters</i>
<pre><code>transform.unique('my article line counter') <br>
#returns a number unique for the domain 'my article line counter'<br>
</code></pre>

<h3>transform.unique_runcounter(domain))</h3>
Returns counter/unique number during the bots-run.<br>
For each 'domain' separate counters are used.<br>
Counter start at '1' (at first time you use counter).<br>
In a next run the counter will start again at '1'.<br>
Useful for eg a message-counter per interchange.<br>
<br>
<h3>transform.inn2out(inn,out)</h3>
Use the incoming message as the outgoing message.<br>
Is useful to translate the message one-on-one to another editype.<br>
Examples:<br>
<ul><li>edifact to flat file. This is what a lot of translators do.<br>
</li><li>x12 to xml. x12 data is translated to xml syntax, semantics are of course still x12<br>
</li><li>Another use: read a edi message, adapt, and write (to same editype/messagetype including changes).