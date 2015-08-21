## Main components of bots ##
  1. Bots-monitor: the user interface; the GUI; this is a web interface and runs in a web browser like Firefox, Chrome, or Internet Explorer.
    * Note: bots uses web technology for the interface - but bots does NOT communicate to the internet for this. All is on your local computer.
    * Bots-monitor can be accessed from all workstations in your LAN.
    * Warning: out-of-the-box bots-monitor uses plain HTTP and is not secure. Advised is either:
      * do not use bots-monitor over a public network (such as Internet)
      * secure the connection using [HTTPS/SSL](DeploymentHttps.md).
  1. Bots-webserver: program that serves web pages to bots-monitor. The bots-webserver has to run in order to use bots-monitor.
  1. Bots-engine: this program does the actual edi communication and translation.
    * Bots-engine does the communications and translations (of eg edifact or x12).
    * Bots-engine has no user interface (is a batch process).
    * To view the results of bots-engine, use bots-monitor.
    * After performing its actions bots-engine stops.

<br>
<h2>Start bots-monitor (using bots-webserver)</h2>
<ol><li>Start bots-webserver; several options:<br>
<ul><li>When bots is installed using with Windows installer use the 'shortcut' to Bots-webserver in your 'Programs' menu.<br>
</li><li>(<code>*</code>nix) Command line: <code> bots-webserver.py </code>
</li><li>(Windows, python 2.7) go to command line and: <code> c:\python27\python c:\python27\Scripts\bots-webserver.py </code>
</li></ul></li><li>Bots-webserver should stay running (and not disappear). If not, see <a href='StartGetBotsRunning#FAQ.md'>Start-up FAQ</a>.<br>
</li><li>View using your Internet browser<br>
<ul><li>When bots-webserver runs on the same computer, use address: <a href='http://localhost:8080'>http://localhost:8080</a>
</li><li>use Firefox, Chrome, Opera or Internet Explorer. Bots does NOT support Internet Explorer 6. Issues have been reported with IE8, but for some IE8 does work.<br>
</li><li>When accessing bots-monitor over your LAN (bots-webserver runs on another computer) the IP address or DNS name of that computer, e.g.: <code>http://192.168.10.10:8080</code>.<br>
</li></ul></li><li>Default login: user name 'bots', password 'botsbots'.<br>
</li><li>Tip: add 'bots' to your favorites/bookmarks.</li></ol>

<br>
<h2>Start bots-engine</h2>
There are several ways to start bots-engine:<br>
<ol><li>(windows, <code>*</code>nix) Start from bots-monitor: <i>bots-monitor->Run->Run (only new)</i>
</li><li>(<code>*</code>nix) Command line: <code> bots-engine.py </code>
</li><li>(Windows, python 2.7) go to command line and: <code> c:\python27\python c:\python27\Scripts\bots-engine.py </code></li></ol>

The results of what bots-engine has done can be viewed in the bots-monitor.<br>
Note: if you did not configure of bots to do something, the bots-engine will run but will not do much. To get bots to do something see <a href='StartMyFirstPlugin.md'>Tutorial</a>.<br>
<br>
<br>
<h2>FAQ</h2>
<ul><li>When starting bots-webserver the window disappears after a few seconds?<br>
<ul><li>Start the bots-webserver from the command line; you will be able to see what goes wrong. (Windows, python 2.7) go to command line and: <code> c:\python27\python c:\python27\Scripts\bots-webserver.py </code>
</li><li>For the most common cause for the problem see the next question.<br>
</li></ul></li><li>Bots-webserver gives error: IOError: Port 8080 not free on 'x.x.x.x' (or similar).<br>
<ul><li>Another program already uses this 'port'.<br>
</li><li>Adapt the port bots uses: in configuration file <i>bots/config/bots.ini</i> look for 'port'.<br>
</li><li>Change port to eg 8090<br>
</li><li>Start bots-webserver again.<br>
</li><li>In your browser you will have to indicate another port eg: <a href='http://localhost:8090'>http://localhost:8090</a>
</li></ul></li><li>Can I run multiple instances of bots-engine in parallel?<br>
<ul><li>No, this is not possible.<br>
</li><li>Instead bots >= 3.0 has better control of running the engine: <a href='Jobqueue.md'>jobqueue-server</a>.