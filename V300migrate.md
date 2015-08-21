## Migrate/update to 3.0.0 ##

## Introduction ##
Version 3.0 is a bigger update for bots, view [all changes](Migrate300#List_of_Changes.md). Overview:
  1. Django 1.1 and 1.2 are not supported anymore. Supported are django 1.3 and 1.4.
  1. Settings.py is changed. Advised: use the new settings.py, and do your customization in the new setting.py (eg for error reports, maybe database and timezone).
  1. The database has changed. A script is included to change the database. I had no database issues while testing this migration.
  1. lots of changes in bots.ini. The 'old' bots.ini is OK, but it is advised to use new bots.ini, and do your customizations there.
  1. Excel input: does work; but is now an incoming messagetype and not via 'preprocessing'.
  1. Most user scripts will work; many user scripts are not needed anymore because the functionality is provided by bots now.
  1. Some functions that may be used in user scripting have changed:
    * botslib.change() -> botslib.changeq(). This function is used to in processing incoming 997's and CONTRL!!
    * botsengine routescripts: for 'new' runs in routescript botsengine.py called function postnewrun(routestorun) -> postnew(routestorun)
    * communication.run(idchannel,idroute) -> communication.run(idchannel,command,idroute). Command is one of: 'new','automaticretrycommunication','resend','rereceive'.
    * transform.run(idchannel,idroute) -> transform.run(idchannel,command,idroute). Command is one of: 'new','automaticretrycommunication','resend','rereceive'.

My experiences: after changing settings.py and database migration, all works (except for and issues mentioned above).
<br>
<br>
<h2>Summary of procedure</h2>
<ol><li>make a backup!<br>
</li><li>rename existing installation.<br>
</li><li>do a fresh install.<br>
</li><li>copy old data to new installation.<br>
</li><li>change settings<br>
</li><li>update the database.<br>
Comments:<br>
</li><li>It is critical to change the settings before updating the database! Bots finds the right database via the settings!<br>
</li><li>If you use MySQL or PostGreSQL: same procedure. The bots-updatedb script also updates MySQL or PostGreSQL.<br>
</li><li>Tested this for migration from bots2.2.1 -> 3.0.0, but works for all bots2.<code>*</code> installations.</li></ol>

<br>
<h2>Windows procedure</h2>
<ol><li>make a backup!<br>
</li><li>rename existing installation<br>
<ul><li>existing bots-installation is in C:\Python27\Lib\site-packages<br>
</li><li>renamed bots directory to bots221<br>
</li><li>also renamed existing directories for cherrypy, django, genshi.<br>
</li></ul></li><li>do a fresh install of bots3.0.0 installer (bots-3.0.0.win32.exe)<br>
</li><li>copy old data to new installation.<br>
<ul><li>in C:\Python27\Lib\site-packages new directories have been installed (bots, django, cherrypy, genshi)<br>
</li><li>copy directories botssys and usersys from bots221-directory to bots directories. Everything can be overwritten.<br>
</li></ul></li><li>change settings<br>
<ul><li>use new config/bots.ini, adapt for your own values.<br>
</li><li>use new config/settings.py, adapt for your own values. Especially the database settings are important; the format is slightly different (but similar enough to give no problem); critical is using the 'ENGINE'-value of the new settings.py.<br>
</li></ul></li><li>update the database.<br>
<ul><li>use command-prompt/dos-box<br>
</li><li>goto directory C:\Python27\Scripts<br>
</li><li>command-line: <code>C:\Python27\python bots-updatedb.py</code>
</li><li>should report that database is successful changed.<br>
If you use a 64-bits version of windows another option is to use the 64-bits versions of python and bots.<br>
<br>
<br>
<h2>Linux procedure</h2>
</li></ul></li><li>make a backup!<br>
</li><li>rename existing installation<br>
<ul><li>existing bots-installation is in /usr/local/lib/python2.7/dist-packages<br>
</li><li>renamed bots directory to bots221<br>
</li><li>for libraries: check you use at least django 1.3<br>
</li></ul></li><li>do a fresh install: see <a href='StartInstallProcedure.md'>installation procedure</a>
</li><li>copy old data to new installation.<br>
<ul><li>in /usr/local/lib/python2.7/dist-packages new bots-directory is installed.<br>
</li><li>copy directories botssys and usersys from bots221-directory to bots directories. Everything can be overwritten.<br>
</li><li>mind your rights!<br>
</li></ul></li><li>change settings<br>
<ul><li>use new config/bots.ini, adapt for your own values.<br>
</li><li>use new config/settings.py, adapt for your own values. Especially the database settings are important; the format is slightly different (but similar enough to give no problem); critical is using the 'ENGINE'-value of the new settings.py.<br>
</li></ul></li><li>update the database.<br>
<ul><li>command-line: <code>bots-updatedb.py</code>
</li><li>should report that database is successful changed.