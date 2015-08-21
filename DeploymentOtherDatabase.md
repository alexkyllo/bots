# Use MySQL or PostgreSQL as database #
Backgrond information:
  * Default bots uses a SQLite database. This is included in the standard installation and works out-of-the-box. Performance of SQLite is good!
  * Bots always uses utf-8 in the database communication.
  * Database tables are installed using django-machinery. See django docs.
  * After installation, you may want to [migrate some data](MigrateDatabase.md).
  * You might have to manually add a database trigger if using [persist functions](MappingPersist.md).

<br>
<h2>PostgreSQL</h2>
<ol><li>install PostgreSQL.<br>
</li><li>install psycopg2 as python database adapter.<br>
</li><li>login in command line client of database.<br>
</li><li>Create database (CLI) : <code> CREATE DATABASE botsdb WITH ENCODING 'UTF8'; </code>
</li><li>Create user (CLI): <code> CREATE USER bots WITH PASSWORD 'botsbots'; </code>
</li><li>Give user rights: (CLI) <code> GRANT ALL PRIVILEGES ON DATABASE botsdb TO bots; </code>
</li><li>make sure database accepts connections over (non-local) TCP/IP: change parameter listen_addresses in in postgresql.conf; add/change setting for user in pg_hba.conf.<br>
</li><li>Set connection parameter in bots configuration in <i>bots/config/settings.py</i>. Examples are provided - see comments in settings.py<br>
</li><li>Create the required tables (CLI):<br>
<ul><li>(CLI) <code> django-admin syncdb  --settings='bots.config.settings' </code>
</li><li>(CLI) or when bots is not installed in the default directory: <code> django-admin syncdb --pythonpath='path to bots' --settings='bots.config.settings' </code>
</li><li>Django asks for name etc of default user.</li></ul></li></ol>

<br>
<h2>MySQL</h2>
<ol><li>install MySQL.<br>
</li><li>install mysql-Python as python database adapter.<br>
</li><li>login in command line client of database.<br>
</li><li>Create database (CLI): <code> CREATE DATABASE botsdb DEFAULT CHARSET utf8; </code>
</li><li>Create user (CLI): <code> CREATE USER 'bots' IDENTIFIED BY 'botsbots'; </code>
</li><li>Give user rights (CLI): <code> GRANT ALL PRIVILEGES ON botsdb.* TO 'bots'; </code>
</li><li>make sure database accepts connections over (non-local) TCP/IP: change parameter 'binds' in /etc/mysql/my.cfg.<br>
</li><li>Set connection parameter in bots configuration in <i>bots/config/settings.py</i>. Examples are provided - see comments in settings.py<br>
</li><li>Create the required tables:<br>
<ul><li>(CLI) <code> django-admin syncdb  --settings='bots.config.settings' </code>
</li><li>(CLI) or when bots is not installed in the default directory: <code> django-admin syncdb --pythonpath='path to bots' --settings='bots.config.settings' </code>
</li><li>Django asks for name etc of default user.</li></ul></li></ol>

<br>
<h2>MySQL on Windows</h2>
<ol><li>Download <a href='http://www.mysql.com/downloads/mysql/'>MySQL community server</a> msi installer. (tested version 5.5.20)<br>
</li><li>Run the installer, do a "typical" installation and follow the prompts. On the final screen, make sure <i>Launch the MySQL Instance Configuration Wizard</i> box is ticked.<br>
</li><li>When the configuration wizard starts, make the following selections:<br>
<ul><li>Detailed configuration<br>
</li><li>Server machine (you may choose developer for your bots test environment)<br>
</li><li>Transactional database<br>
</li><li>DSS/OLAP (20 connections)<br>
</li><li>Enable TCP/IP and Strict mode (defaults)<br>
</li><li>Best support for multilingualism (<b>UTF8</b>)<br>
</li><li>Install as Windows service (default)<br>
</li><li>Modify security settings; enter a root password and write it down.<br>
</li><li>Execute configuration<br>
</li><li>Create a shortcut to <i>C:\Program Files\MySQL\MySQL Server 5.5\bin\MySQLInstanceConfig.exe</i> in case you want to modify any of these settings later.<br>
</li></ul></li><li>Go to <i>Start > Programs > MySQL > MySQL Server > MySQL Command Line Client</i>. Enter your root password when prompted. You should now have a <code>mysql&gt;</code> command prompt.<br>
</li><li>Enter the following MySQL commands at the prompt:<br>
<pre><code>mysql&gt; CREATE DATABASE botsdb DEFAULT CHARSET utf8;<br>
 Query OK, 1 row affected (0.01 sec)<br>
