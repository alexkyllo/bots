## Partner look-up (bots>=3.0) ##
Often there is a need to retrieve data from a partner, using a IDpartner.
Think of:
  * check if partner is active
  * get name/address of partner
  * get senderID for partner


### Recipe ###
Get the value in field 'attr1' for the IDpartner.<br>
See partners in <i>bots-monitor->Configuration->Partners</i> for possible fields.<br>
<pre><code>transform.partnerlookup('buyer1','attr1',safe=True) <br>
</code></pre>

Check if a partner exists, and is active. If not, raise an exception.<br>
<pre><code>transform.partnerlookup('buyer1','active') <br>
</code></pre>


<table><thead><th> <b>Value for safe</b> </th><th> <b>If a record matching your lookup does not exist, or the requested field is empty</b></th></thead><tbody>
<tr><td>safe=False<br>(default)</td><td>An exception is raised<br>You can check for this in your script if required and take action</td></tr>
<tr><td>safe=True              </td><td>No exception is raised, just returns the lookup value<br>eg. to lookup a user defined field for partner translation on some partners</td></tr>
<tr><td>safe=None<br>(Bots>=3.2)</td><td>No exception is raised, returns None<br>eg. to get address lines where not all partners have addresses, but this is not an error</td></tr></tbody></table>

<h3>Lookup using a field other than IDpartner</h3>
This is similar to reverse code conversion, but can look up any partner field and return any other partner field. Beware of performance issues if you have a large number of partners. Also there may be multiple matches if the lookup is not unique, only one is returned.<br><br>
Get the value in field 'name' by looking up value in 'attr2'.<br>
<pre><code>transform.partnerlookup('my attribute','name','attr2',safe=True) <br>
</code></pre>

<h3>Notes</h3>
<ul><li>In bots<3.0 this was possible using <a href='MappingCcode.md'>code conversion</a>. But this could lead to situations where partners where both in <i>bots-monitor->Configuration->Partners & groups</i> and in code conversions.<br>
</li><li>partners have more fields in bots>=3.0 like name, address, 'free' fields.