## Direct database communication ##

Bots can read and write from a database.<br>
See plugin demo_databasecommunication on the <a href='https://sourceforge.net/projects/bots/files/plugins/'>bots sourceforge site</a>.<br>

<br>
<h3>Discussion: direct database communication or not</h3>
In most edi setups there is no direct database communication, but an intermediate file is used:<br>
<ul><li>inbound edi: bots translates edi files to your import format<br>
</li><li>outbound edi: the export files of your application are translated by bots to the wished edi format.</li></ul>

<br>
Reasons to set up edi using an intermediate file:<br>
<ul><li>it is better to do the import/export with the tools you are familiar with, and not to use a new tool (knowledge, maintenance).<br>
</li><li>different edi partners do use different standards (dialects of the standards, different interpretations, different countries, different sectors, edi standards are not that good). Try to use one import/export format; let the edi software handle the differences between partners.</li></ul>

<br>
Reasons to use direct database format:<br>
<ul><li>import/exports are very simple/straightforward<br>
</li><li>your system does not (yet) have good functionality for handling the incoming edi data. Example: receive sales reports, but what to do with this? This data is quite simple, just import this in one (new) table. The users can query this table for information.</li></ul>

<br>
<h3>Inbound edi (write to database)</h3>

<ul><li>Translation rule should be to edi-type 'db'<br>
</li><li>In the mapping script: out.root should be a python object (dict, list, class, etc); this object is passed to the actual database connector.<br>
</li><li>Outgoing channel should be type 'db'.<br>
</li><li>Use a communication script for the outgoing channel (usersys/communicationscripts/channelname.py). This communication script does the actual communication with the database.<br>
</li><li>In the communication script should be 3 functions:<br>
<ul><li>connect - build database connection.<br>
</li><li>out-communicate - put the data in the database using the data as received from the mapping script.<br>
</li><li>disconnect - close database connection.<br>
</li></ul></li><li>Use the database connector as needed, eg: python provides by default the sqlite3 connector, mysql-Python as MySQL database connector, psycopg2 as PostgreSQL database connector, etc</li></ul>

<br>
<h3>Outbound edi (read from database)</h3>
<ul><li>Incoming channel should be type 'db'.<br>
</li><li>Use a communication script for the incoming channel (usersys/communicationscripts/channelname.py). This communication script does the actual communication with the database.<br>
</li><li>In the communication script should be 3 functions:<br>
<ul><li>connect - build database connection.<br>
</li><li>incommunicate - fetch the data from the database, send it to the mapping script.<br>
</li><li>disconnect - close database connection.<br>
</li></ul></li><li>Use the database connector as needed, eg: python provides by default the sqlite3 connector, mysql-Python as MySQL database connector, psycopg2 as PostgreSQL database connector, etc<br>
</li><li>Translation should be from edi-type 'db'<br>
</li><li>In the mapping script: inn.root is the data as received from the database connector.<br>
</li><li>Note: the data passed from the communication-script can be any python object (eg dict, list). If a list (or tuple) is return from the communication script, bots passes each member of the list as a separate edi-message to the mapping script.