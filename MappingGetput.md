

<br>
<h2>Get data from message</h2>

<h3>get(mpath)</h3>
Get 1 field from the incoming message; mpath specifies which field to get.<br>
Returns: string or, if field not found, None<br>
<pre><code>#get the message date from an edifact invoice:<br>
inn.get({'BOTSID':'UNH'},{'BOTSID':'DTM','C507.2005':'137','C507.2380':None}) <br>
</code></pre>
Explanation: get field C507.2380 from DTM-record if field C507.2005 is '137', DTM-record nested under UNH-record.<br>
The field to retrieve is specified as None.<br>
<br>
<h3>getnozero(mpath)</h3>
Like get(), but: return a numeric string not equal to '0', otherwise None.<br>
Eg useful in fixed records, where a numeric field is often initialized with zero's.<br>
<br>
<h3>getloop(mpath)</h3>
For looping over repeated records or record groups.<br>
Typical use: loop over article lines in an order.<br>
Returns an object usable with get(); see example.<br>
<pre><code>#loop over lines in edifact order:<br>
for lin in inn.getloop({'BOTSID':'UNH'},{'BOTSID':'LIN'}):<br>
    linenumber = lin.get({'BOTSID':'LIN','1082':None})<br>
    articlenumber = lin.get({'BOTSID':'LIN','C212.7140':None})<br>
    quantity = lin.get({'BOTSID':'LIN'},{'BOTSID':'QTY','C186.6063':'21','C186.6060':None})<br>
</code></pre>

<br>
<h2>Put data in message</h2>

<h3>put(mpath)</h3>
Places the field(s)/record(s) as specified in mpath in the outmessage.<br>
Returns: if successful, True, otherwise False.<br>
If mpath contains None-values (typically because a get() gave no result) nothing is placed in the outmessage, and put() returns False.<br>
<pre><code>#put a message date in a edifact message<br>
out.put({'BOTSID':'UNH'},{'BOTSID':'DTM','C507.2005':'137','C507.2380':'20070521'}) <br>
</code></pre>
Explanation: put date '20070521' in field C507.2380 and code '137' in field C507.2005 of DTM-record; DTM-record is nested under UNH-record.<br>
<br>
<h3>putloop(mpath)</h3>
Used to generate repeated records or record groups.<br>
Recommended: only use it as in:  <i>line = putloop(mpath)</i><br>
line is used as line.put()<br>
Typical use: generate article lines in an order.<br>
Note: do not use to loop over every record, use put() with the right selection.<br>
<pre><code>#loop over lines in edifact-order and write them to fixed in-house:<br>
for lin in inn.getloop({'BOTSID':'UNH'},{'BOTSID':'LIN'}):<br>
    lou = out.putloop({'BOTSID':'HEA'},{'BOTSID':'LIN'})<br>
    lou.put({'BOTSID':'LIN','REGEL':lin.get({'BOTSID':'LIN','1082':None})})<br>
    lou.put({'BOTSID':'LIN','ARTIKEL':lin.get({'BOTSID':'LIN','C212.7140':None})})<br>
    lou.put({'BOTSID':'LIN','BESTELDAANTAL':lin.get({'BOTSID':'LIN'},<br>
				{'BOTSID':'QTY','C186.6063':'21','C186.6060':None})})<br>
</code></pre>

<br>
<h3>Warn: do not use</h3>
<b>Never</b> use 2 inn.get's in one out.put (unless you really know what you are doing ;-)<br>
<pre><code>out.put({'BOTSID':'ADD','7747':inn.get('BOTSID':'HEA','name1':None),'7749':inn.get('BOTSID':'HEA','name2':None)})} <br>
</code></pre>
Because: if either name1 or name2 is not there (empty, None) nothing will be written in this statement.