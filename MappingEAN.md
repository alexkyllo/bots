## EAN/UCC checkdigits ##

Synonyms: GTIN, ILN, GLN, UPC, EAN, UAC, JAN<br>
Can be used for UPC-A, UPC-E, EAN8, EAN13, ITF-14, SSCC/EAN-128 etc.<br>

These numbers end with a check-digit.<br>
<br>
<br>
<h3>transform.checkean(EAN_number)</h3>
Returns True is if check-digit is OK, False if not.<br>
When not a string with digits, raises botslib.EanError<br>
<pre><code> transform.checkean('8712345678906') <br>
 #returns 'True' for this EAN number.<br>
</code></pre>

<br>
<h3>transform.addeancheckdigit(EAN_number)</h3>
<blockquote>Returns EAN number including check digit (adds checkdigit).<br>
<pre><code> transform.addeancheckdigit('871234567890') <br>
 #returns '8712345678906' for EAN number '871234567890'.<br>
</code></pre></blockquote>

<br>
<h3>transform.calceancheckdigit(EAN_number)</h3>
Returns the checkdigit-string for a number without check-digit.<br>
<pre><code> transform.calceancheckdigit('871234567890') <br>
 #returns '6' for EAN number '871234567890'.<br>
</code></pre>