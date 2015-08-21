Purpose of this tutorial is to get your first edi configuration running.<br>
This is done by installing plugin 'my_first_plugin'; this plugin provides a working configuration.<br>
When run, this configuration will read and write example edi messages (provided in the plugin) from your system.<br>
In this configuration incoming edifact orders are translated to a fixed file format.<br>
<br>
<br>
<h2>Install plugin 'my_first_plugin'</h2>
Assumed is:<br>
<ol><li>You've installed bots, see <a href='StartInstallProcedure.md'>installation</a>
</li><li>You've managed to get bots-monitor running, see <a href='StartGetBotsRunning.md'>get bots running</a>.</li></ol>

Now download and install plugin 'my_first_plugin'.<br>
Instructions for installing a plugin are <a href='PluginInstall.md'>here</a>.<br>
The plugin can be downloaded from <a href='http://sourceforge.net/projects/bots/files/plugins/'>the bots sourceforge site</a>.<br>
<br>
<br>
<h2>Activate the route</h2>
<ol><li>go to the routes screen: <i>bots-monitor->Configuration->Routes</i>
</li><li>note that route 'myfirstroute' is not active now (indicated by red icon)<br>
</li><li>select the tick-box in front of the route 'myfirstroute'<br>
</li><li>select action 'activate/de-activate'<br>
</li><li>click on the 'Go'-button behind the selected action.<br>
</li><li>note that route 'myfirstroute' is active now (indicated by green icon)</li></ol>

<br>
<h2>Run the translation</h2>
Run the translation: <i>bots-monitor->Run->Run (Only New)</i>.<br>
You will get notified that the bots-engine is started.<br>
Bots-engine is the part of bots that does the translations and communications; it runs in the background. Bots-engine will be finished in approximately one second.<br>
<br>
<br>
<h2>View the results</h2>
Now let's view the results of the translation:<br>
<ul><li>First look at the results of the run: <i>bots-monitor->All runs->Reports (per run)</i>. Each run of bots is represented by a line; the last run is on top.<br>
</li><li>View the incoming files via <i>bots-monitor->Last run->Incoming</i>. Click on the incoming file to see its contents.<br>
</li><li>View the outgoing files (the results of the translation) go to or <i>bots-monitor->Last run->outgoing</i>. Again: click on the file name to see its contents.</li></ul>

Note: this configuration reads the incoming files but does not delete them. So you can run it over and over again.<br>
<br>
<br>
<h2>More</h2>
<ul><li>Screenshots and information about <a href='StartMyFirstPluginResults.md'>viewing the results</a>.<br>
</li><li>Walk through the configuration in this plugin is <a href='StartMyFirstPluginSetup.md'>here</a>.<br>
</li><li>A more detailed explanation about the 'run' and what happens in a run is <a href='StartMyFirstPluginDepth.md'>here</a>.</li></ul>