<br>
mysql&gt; CREATE USER 'bots' IDENTIFIED BY 'botsbots';<br>
 Query OK, 0 rows affected (0.00 sec)<br>
<br>
mysql&gt; GRANT ALL ON botsdb.* TO 'bots';<br>
 Query OK, 0 rows affected (0.03 sec)<br>
<br>
</code></pre>
</li><li>Download and install <a href='http://www.codegood.com/downloads'>MySQL-python for Windows</a> to suit your python version (tested MySQL-python-1.2.3.win32-py2.7.exe)<br>
</li><li>Set connection parameters in bots configuration in <i>bots/config/settings.py</i>. MySQL example is provided, I only changed HOST.<br>
<pre><code>#MySQL:<br>
DATABASES = {<br>
    'default': {<br>
        'ENGINE': 'django.db.backends.mysql',<br>
        'NAME': 'botsdb',<br>
        'USER': 'bots',<br>
        'PASSWORD': 'botsbots',<br>
        'HOST': 'localhost',  #database is on same server as Bots<br>
        'PORT': '3306',<br>
        'OPTIONS': {'use_unicode':True,'charset':'utf8','init_command': 'SET storage_engine=INNODB'},<br>
        }<br>
    }<br>
</code></pre>
</li><li>Create the required tables from a command prompt. Django asks for name etc of superuser. (enter user: bots, password: botsbots)<br>
<pre><code>&gt; D:\python27\python.exe D:\Python27\lib\site-packages\django\bin\django-admin.py syncdb <br>
  --settings=bots.config.settings<br>
<br>
Creating tables ...<br>
Creating table auth_permission<br>
Creating table auth_group_permissions<br>
Creating table auth_group<br>
Creating table auth_user_user_permissions<br>
Creating table auth_user_groups<br>
Creating table auth_user<br>
Creating table auth_message<br>
Creating table django_content_type<br>
Creating table django_session<br>
Creating table django_admin_log<br>
Creating table confirmrule<br>
Creating table ccodetrigger<br>
Creating table ccode<br>
Creating table channel<br>
Creating table partnergroup<br>
Creating table partner<br>
Creating table chanpar<br>
Creating table translate<br>
Creating table routes<br>
Creating table filereport<br>
Creating table mutex<br>
Creating table persist<br>
Creating table report<br>
Creating table ta<br>
Creating table uniek<br>
<br>
You just installed Django's auth system, which means you don't have any superusers defined.<br>
Would you like to create one now? (yes/no): yes<br>
Username (Leave blank to use 'mike'): bots<br>
E-mail address: bots@bots.com<br>
Password: botsbots<br>
Password (again): botsbots<br>
Superuser created successfully.<br>
Installing custom SQL ...<br>
Installing indexes ...<br>
No fixtures found.<br>
</code></pre>
</li><li>Now start bots-webserver and log in as bots.</li></ol>

Note: The database is stored in C:/ProgramData/MySQL/MySQL Server 5.5/Data/ by default (on Windows 7).<br>
To move the database, do the following:<br>
<ol><li>Stop the MySQL service<br>
</li><li>Move the /Data/ folder only to your required location (eg. D:/MySQL Server 5.5/Data/<br>
</li><li>Make sure the permissions are moved with it. "NETWORK SERVCE" must have full control<br>
</li><li>Change the setting "datadir" in C:/ProgramData/MySQL/MySQL Server 5.5/my.ini to indicate the new folder location<br>
<pre><code># Path to the database root<br>
datadir=D:/MySQL Server 5.6/Data<br>
</code></pre>
</li><li>Restart the MySQL service. If it will not start, check permissions!