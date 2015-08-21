Bots 3.2.0rc was released 2014-03-22.<br>
Bots 3.2.0rc2 was released 2014-05-27.<br>
Bots 3.2.0 was released 2014-09-02.<br>

Migration notes:<br>
<ol><li>bots 3.2.0 is suited for django 1.4, 1.5, 1.6 and 1.7. Support for Django 1.3 is dropped.<br>
</li><li>in existing settings.py django requires parameter 'ALLOWED_HOSTS'. Add this as eg:<br>
<pre><code>    ALLOWED_HOSTS = ['*']<br>
</code></pre>
</li><li>For SQLite no database migration is needed. For MySQL and PostgreSQL: in table unique, field 'domein' should be changed to 70 positions (was: 35) if using option to have in-communication connect failures reported after xx times (field 'Max failures' in channels).<br>
</li><li>Python 2.5 is not supported anymore. use 2.6, preferably 2.7.<br>
</li><li>Bots does not support python > 3 (yet). Reason is that python MySQL connector is not suited for python 3 (yet).