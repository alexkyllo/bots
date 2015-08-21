## Using virtualenv ##
virtualenv is a tool to create isolated Python environments. Please refer to the [virtualenv package documentation](https://pypi.python.org/pypi/virtualenv) to understand what it does and how to install it. Virtual environments are not just for Bots; you can use them for any other python development. That is why I started investigating this methodology.<br>

This guide is based on information from the following links.<br>
<a href='https://zignar.net/2012/06/17/install-python-on-windows/'>https://zignar.net/2012/06/17/install-python-on-windows/</a><br>
<a href='http://www.stuartellis.eu/articles/python-development-windows/'>http://www.stuartellis.eu/articles/python-development-windows/</a><br>

<h3>Installation</h3>
1. Install python: You have probably done this already! Make sure you have the paths of your <code>python27</code> and <code>python27\scripts</code> included in the <a href='http://en.wikipedia.org/wiki/PATH_%28variable%29'>system path variable</a>.<br>
<br>
2. Install distribute: Download <a href='http://python-distribute.org/distribute_setup.py'>distribute_setup.py</a> and invoke it using python.<br>
<pre><code>&gt;&gt; python C:\Path\to\distribute_setup.py<br>
</code></pre>

3. Install Pip: Download <a href='https://raw.github.com/pypa/pip/master/contrib/get-pip.py'>get-pip.py</a> (right click, save as) and invoke it using python.<br>
<pre><code>&gt;&gt; python C:\Path\to\get-pip.py<br>
</code></pre>

4. Install Virtualenv: Once Pip is installed, installing any other package (that is available in the Python Package Index) is easy.<br>
<pre><code>&gt;&gt; pip install virtualenv<br>
</code></pre>

5. Install C and C++ compilers (optional): Not all python libraries are pure python, some may contain C code that must be compiled to install successfully. Download <a href='http://sourceforge.net/projects/mingw/'>MinGW</a>, run it, and select the C and C++ compilers to install. When complete, edit the file <code>Python27\Lib\distutils\cygwincompiler.py</code> and remove <code>-mno-cygwin</code> from lines 322-326. This flag is no longer supported. You also need to add a setting to each virtual environment that needs to use the compilers (described in the next section). Make sure you have the path of your <code>MinGW\bin</code> included in the <a href='http://en.wikipedia.org/wiki/PATH_%28variable%29'>system path variable</a>.<br>
<br>
<h3>Create your environments</h3>
Technically your virtual environments can be stored and scattered anywhere, but it makes sense to keep them all grouped together. I suggest you create a "root" directory for environments, each environment will be a subdirectory, eg.<br>
<pre><code>D:\&gt; mkdir PythonEnv<br>
D:\&gt; cd PythonEnv<br>
D:\PythonEnv&gt;<br>
</code></pre>

Create as many environments as you need (for ease of use, keep environment names short but meaningful and without spaces), eg. bots310<br>
<pre><code>D:\PythonEnv&gt; virtualenv bots310<br>
New python executable in bots310\Scripts\python.exe<br>
Installing Setuptools...........................................................<br>
............................done.<br>
Installing Pip..................................................................<br>
.......................done.<br>
<br>
D:\PythonEnv&gt;<br>
</code></pre>

If you installed compilers in the previous section and want to use them for this environment, then edit <code>Lib\distutils\distutils.cfg</code> within the environment folder, and add<br>
<pre><code>[build]<br>
compiler=mingw32<br>
</code></pre>

<h3>Activate and deactivate environments</h3>
To activate an environment, use the activate command in it's script directory. Notice your command prompt changes to show the active environment in brackets. Only one environment can be "activated" at a time, in order to install modules etc.<br>
<pre><code>D:\PythonEnv&gt; bots310\scripts\activate<br>
(bots310) D:\PythonEnv&gt;<br>
</code></pre>
To deactivate the current environment, use the deactivate command. Notice your command prompt changes back to show no active environment in brackets.<br>
<pre><code>(bots310) D:\PythonEnv&gt; deactivate<br>
D:\PythonEnv&gt;<br>
</code></pre>
Optional; create an activate.bat file in your environment root directory. This gives you a shortcut to activate environments.<br>
<pre><code>REM activate.bat gives you a shortcut to activate python environments<br>
REM eg. activate bots310<br>
call "%1\scripts\activate"<br>
</code></pre>

<h3>Install Bots in a virtual environment</h3>
First, activate the required environment.<br>
Install Bots and dependencies using pip (don't use the Bots Windows installer, because it installs to the default python folder!)<br>
<br>
<h4>Install Bots from local downloaded .tar.gz file</h4>
<pre><code>(bots310) D:\PythonEnv&gt; pip install .\bots-3.1.0.tar.gz<br>
Unpacking d:\pythonenv\bots-3.1.0.tar.gz<br>
  Running setup.py egg_info for package from file:///d7C%5Cpythonenv%5Cbots-3.1.0.tar.gz<br>
<br>
Installing collected packages: bots<br>
  Running setup.py install for bots<br>
<br>
Successfully installed bots<br>
Cleaning up...<br>
<br>
(bots310) D:\PythonEnv&gt;<br>
</code></pre>

<h4>Install Django (version 1.4.x)</h4>
<pre><code>(bots310) D:\PythonEnv&gt;pip install Django==1.4.6<br>
Downloading/unpacking Django==1.4.6<br>
  Downloading Django-1.4.6.tar.gz (7.7MB): 7.7MB downloaded<br>
  Running setup.py egg_info for package Django<br>
<br>
Installing collected packages: Django<br>
  Running setup.py install for Django<br>
<br>
Successfully installed Django<br>
Cleaning up...<br>
<br>
(bots310) D:\PythonEnv&gt;<br>
</code></pre>
<h4>Install cherrypy (latest)</h4>
<pre><code>(bots310) D:\PythonEnv&gt; pip install cherrypy<br>
Downloading/unpacking cherrypy<br>
  Downloading CherryPy-3.2.4.tar.gz (424kB): 424kB downloaded<br>
  Running setup.py egg_info for package cherrypy<br>
<br>
Installing collected packages: cherrypy<br>
  Running setup.py install for cherrypy<br>
<br>
Successfully installed cherrypy<br>
Cleaning up...<br>
<br>
(bots310) D:\PythonEnv&gt;<br>
</code></pre>
<h4>Install Genshi (optional, required for template-html output)</h4>
<pre><code>(bots310) D:\PythonEnv&gt; pip install Genshi<br>
Downloading/unpacking Genshi<br>
  You are installing a potentially insecure and unverifiable file. Future versions of pip will default to disallowing insecure files.<br>
  Downloading Genshi-0.7.tar.gz (491kB): 491kB downloaded<br>
  Running setup.py egg_info for package Genshi<br>
<br>
    warning: no files found matching 'COPYING' under directory 'doc'<br>
    warning: no previously-included files matching '*' found under directory 'doc\logo.lineform'<br>
    warning: no previously-included files found matching 'doc\2000ft.graffle'<br>
    warning: no previously-included files matching '*.pyc' found anywhere in distribution<br>
Installing collected packages: Genshi<br>
  Running setup.py install for Genshi<br>
    building 'genshi._speedups' extension<br>
    C:\MinGW\bin\gcc.exe -mdll -O -Wall -ID:\Python27\include -ID:\PythonEnv\bots310\PC -c genshi/_speedups.c -o build\temp.win32-2.7\Release\genshi\_speedups.o<br>
    C:\MinGW\bin\gcc.exe -shared -s build\temp.win32-2.7\Release\genshi\_speedups.o build\temp.win32-2.7\Release\genshi\_speedups.def -LD:\Python27\Libs -LD:\PythonEnv\bots310\libs -LD:\PythonEnv\bots310\PCbuild -lpython27 -lmsvcr90 -obuild\lib.win32-2.7\genshi\_speedups.pyd<br>
<br>
    warning: no files found matching 'COPYING' under directory 'doc'<br>
    warning: no previously-included files matching '*' found under directory 'doc\logo.lineform'<br>
    warning: no previously-included files found matching 'doc\2000ft.graffle'<br>
    warning: no previously-included files matching '*.pyc' found anywhere in distribution<br>
Successfully installed Genshi<br>
Cleaning up...<br>
<br>
(bots310) D:\PythonEnv&gt;<br>
</code></pre>

<h4>Install cdecimal (optional, improves <a href='http://code.google.com/p/bots/wiki/Performance'>performance</a>)</h4>
This will not install/compile correctly on Windows using pip, and the installer is an msi (not exe) so easy_install won't work either. You can install it manually though; the two files needed are <code>cdedimal.pyd</code> and <code>cdecimal-2.3-py2.7.egg-info</code> and they go in your virtual environment's <code>site-packages</code> directory. There are two ways to get these files.<br>
<ol><li>Install cdecimal in the default python folder (eg. <code>C:\python27\lib\site-packages</code>) using the windows msi installer, then copy the two files to your virtual environment.<br>
</li><li>Extract the files from the windows msi installer using a tool such as <a href='http://www.lupopensuite.com/db/universalextractor.htm'>universal extractor</a>.</li></ol>

<h4>Install pycrypto and paramiko (optional, required for sftp channels)</h4>
These will not install/compile correctly on Windows using pip. Instead, I used easy_install with a downloaded Windows installer exe.<br>
<pre><code>(bots310) C:\PythonEnv&gt;easy_install pycrypto-2.1.0.win32-py2.7.exe<br>
<br>
Processing pycrypto-2.1.0.win32-py2.7.exe<br>
creating 'c:\docume~1\adadmi~3\locals~1\temp\1\easy_install-wy9qt4\pycrypto-2.1.<br>
0-py2.7-win32.egg' and adding 'c:\docume~1\adadmi~3\locals~1\temp\1\easy_install<br>
-wy9qt4\pycrypto-2.1.0-py2.7-win32.egg.tmp' to it<br>
Moving pycrypto-2.1.0-py2.7-win32.egg to c:\pythonenv\bots310\lib\site-packages<br>
Adding pycrypto 2.1.0 to easy-install.pth file<br>
<br>
Installed c:\pythonenv\bots310\lib\site-packages\pycrypto-2.1.0-py2.7-win32.egg<br>
Processing dependencies for pycrypto==2.1.0<br>
Finished processing dependencies for pycrypto==2.1.0<br>
<br>
(bots310) C:\PythonEnv&gt;easy_install paramiko-1.7.6.win32.exe<br>
<br>
Processing paramiko-1.7.6.win32.exe<br>
creating 'c:\docume~1\adadmi~3\locals~1\temp\1\easy_install-mwtlnu\paramiko-1.7.<br>
6-py2.7-win32.egg' and adding 'c:\docume~1\adadmi~3\locals~1\temp\1\easy_install<br>
-mwtlnu\paramiko-1.7.6-py2.7-win32.egg.tmp' to it<br>
Moving paramiko-1.7.6-py2.7-win32.egg to c:\pythonenv\bots310\lib\site-packages<br>
Adding paramiko 1.7.6 to easy-install.pth file<br>
<br>
Installed c:\pythonenv\bots310\lib\site-packages\paramiko-1.7.6-py2.7-win32.egg<br>
Processing dependencies for paramiko==1.7.6<br>
Finished processing dependencies for paramiko==1.7.6<br>
</code></pre>

<h3>Start Bots Webserver in the virtual environment</h3>
You can simply start the webserver manually from commandline. The variable %VIRTUAL_ENV% contains the path to the activated environment. Using the start command causes a new console window to be opened.<br>
<pre><code>(bots310) D:\PythonEnv&gt; start python %VIRTUAL_ENV%\scripts\bots-webserver.py<br>
</code></pre>
Alternatively you can modify the environment's activate command (it is a small batch file of about 25 lines). Edit <code>%VIRTUAL_ENV%\scripts\activate.bat</code> and add the above command to the end. Then every time you activate the environment, the webserver is started too. Same for jobqueueserver (if required). I also add a window title. eg.<br>
<pre><code>start "webserver (bots310)" python %VIRTUAL_ENV%\scripts\bots-webserver.py<br>
</code></pre>

<h3>Running multiple Bots environments concurrently</h3>
Yes, this is possible!<br>
Although only a single environment can be "activated", once they are created you can run multiple bots webservers and engines simultaneously from different environments, if configured with different ports.<br>
<br>
bots.ini - use different ports for each environment. eg.<br>
<pre><code>[settings]<br>
#port used to assure only one instance of bots-engine is running. default: 28081<br>
port = 28091<br>
<br>
[webserver]<br>
#port at which at bots-gui is server. default is 8080<br>
port = 8090<br>
<br>
[jobqueue]<br>
# Port to use for the job queue xmlrpc server (on localhost). Default: 28082<br>
port = 28092<br>
</code></pre>
settings.py - add new setting for the session cookie name, and use a different name for each environment. This allows simultaneous login to each environment from the same browser. eg. use the environment name (default is 'sessionid')<br>
<pre><code>#*********sessions, cookies, log out time*************************<br>
SESSION_COOKIE_NAME = 'bots310'<br>
</code></pre>