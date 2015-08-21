Several situations:
  * send different versions of messages
  * receive different versions
Note: in real world versions are often so similar that the same mapping script can be used (or a simple if-then can cater for the differences).


<br>
<h3>Send multiple versions using partners</h3>
use the 'topartner' to determine the right version to send.<br>
<ul><li>one grammar for in-house message:<br>
<ul><li>myinhouseorder.py<br>
</li><li>this grammar uses QUERIES to extract 'topartner'.<br>
</li></ul></li><li>grammars for both versions:<br>
<ul><li>ORDERSD93AUN<br>
</li><li>ORDERSD96AUN<br>
</li></ul></li><li>2 translation rules:<br>
<ul><li>fixed-myinhouseorder to edifact-ORDERSD93AUN using mapping script ordersfixed2edifact93.py for topartner=XXX<br>
</li><li>fixed-myinhouseorder to edifact-ORDERSD96AUN using mapping script ordersfixed2edifact93.py for topartern=YYY</li></ul></li></ul>


<br>
<h3>Send multiple versions using alt</h3>
Information about the version is in in-house-message: a field that contains either '93' or '96'.<br>
<ul><li>one grammar for in-house message:<br>
<ul><li>myinhouseorder.py<br>
</li></ul></li><li>grammars for both versions:<br>
<ul><li>ORDERSD93AUN<br>
</li><li>ORDERSD96AUN<br>
</li></ul></li><li>2 translation rules<br>
<ul><li>fixed-myinhouseorder to edifact-ORDERSD93AUN using mapping script orders_fixed2edifact93.py for alt=93<br>
</li><li>fixed-myinhouseorder to edifact-ORDERSD96AUN using mapping script orders_fixed2edifact93.py for alt=96</li></ul></li></ul>

<br>
<h3>Receive multiple versions</h3>
<ul><li>grammars for both versions:<br>
<ul><li>ORDERSD93AUN<br>
</li><li>ORDERSD96AUN<br>
</li></ul></li><li>one grammar for in-house message:<br>
<ul><li>myinhouseorder.py<br>
</li><li>this grammar uses QUERIES to extract 'alt'-value.<br>
</li></ul></li><li>2 translation rules<br>
<ul><li>edifact-ORDERSD93AUN to fixed-myinhouseorder using mapping script orders_edifact93_2_fixed.py<br>
</li><li>edifact-ORDERSD6AUN to fixed-myinhouseorder using mapping script orders_edifact96_2_fixed.py