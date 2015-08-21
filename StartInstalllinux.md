## Linux, Unix installation ##
There is no `*`.deb or `*`.rpm for bots - would be great if you have experience with this and want to give some help.<br>
So a standard python source code install is done.<br>
<ol><li>Install Python<br>
<ol><li>Check if Python is already installed - most of the time python is already installed on <code>*</code>nix. Use python 2.6 or 2.7. (not python >= 3.0).<br>
</li><li>If not: use package manager or see python web site.<br>
</li></ol></li><li>Install dependencies/libraries<br>
<ul><li>See <a href='StartInstallDependencies.md'>list of dependencies</a>.<br>
</li><li>Easiest is to use your package manager for installing.<br>
</li></ul></li><li>Install bots<br>
<ol><li>Download <a href='http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/'>bots installer</a> (e.g. bots-3.1.0.tar.gz)<br>
</li><li>Unpack (command-line):<br><code> tar bots-3.1.0.tar.gz </code>
</li><li>Go to created directory (command-line):<br><code> cd bots-3.1.0 </code>
</li><li>Install (command-line):<br><code> python setup.py install </code>
</li><li>Postinstall: depending on what do want: change rights for directories botssys, usersys and config or place these elsewhere and make symbolic links in the bots installation directories.</li></ol></li></ol>

Tip: place the directories botssys, usersys and config somewhere else (out of /usr), change the owner/rights and make symbolic links in the bots installation to these directories.<br>
<br>
<h3>Installation from scratch</h3>
(Note that versions might not be correct anymore.<br>
Installation on amazon EC2, looks like red hat version of linux:<br>
<pre><code>#install django<br>
wget -O django.tar.gz https://www.djangoproject.com/download/1.4.13/tarball/<br>
tar -xf django.tar.gz<br>
cd Django-1.4.13<br>
sudo python setup.py install<br>
cd ..      <br>
#install cherrypy<br>
wget http://download.cherrypy.org/CherryPy/3.2.2/CherryPy-3.2.2.tar.gz<br>
tar -xf CherryPy-3.2.2.tar.gz<br>
cd CherryPy-3.2.2<br>
sudo python setup.py install<br>
cd ..      <br>
#install Genshi<br>
wget http://ftp.edgewall.com/pub/genshi/Genshi-0.7.tar.gz<br>
tar -xf Genshi-0.7.tar.gz<br>
cd Genshi-0.7<br>
sudo python setup.py install<br>
cd ..      <br>
#install bots<br>
wget -O bots-3.1.0.tar.gz http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/3.1.0/bots-3.1.0.tar.gz/download<br>
tar -xf bots-3.1.0.tar.gz<br>
cd bots-3.1.0<br>
sudo python setup.py install<br>
cd .. <br>
#set rigths for bots directory to non-root:<br>
sudo chown -R myusername /usr/lib/python2.6/site-packages/bots<br>
 <br>
#start up bots-webserver:<br>
bots-webserver.py<br>
</code></pre>

<br>
<h3>Installation from scratch (bots2.2)</h3>
(Note that versions might not be correct anymore.<br>
Installation on vanilla CentOS6.2 (logged in as root):<br>
<pre><code>#install django<br>
wget http://www.djangoproject.com/download/1.3.1/tarball/<br>
tar -xf Django-1.3.1.tar.gz<br>
cd Django-1.3.1<br>
python setup.py install<br>
cd ..      <br>
#install cherrypy<br>
wget http://download.cherrypy.org/CherryPy/3.2.2/CherryPy-3.2.2.tar.gz<br>
tar -xf CherryPy-3.2.2.tar.gz<br>
cd CherryPy-3.2.2<br>
python setup.py install<br>
cd ..      <br>
#install Genshi<br>
wget http://ftp.edgewall.com/pub/genshi/Genshi-0.6.tar.gz<br>
tar -xf Genshi-0.6.tar.gz<br>
cd Genshi-0.6<br>
python setup.py install<br>
cd ..      <br>
#install bots<br>
wget http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/2.2.1/bots-2.2.1.tar.gz/download<br>
tar -xf bots-2.2.1.tar.gz<br>
cd bots-2.2.1<br>
python setup.py install<br>
cd .. <br>
     <br>
#start up bots-webserver:<br>
bots-webserver.py<br>
</code></pre>