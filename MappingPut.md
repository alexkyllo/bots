## Put data in outgoing message ##

### put(mpath) ###
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