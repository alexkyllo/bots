## Document View ##

Bots focuses mostly on edi files.<br>
Another useful way of looking at edi is to view at 'business documents': orders, asn's, invoices etc.<br>
<br>
Bots support this, but to have this work satisfactory some configuration needs to be done.<br>
Essential is the use of document numbers (eg order number, shipment number, invoice number); in bots this is called 'botskey'.<br>
<br>
<br>
<h3>Usage</h3>
Once 'botskey' is set correct for your documents,  it can be used for:<br>
<ul><li>Viewing and searching business documents:<br>
<ul><li>View last run: <i>bots-monitor->Last run->Document</i>
</li><li>View all runs: <i>bots-monitor->All run->Document</i>
</li><li>Select/search for documents: <i>bots-monitor->Select->Document</i>
</li></ul></li><li>Set output <a href='http://code.google.com/p/bots/wiki/Filenames'>file name in a channel</a> or in a <a href='http://code.google.com/p/bots/wiki/ChannelsScripting'>communicationscript</a></li></ul>

<br>
<h3>Configure botskey</h3>
This can be done in two ways:<br>
<ol><li>Using QUERIES in the <a href='http://code.google.com/p/bots/wiki/GrammarsIntroduction'>grammar</a> of the incoming edi file.<br>
<pre><code># Example: botskey in a simple csv grammar<br>
structure = [<br>
    {ID:'LIN',MIN:1,MAX:99999,<br>
        QUERIES:{<br>
            'frompartner': ({'BOTSID':'LIN','AccountCode':None}),<br>
            'topartner':   ({'BOTSID':'LIN','CustomerCode':None}),<br>
            'botskey':     ({'BOTSID':'LIN','PurchaseOrderNo':None}),<br>
        },<br>
    }<br>
]<br>
</code></pre>
</li><li>In your <a href='http://code.google.com/p/bots/wiki/MappingIntroduction'>mapping script</a>.<br>
<pre><code>    out.ta_info['botskey'] = inn.get({'BOTSID':'LIN','PurchaseOrderCode':None})<br>
</code></pre>