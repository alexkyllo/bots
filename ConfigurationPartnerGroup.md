## Using partner groups ##

edi-partners can be assigned to groups.<br>

This might come in handy:<br>
<ul><li>partner dependent translations (in <i>bots-monitor->Configuration->Translations</i>). Select a group here, and translation is done for all members of the group.<br>
</li><li>partner-based filtering for routes/outchannel  (in <i>bots-monitor->Configuration->Routes</i>): the outchannel is used for all members of the group.<br>
</li><li>in selections you can use partner-groups.<br>
Note: partner-groups do not work for confirmations.</li></ul>

<br>
<h3>How to</h3>
<ol><li>Create a group in <i>bots-monitor->Configuration->Partners & groups</i>. Indicate it is a group using tick-box 'Isgroup'.<br>
</li><li>For the partners in a group, assign them to this group using 'Is in groups'.</li></ol>

<br>
<h3>Plugin</h3>
Plugin 'demo_partnerdependent' at <a href='http://sourceforge.net/projects/bots/files/plugins/'>the bots sourceforge site</a> demonstrates partner-groups.