Note: the [tutorial](StartMyFirstPlugin.md) contains some detailed information and screen-shots of bots-monitor!

<br>
<h2>Menu in bots-monitor</h2>

<ol><li>Home: start page and general information.<br>
</li><li>Last run: view results of the last run:<br>
<ul><li>incoming: view incoming files and results<br>
</li><li>document: view status of business document. An edi file can contain multiple documents (eg orders). In this view are the results of the separate business documents. See <a href='ConfigurationBotskey.md'>setting document views</a>
</li><li>outgoing: view outgoing files and results<br>
</li><li>process errors: view process errors; mostly these will be communication errors.<br>
</li></ul></li><li>All runs: view results of all runs:<br>
<ul><li>reports: view of all runs and results<br>
</li><li>incoming: view incoming files and results<br>
</li><li>document: view status of business document. An edi file can contain multiple documents (eg orders). In this view are the results of the separate business documents. See <a href='ConfigurationBotskey.md'>setting document views</a>
</li><li>outgoing: view outgoing files and results<br>
</li><li>process errors: view process errors; mostly these will be communication errors.<br>
</li><li>confirmations: view the results of confirmations you wanted and confirmation you gave. See <a href='Confirmations.md'>setup confirmations</a>
</li></ul></li><li>Select: use criteria like date/time to view results you want to see like eg editype edifact or x12.<br>
<ul><li>Note: select screens can also be used using 'select' button in other views.<br>
</li></ul></li><li>Configuration: configuration of the edi setup.<br>
</li><li>System tasks (administrators only): read plugins, create plugins, maintain users, etc.<br>
</li><li>Run: manually start a run of bots-engine:<br>
<ul><li>Run (only new): receive, translate, and send new edi messages.<br>
</li><li>Run userindicated rerecieves: receive previously received edi-files again from archive. User has to mark edi-files as 're-receive' via incoming view.<br>
</li><li>Run userindicated resends: resend previously send edi-files again. User has to mark edi-files as 're-send' via outgoing view.</li></ul></li></ol>

<br>
<h2>User interface tips</h2>
<ul><li>View screens often have a star at the beginning of each line; moving over the star will show possible actions.<br>
</li><li>In view screens, you can see the contents of an edi file if you click on the file name.<br>
</li><li>When viewing the contents of an edi file, you can go backwards and forwards to see the processing steps of the file.<br>
</li><li>Might be handy to use tabbed browsing.<br>
</li><li>Bots uses user rights (viewers, administrators and superuser). See <a href='UserSecurity.md'>setting user rights</a>