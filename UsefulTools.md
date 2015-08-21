## Useful tools for working with Bots ##

These are programs you can use in bots development and deployment. (please add more)

<br>
<h2>Text Editors</h2>
Any text editor you use should have syntax colouring/highlighting. This makes it much easier to spot any mistakes. It is also good to be able to run python to do syntax checks. Also a good search/replace function (eg to add extra CR/LF in edifact or x12 files).<br>
<br>
<ul><li><b><a href='http://www.editplus.com/index.html'>EditPlus</a></b> (Windows) is the editor I have used for many years and so continued to use it with Python. There are no python syntax files in the default installation but you can easily <a href='http://www.editplus.com/javacpp.html'>download</a> and add them, several versions are available. You can also add a "user tool" option to run a python syntax check directly in the editor, and one to run the bots grammar check.<br>
</li><li><b><a href='http://www.scintilla.org/SciTE.html'>Scite</a></b> (Windows, Linux) provides Python syntax highlighting and python syntax check directly in the editor to check the correctness of Python scripts.<br>
</li><li><b><a href='http://www.geany.org/'>Geany</a></b> (Windows, Linux) provides Python syntax highlighting and python syntax check directly in the editor to check the correctness of Python scripts. Quite similar to scite, but more fancy eg with spell checking. Web site calls it an IDE.<br>
</li><li><b><a href='http://www.barebones.com/products/textwrangler/'>TextWrangler</a></b> (Mac) provides Python syntax highlighting and python syntax check directly in the editor to check the correctness of Python scripts. Also quite similar to Scite, very interesting access to remote scripts via SSH/SFTP.</li></ul>

<br>
<h2>IDE (Integrated Development Environment)</h2>
These are a "step up" from just using a text editor. Please add more if you have anny experience with these.<br>
<br>
<ul><li><b><a href='http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/indigosr2'>Eclipse</a></b> with <a href='http://marketplace.eclipse.org/node/114'>PyDev</a>. You just create a project in the bots directory and edit everything from that folder.</li></ul>

<br>
<h2>Compare and merge</h2>
Tool for comparing files and directories, analyse changes and copy code changes eg between test and production environments.<br>
<ul><li><b><a href='http://winmerge.org/'>Winmerge</a></b> (Windows)<br>
</li><li><b><a href='http://meldmerge.org/'>Meld</a></b> (linux)<br>
</li><li><b><a href='http://sourceforge.net/projects/tkdiff/'>Tkdiff</a></b> (windows,linux)<br>
</li><li><b><a href='http://kdiff3.sourceforge.net/'>KDiff3</a></b> (linux)</li></ul>


<br>
<h2>Database</h2>
<ul><li><b><a href='http://www.sqlite.org/'>SQLite Expert</a></b> (Windows, Linux) is a database browser tool for SQLite. Useful for advanced troubleshooting or learning more about Bots internal workings. You can use SQL commands to do quick updates or create reports. Note: I use an old version (1.7) as the newer versions are much larger and slower and offer nothing more useful.<br>
</li><li><b><a href='http://www.heidisql.com/download.php'>HeidiSQL</a></b> (Windows) can be used similarly to the above for bots installations using the MySQL database. A lightweight interface for managing MySQL and Microsoft SQL databases. It enables you to browse and edit data, create and edit tables, views, procedures, triggers and scheduled events. Also, you can export structure and data either to SQL file, clipboard or to other servers.<br>
</li><li><b><a href='http://dev.mysql.com/downloads/workbench/'>MySQL Workbench</a></b> (multiple platforms) is the full blown MySQL management toolset. It provides an integrated tools environment for Database Design & Modeling, SQL Development (replacing MySQL Query Browser) and Database Administration (replacing MySQL Administrator). The Community (OSS) Edition is available from this page under the GPL.</li></ul>

<br>
<h2>Other tools</h2>
<ul><li><b><a href='http://www.izarc.org/'>IZArc</a></b> (Windows) is an archive tool that allows you to open bots plugins (zip files) and easily modify their contents.<br>
</li><li><b><a href='http://www.baremetalsoft.com/baretail/'>BareTail</a></b> (Windows) is a free real-time log file monitoring tool. It is useful for watching Bots log files (engine.log, webserver.log etc). Multiple tabbed interface, colour highlighting, single small program, no installer.