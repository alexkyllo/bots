## Persist ##
Persist allows to store data for use in other messages/transactions.

Use cases:
  * store data from an incoming order, and use the data later for DESADV and/or INVOIC. Often the buyer want you to return data in the orders that are hard to store in your internal system.
  * is used in plugin alto\_seperate\_headers\_details: input: 2 csv files, one with headers, one with details lines. This is processed into one document (so the headers and details are merged) using persist.

Details:
  * persist data is store in the bots database.
  * You can store and retrieve 'any' python data (python pickle is used).
  * bots < 3.0: storage size (per item) is limited to 1024 positions; bots >= 3.0: unlimited.
  * Parameter 'maxdayspersist' in [bots.ini](StartConfigurationFiles.md) controls how long the values are kept in bots. This is done using a timestamp for the persisted data. However, the timestamp is not updated if you update the information in the persist database. This can be done via a database trigger. In bots 3.2.0 and later the SQLite database includes this trigger (might be somewhat SQLite specific):
```
CREATE TRIGGER persist_update AFTER UPDATE OF content ON persist
BEGIN
     UPDATE persist SET ts = datetime('now','localtime')
     WHERE domein = new.domein and botskey = new.botskey ;
END
```

<br>
<h3>Example</h3>
You receive orders from buyer 'XXX'. In the order they have a 'reference number' that has to be returned in ASN's and invoices.<br>
<pre><code>#in the order:<br>
buyerID = inn.ta_info['frompartner']<br>
po_number = inn.get({'BOTSID':'ST'},{'BOTSID':'BEG','BEG03':None})<br>
ref_number = inn.get({'BOTSID':'ST'}{'BOTSID':'REF','REF01':'IP','REF02':None})<br>
transform.persist_add(buyerID, po_number, ref_number)<br>
#now this referenced number is in persist; domain is the buyerID, key is the po_number (that will be return eg in invoice)<br>
<br>
#in the invoice find the domain and key:<br>
buyerID = inn.ta_info['frompartner']     #via QUERIES in invoice in-house grammar<br>
po_number = inn.get({'BOTSID':'HEADER','PO_NUMBER':None})<br>
#fetch reference number from persist:<br>
ref_number = transform.persist_lookup(buyerID, po_number)<br>
<br>
</code></pre>

<br>
<h3>functions</h3>

<b>transform.persist_add(domain, key, value)</b><br>
Add value to persist.<br>
If not possible, eg. because domain-key exists already, botslib.PersistError is raised.<br>
<br>
<br>
<b>transform.persist_update(domain, key, value)</b><br>
Update the value.<br>
If domain-key does not exist: does not add it, gives no error.<br>
<br>
<br>
<b>transform.persist_add_update(domain, key, value)</b><br>
add, but if domain-key already exist: update.<br>
<br>
<br>
<b>transform.persist_lookup(domain, key)</b><br>
returns value.<br>
if domain-key does not exist: returns None<br>
<br>
<br>
<b>transform.persist_delete(domain, key)</b><br>
deletes value.<br>
if domain-key does not exits: gives no error.