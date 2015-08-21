## Multiple Environments (bots>=2.1) ##
There is more than one way of configuring multiple environments.<br>
Directories relevant for separate environments are:<br>
<ul><li><i>bots/config</i>: global configuration; eg values for usersys, botssys, database connection, port number.<br>
</li><li><i>bots/botssys</i>: storage of edi files, database, loggings etc.<br>
</li><li><i>bots/usersys</i>: grammars, mappings, route scripts etc.</li></ul>

<br>
<h3>1. Use config parameter</h3>

Each bots program "start script" accepts a parameter (-c) that indicates which config directory to use. Within config there are settings for botssys and usersys, so this gives us the ability to have separate environments. The default, if this parameter is not used, is <b>config</b>.<br>
<br>
<b>By example:</b>
<ol><li>Start with configuration with the default <i>config</i>, <i>usersys</i> and <i>botssys</i> directories in bots directory.<br>
</li><li>Purpose is to create a 2nd environment (env2).<br>
</li><li>Make copies of 3 directories within bots directory. Advised is to use the same name-suffix:<br>
<ul><li>Make copy of <i>config</i>, name it <i>config-env2</i>
</li><li>Make copy of <i>botssys</i>, name it <i>botssys-env2</i>
</li><li>Make copy of <i>usersys</i>, name it <i>usersys-env2</i>
</li></ul></li><li>Edit the configuration files in <i>config-env2</i> and change (at least) the following settings:<br>
<ul><li>in bots.ini<br>
<pre><code> botssys = botssys-env2<br>
 usersys = usersys-env2 <br>
</code></pre>
</li><li>settings.py<br>
<pre><code>DATABASE_NAME = os.path.join(PROJECT_PATH, 'botssys-env2/sqlitedb/botsdb')<br>
</code></pre>
</li></ul></li><li>Start bots scripts using the -c parameter to refer to the new environment, eg:<br>
<pre><code>bots-webserver.py -cconfig-env2<br>
bots-engine.py -cconfig-env2<br>
</code></pre>
Note: on linux the use of symlinks in bots directory might be useful.</li></ol>

<br>
<h3>2. Use different computers</h3>
Your production environment is on a server.<br>
Your development environment is on your desktop/laptop PC.<br>
In this way, you can replicate exactly the same setup (same python version etc), and transfer things from one to the other once tested.<br>

<br>
<h3>3. Using different python installations</h3>
I used this for a long time for windows.<br>
I had python2.5 and 2.6 installed;<br>
Bots in python 2.6 was my development environment; bots in python 2.5 was production.<br>
This is a very simple way to have 2 environments in windows.<br>
<br>
<br>
<h3>4. Using python virtualenv tool</h3>
<a href='https://pypi.python.org/pypi/virtualenv'>virtualenv</a> is a tool to create isolated Python environments.<br>
Each environment has a separate installation of bots and its dependencies, so <b>different versions</b> can be tested. You can activate and deactivate the environments as needed. You can use in combination with method 1 to have "config environments within python environments".<br>
<br><br>Mike has just started testing this method and will add <a href='DeploymentMultipleEnvironmentsVirtual.md'>details</a> soon...