# Bots directories, executables and files #

## Where can I find bots on my system? ##
  * Windows (depends upon python version used):
    * eg. _C:\python27\Lib\site-packages\bots_
  * Linux, Unix:
    * _/usr/lib/python2.7/site-packages/bots_
    * _/usr/local/lib/python2.7/dist-packages/bots_ (Debian, Ubuntu)
Note: in the main screen (home) of bots-monitor (GUI) you can see where the bots-directories are.
<br>
<br>
<h2>Where are the programs/executable scripts?</h2>
</li></ul>  * Where installed
    * Windows (depends upon python version used): _C:\python27\Scripts_
    * Linux, Unix eg in _/usr/bin/_ or _/usr/local/bin/_
  * Overview of executables:
    * bots-webserver.py - serves the html-pages for the bots-monitor.
    * bots-engine.py - does the actual edi communication and translation.
    * bots-jobqueueserver.py - the jobqueue-server maintains a queue with (job-engine) jobs and fires these asap.
    * bots-job2queue.py - to send jobs to the jobqueueserver
    * bots-dirmonitor.py - monitors/watches directoriess; if a file is placed in a directory, bots-engine stats (via jobqueueserver)
    * bots-grammarcheck.py - utility to check a grammar.
    * bots-xml2botsgrammar.py - utility to generate an xml-grammar from an xml file.
    * bots-updatedb.py - for version migrations: updates the database to new definition/schema
    * bots-plugoutindex.py - for version control systems: generate a file with the configuration (routes, channels, etc). (configuration as in the database).
Note: for the usage instructions of the executables use 'help', eg:
```
bots-engine.py --help
```

<br>
<h2>Where are the edi files?</h2>
<ul><li>Incoming and outgoing<br>
<ul><li>Set this per channel, using 'path' and 'filename'.<br>
</li><li>Relative path is relative to bots directory, absolute paths are OK.<br>
</li><li>In the plugins the edi-files are in <i>bots/botssys/infile</i>
</li></ul></li><li>The archive/backup.<br>
<ul><li>each communication channel of bots CAN archive the incoming or outgoing edi messages.<br>
</li><li>Set this per channel, using 'archivepath'.<br>
</li><li>The place of the archive can be 'anywhere'. We mostly use botssys/archive.<br>
</li><li>Relative path is relative to bots directory, absolute paths are OK.<br>
</li></ul></li><li>Internal storage of edi data.<br>
<ul><li>in subdirectories of bots/botssys/data.<br>
</li><li>this is where the edi files are fetched from by the bots-monitor (the 'filer' module).<br>
</li></ul></li><li>Cleanup of old files<br>
<ul><li>bots manages cleanup of archive and internal storage, based on configuration settings for number of days to keep.<br>
</li><li>Incoming files are (usually, unless testing) removed by the channel setting "remove".<br>
</li><li>Outgoing files are never removed by bots</li></ul></li></ul>

<br>
<h2>The directory structure within bots directory</h2>
<ul><li><i>bots</i>: source code (<code>*</code>.py, <code>*</code>.pyc, <code>*</code>.pyo)<br>
<ul><li><i>bots/botssys</i>: data file, database, etc<br>
<ul><li><i>bots/botssys</i>: when installing a plugin bots makes a backup of configuration here.<br>
</li><li><i>bots/botssys/data</i>: internal storage of edi data.<br>
</li><li><i>bots/botssys/sqlitedb</i>: database file(s) of SQLite.<br>
</li><li><i>bots/botssys/logging</i>: log file(s) for each run of bots-engine.<br>
</li><li><i>bots/botssys/infile</i>: plugins place here example edi data<br>
</li><li><i>bots/botssys/outfile</i>: plugins place here translated edi data<br>
</li></ul></li><li><i>bots/config</i>: <a href='StartConfigurationFiles.md'>configuration files</a>. See also <a href='DeploymentMultipleEnvironments.md'>multiple environments</a>.<br>
</li><li><i>bots/install</i>: contains an empty sqlite database and default configuration files.<br>
</li><li><i>bots/installwin</i>: (windows) python libraries used during installation.<br>
</li><li><i>bots/locale</i>: translation/internationalisation files for use of another language.<br>
</li><li><i>bots/media</i>: static data for bots-webserver (CSS, html, images, JavaScript)<br>
</li><li><i>bots/sql</i>: sql files for initialising a new database.<br>
</li><li><i>bots/templates</i>: templates for bots-webserver<br>
</li><li><i>bots/templatetags</i>: custom template-tags for use in django.<br>
</li><li><i>bots/usersys</i>: <a href='UserScriptingIntroduction.md'>user scripts</a>.<br>
<ul><li><i>bots/usersys/charsets</i>: e.g. edifact uses its own character-sets.<br>
</li><li><i>bots/usersys/communicationscripts</i>: user scripts for communication (inchannel, outchannel).<br>
</li><li><i>bots/usersys/envelopescripts</i>: user scripts for enveloping.<br>
</li><li><i>bots/usersys/grammars</i>: grammars of edi-messages; directories per editype (x12, edifact, tradacoms, etc).<br>
</li><li><i>bots/usersys/mappings</i>: mappings scripts; directories per editype (incoming).<br>
</li><li><i>bots/usersys/partners</i>: partner specific syntax for outgoing messages; directories per editype.<br>
</li><li><i>bots/usersys/routescripts</i>: user scripts for running (part of) route.<br>
</li><li><i>bots/usersys/codeconversions</i>: for conversions of codes (deprecated).<br>
</li><li><i>bots/usersys/dbconnectors</i>: user scripts for communication from/to database (old database connector, deprecated).