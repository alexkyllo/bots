## Mapping script ##
> Definition: _Instructions to get data from incoming edi-message and put it in the outgoing edi-message_

Mapping scripts are python programs.<br>
Mapping script are in: <i>usersys/mappings/editype/mapping script name.py</i><br>
Within a mapping script function main() is called.<br>
<br>
<br>
Notes:<br>
<ul><li><b>All</b> data in the incoming/outgoing messages are strings.<br>
</li><li>Errors in a mapping script are caught by Bots and displayed in bots-monitor.<br>
</li><li>You can Raise an exception in your mapping script if you encounter an error situation.<br>
</li><li>(Bots>=3.0) if an error is raised in a script, other translations for message in same edi-file will continue.<br>
</li><li>(Bots>=3.0) when an error situation is met in script: you can send specific error-email to responsible people.