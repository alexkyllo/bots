## What translation when? ##

Bots figures out what translation to use via the translation rules.<br>
Best is to think of the translation rules as a 'lookup' table:<br>
<blockquote>look-up with (from-editype, from-messagetype, alt, frompartner and topartner) to find mappingscript, to-editype and to-messagetype</blockquote>

<br>
How the input values for the look-up are determined:<br>
<ol><li>editype<br>
<ul><li>configured in the route<br>
</li><li>if you configure editype=mailbag, bots will figure out if editype is x12, edifact or tradacoms.<br>
</li></ul></li><li>messagetype can be:<br>
<ul><li>configured in the route, eg for editype csv<br>
</li><li>for edifact, x12 and tradacoms: bots figures out the detailed messagetype. Example:<br>
<ul><li>in route: editype: edifact, messagetype: edifact<br>
</li><li>in incoming edi file bots finds detail messagetype  'ORDERSD96AUN'.<br>
</li></ul></li></ul></li><li>frompartner can be:<br>
<ul><li>configured in the route<br>
</li><li>determined by the grammar using <a href='GrammarsStructure#QUERIES.md'>QUERIES</a>
</li></ul></li><li>topartner can be:<br>
<ul><li>configured in the route<br>
</li><li>determined by the grammar using <a href='GrammarsStructure#QUERIES.md'>QUERIES</a>
</li></ul></li><li>alt can be:<br>
<ul><li>configured in the route<br>
</li><li>determined by the grammar using <a href='GrammarsStructure#QUERIES.md'>QUERIES</a>
</li><li>set by mapping script in a <a href='TranslationAlt.md'>chained translation</a></li></ul></li></ol>

<br>
Notes:<br>
<ul><li>For frompartner and topartner: bots finds the most specific translation.<br>
<ul><li>Eg example with 2 translation rules:<br>
<ul><li>fromeditype = edifact, frommessagetype = ORDERSD96AUNEAN008<br>
</li><li>fromeditype = edifact, frommessagetype = ORDERSD96AUNEAN008, frompartner=RETAILERX<br>
</li></ul></li><li>If bots receives an ORDERS message from RETAILERX, the 2nd translation is used.<br>
</li><li>For other partners the first translation is used.</li></ul></li></ul>

<ul><li>for alt-translations: only find the translation with that specific 'alt'.