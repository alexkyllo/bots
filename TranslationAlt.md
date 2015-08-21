## Chained Translations ##

> Definition: _chained translations translate one incoming format to multiple outgoing formats._

Eg: translate edi-order to in-house format AND send an email to inform sales representative.<br>
To use this bots uses the 'alt'.<br>
How this works:<br>
<ul><li>receive incoming file<br>
</li><li>do a translation (using mapping script)<br>
</li><li>mapping script returns alt-value<br>
</li><li>do another translation using the alt-value.<br>
Background information: <a href='.md'>TranslationRules how bots determines what to translate</a>.</li></ul>

<h3>By example</h3>

<ul><li>Set up first translation rule (to csv-format) as usual:<br>
<ul><li>translate x12-850 to csv-orders using mapping script 850_2_csv<br>
</li></ul></li><li>at end of mapping script 850_2_csv:<br>
<pre><code>  return 'do_email_translation'        #alt-value is returned<br>
</code></pre>
</li><li>Set up the second translation rule:<br>
<ul><li>translate x12-850 to csv-orders using mapping script 850_2_email <b>where alt=do_email_translation</b></li></ul></li></ul>

By returning the alt-value 'do_email_translation' mapping script 850_2_csv triggers the 2nd translation (with mapping script 850_2_email).<br>

<h3>Plugin</h3>
In plugin <i>edifact_ordersdesadvinvoic</i> on <a href='http://sourceforge.net/projects/bots/files/plugins/'>bots sourceforge site</a>:<br>
<ol><li>incoming is edifact orders.<br>
</li><li>translate fixed inhouse format.<br>
</li><li>translate to edifact APERAK/acknowledgement (if acknowledgement is asked).</li></ol>

<h3>Details</h3>
<ul><li>Of course it is possible to 'chain' more than one translation.<br>
</li><li>I have used this to do complex 'sorts' on incoming documents, eg:<br>
<ul><li>write/sort to multiple outgoing messages sorting for destination of goods<br>
</li></ul></li><li>Note: in this type of set-up multiple formats are outgoing, you'll want to use a <a href='RoutesComposite.md'>composite route</a>.</li></ul>

<br>
<h2>Special Chained Translations</h2>
You can also return an alt value that is a python dict. The dict must contain 'type' and 'alt' strings; there are several special types available for different processing requirements.<br>
<br>
<h3>out_as_inn</h3>
Do chained translation: use the out-object as inn-object, new out-object.<br>
Use cases:<br>
<ol><li>Detected error in incoming file; use out-object to generate warning email.<br>
</li><li>Map inputs to standard format, also map standard format to human readable version (eg. html template)<br>
Both out-objects are output by Bots and can be sent to same or different channels using channel filtering.<br>
<pre><code>    # if the first output is not needed to send somewhere, discard it<br>
    # omit this step and you will get both outputs<br>
    from bots.botsconfig import *<br>
    out.ta_info['statust'] = DONE<br>
<br>
    # use output of first mapping as input of second mapping<br>
    return {'type':'out_as_inn','alt':'do_email_translation'}<br>
</code></pre></li></ol>

<h3>no_check_on_infinite_loop</h3>
Do chained translation: allow many loops with same alt-value. <br>
Normally, Bots will detect and prevent this, by stopping after 10 iterations of the loop. You are disabling this safety feature, so your mapping script will have to handle this correctly to ensure the looping is not infinite.<br>
<pre><code>    # we MUST have a way to exit the loop!<br>
    if (some condition):<br>
        return<br>
<br>
    # loop through this mapping multiple times...<br>
    return {'type':'no_check_on_infinite_loop','alt':'repeat'}<br>
</code></pre>