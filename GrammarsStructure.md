## Structure ##

> Definition: _the structure section in a grammar defines the sequence of records in a message._<br>
A structure is required in a grammar except for template grammars.<br>
Example of a simple structure:<br>
<pre><code>structure = [<br>
{ID:'ENV',MIN:1,MAX:999, LEVEL:[        #envelope record<br>
    {ID:'HEA',MIN:1,MAX:9999,LEVEL:[    #header record<br>
        {ID:'LIN',MIN:0,MAX:9999},      #line record<br>
        ]},<br>
    ]}<br>
]<br>
</code></pre></li></ul>

The example above should be read as:
> ENV-record is required; max 999 repeats.<br>
<blockquote>'Nested' under the ENV-record: HEA-record; per ENV max 9999 HEA-records; min is 1, so required.<br>
Per HEA-record max 9999 LIN-records; the LIN-record is not required (MIN=0).<br>
<br></blockquote>

<br>
Example of a more elaborate structure:<br>
<pre><code>structure = [<br>
{ID:'ENV',MIN:1,MAX:1, LEVEL:[        #envelope record: max one per file<br>
    {ID:'HEA',MIN:1,MAX:9999,LEVEL:[  #header record of messageat least one message per ENV, max 9999 messages<br>
        {ID:'PAR',MIN:2,MAX:10},      #party record<br>
        {ID:'ALC',MIN:0,MAX:9},       #allowances/charges per message<br>
        {ID:'LIN',MIN:0,MAX:9999},    #line record<br>
        ]},<br>
    {ID:'TRL',MIN:1,MAX:1},           #each ENV record has a trailer record<br>
    ]}<br>
]<br>
</code></pre>

<br>
<h3>A structure consists of</h3>
<ol><li>A structure is a nested list of records.<br>
</li><li>Each record is a python dict.<br>
</li><li>per record:<br>
<ul><li>ID: tag of record.<br>
</li><li>MIN: minimum number of occurrences.<br>
</li><li>MAX: maximum number of occurrences.<br>
</li><li>LEVEL (optional): indicate nested record. The nested records are in a list of records.<br>
</li><li><a href='GrammarsStructure#QUERIES.md'>QUERIES</a> (optional)<br>
</li><li>SUBTRANSLATION (optional). Very advanced. Purpose: identify separate messages within within a standard envelope.</li></ul></li></ol>

<br>
<h3>QUERIES</h3>
QUERIES in a structure are used to extract values from edi files before the mapping script starts.<br>
Example of an structure with QUERIES:<br>
<pre><code>structure = [<br>
{ID:'ENV',MIN:1,MAX:999,                #envelope record<br>
    QUERIES:{<br>
        'frompartner':  {'BOTSID':'ENV','sender':None},   #extract sender from ENV record.<br>
        'topartner':    {'BOTSID':'ENV','receiver':None}, #extract receiver from ENV record.<br>
        'testindicator':({'BOTSID':'ENV'},{'BOTSID':'MESSAGE','test':None}), #extract testindicator from 'deeper' level; note that this is in tuple (with brackets).<br>
        },<br>
    LEVEL:[         <br>
    {ID:'HEA',MIN:1,MAX:9999,LEVEL:[    #header record<br>
        {ID:'LIN',MIN:0,MAX:9999},      #line record<br>
        ]},<br>
    ]}<br>
]<br>
</code></pre>

Use cases of the information extracted by QUERIES:<br>
Think of frompartner, topartner, reference, testindicator etc.<br>
<ol><li>to choose the right translation (QUERIES can extract frompartner, topartner, alt)<br>
</li><li>Update the database.<br>
</li><li>In a mapping script this information is inn.ta_info'.<br>
</li><li>data in the envelope can be accessed in the mapping.<br>
</li><li>One of the most import uses is the extraction of <b>botskey</b>.<br>
</li><li>Typical information extracted by QUERIES:<br>
<ul><li>frompartner<br>
</li><li>topartner<br>
</li><li>reference<br>
</li><li>testindicator<br>
</li><li>botskey<br>
</li><li>alt