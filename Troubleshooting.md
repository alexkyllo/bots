## Troubleshooting FAQ ##
Answers to common problems in bots..."traps for new players". See also:
  * [Installation FAQ](StartInstallProcedure#Installation_FAQ.md)
  * [Get Bots Running FAQ](StartGetBotsRunning#FAQ.md)

<br>
<b>Files get "stuck"</b><br>
<i>Background</i>:<br>
Basically bots expects input to lead to output. When a file is 'stuck' input did not lead to output.<br>
<i>Answer</i>:<br>
Somehow the setup you made is not OK. Files go in, but nothing comes out.<br>
Often this is the problem: Have you put any <a href='RoutesComposite.md'>filtering</a> on the output of your route? (under 'Filtering for outchannel' in the route configuration).<br> Filtering allows you send only particular files via an out-channel; but a file that does not match one of the filters will end up "stuck" because Bots does not know where to send it. If you have only one outchannel, there is no need for filtering.<br>
<br>
<b>Incoming edi-files are read over and over again</b><br>
<i>Answer:</i>
In the in-channel, there is a 'remove'-option. Turn it on to have incoming files removed after reading. (it is more normal to have this on, but  turning it off is handy in development).<br>
<br>
<b>Outgoing files to sftp server result in "IOError: <code>[</code>Errno 13<code>]</code> Requested operation is not supported."</b><br>
<i>Answer:</i>
It appears that some sftp severs do not support append mode (bots default mode). In this case include {overwrite} in the channel filename specification to force write mode. See <a href='http://code.google.com/p/bots/wiki/Filenames#Output_filenames'>here</a> for output filename formatting.<br>
<br>
<b>Incoming files can be seen but are not picked up by Bots (particularly with unc paths)</b><br>
<i>Answer:</i>
This is usually a permission problem. Remember that if you are running Bots Engine as a daemon/service it may be running under a system user account. Make sure the user has rights to the folder/files, or run the engine with a special user account that does have the required rights. It is best to use the <a href='Jobqueue.md'>Jobqueue</a> so that engine runs started from the GUI also run under the special user account.<br>
<br>
<b>Error in Internet Explorer: ValueError: invalid literal for int() with base 10</b><br>
<i>Answer:</i>
This has to do with the compatibility-settings of IE (tools->compatibility view settings). Text from Microsoft: Websites that were designed for earlier versions of Internet Explorer might not display correctly in IE8, IE9, or IE10. When you turn on Compatibility View, the webpage you're viewing, as well as any other webpages within the website's domain, will be displayed as if you were using an earlier version of Internet Explorer.<br>
So: if the compatibility view is used this error occurs, else it goes OK.<br>
Solution: do not this the compatibility view in IE, or use another browser.<br>
<br>
<b>Error in Internet Explorer: DoesNotExist: report matching query does not exist.</b><br>
<i>Answer:</i>
Same problem as last question:<br>
This has to do with the compatibility-settings of IE (tools->compatibility view settings). Text from Microsoft: Websites that were designed for earlier versions of Internet Explorer might not display correctly in IE8, IE9, or IE10. When you turn on Compatibility View, the webpage you're viewing, as well as any other webpages within the website's domain, will be displayed as if you were using an earlier version of Internet Explorer.<br>
So: if the compatibility view is used this error occurs, else it goes OK.<br>
Solution: do not this the compatibility view in IE, or use another browser.<br>
<br>
<b>"root" of incoming message is empty; either split messages or use inn.getloop</b><br>
<i>Answer:</i>
This may occur with incoming files that have only one record format. Even if the whole file is one edi message, you need to use <a href='https://code.google.com/p/bots/wiki/GrammarsNextmessageblock'>nextmessageblock</a> in your incoming grammar.<br>
<br>
<b>error_perm: 502 Command not implemented.</b><br>
<i>Answer1:</i>
Some FTP-servers do no support 'APPE' command (only 'STOR').<br>
In filename use: {overwrite}<br>
Eg:<br>
<blockquote><code>OUT_{messagetype}_{datetime:%Y%m%d%H%M%S}_*{overwrite}.edi</code>
Note: this {overwrite} thing only takes care of using STOR instead of APPE. Make sure filename is unique  (use <code>*</code> !).<br>
<i>Answer2:</i>
Error occurs in communication via FTP. In channel, set the 'FTP active mode' (under FTP specfic).</blockquote>

<b>ftp server gives a timeout when writing file (connect is OK)</b><br>
<i>Answer1:</i>
In channel, set the 'FTP active mode' (under FTP specfic).