## communication type 'communicationscript' ##
In this case, the channel must be configured with Type: communicationscript.<br>
In the communicationscript some functions will be called:<br>
<ul><li>connect (required)<br>
</li><li>main (optional, 'main' should handle files one by one)<br>
</li><li>disconnect  (optional)</li></ul>

Different ways of working:<br>
<ol><li>for incoming files (bots receives the files):<br>
<ul><li>connect puts all files in a directory, there is no 'main' function. bots can remove the files (if you use the 'remove' switch of the channel). See example 1.<br>
</li><li>connect only builds the connection, 'main' is a generator that passes the messages one by one (using 'yield'). bots can remove the files (if you use the 'remove' switch of the channel). See example 2.<br>
</li></ul></li><li>for outgoing files (bots sends the files):<br>
<ul><li>no 'main' function: the processing of all the files can be done in 'disconnect'. bots can remove the files (if you use the 'remove' switch of the channel). See example 3.<br>
</li><li>if there is a 'main' function: the 'main' function is called by bots after writing each file. bots can remove the files (if you use the 'remove' switch of the channel). See example 4.</li></ul></li></ol>

<br>
<h3>Example 1: incoming files via external program all at once</h3>
Calls an external program.<br>
Think eg of a specific communication module for a VAN.<br>
All files are received at once to a folder, then processed like a normal file channel.<br>
<br>
<pre><code>import subprocess<br>
<br>
def connect(channeldict,*args,**kwargs):<br>
    subprocess.call(['C:/Program files/my VAN/comms-module.exe','-receive'])<br>
</code></pre>

<br>
<h3>Example 2: incoming files via external program one by one</h3>
TODO: make a valid example using yield.<br>
main is a generator.<br>
<pre><code>import subprocess<br>
<br>
def connect(channeldict,*args,**kwargs):<br>
    ''' function does nothing but it is required.'''<br>
    pass<br>
<br>
def main(channeldict,*args,**kwargs):<br>
<br>
    yield ?<br>
<br>
</code></pre>
<br>
<h3>Example 3: outgoing files via external program all at once</h3>
Calls an external program.<br>
Think eg of a specific communication module for a VAN.<br>
In this example the 'disconnect' script is called after all files are written to directory;<br>
in disconnect all files are passed to external communication-module.<br>
<pre><code>import subprocess<br>
import os<br>
<br>
def connect(channeldict,*args,**kwargs):<br>
    ''' function does nothing but it is required.'''<br>
    pass<br>
<br>
def disconnect(channeldict,*args,**kwargs):<br>
    subprocess.call(['C:/Program files/my VAN/comms-module.exe','-send',os.path.join(channeldict['path'],'*.xml'])<br>
</code></pre>
<br>
<h3>Example 4: outgoing files via external program one by one</h3>
Calls an external program.<br>
Think eg of a specific communication module for a VAN.<br>
In this example the 'main' script is called for each outgoing file.<br>
<pre><code>import subprocess<br>
<br>
def connect(channeldict,*args,**kwargs):<br>
    ''' function does nothing but it is required.'''<br>
    pass<br>
<br>
def main(channeldict,filename,ta,*args,**kwargs):<br>
    subprocess.call(['C:/Program files/my VAN/comms-module.exe','-send',filename])<br>
</code></pre>


<br>
<h3>Example 5: outgoing files to a printer</h3>
Send data (eg. ZPL code to print fancy labels) directly to a Windows configured printer.<br>
The printer can be defined in Windows either as "Generic/Text Only" or with the<br>
proper driver, because this script just sends raw data, bypassing the driver.<br>
Dependencies: Requires pywin32<br>
Reference: <a href='http://timgolden.me.uk/pywin32-docs/win32print.html'>http://timgolden.me.uk/pywin32-docs/win32print.html</a>
<pre><code>import os<br>
import win32print<br>
import bots.transform as transform<br>
<br>
def connect(channeldict,*args,**kwargs):<br>
    ''' function does nothing but it is required.'''<br>
    pass<br>
<br>
def main(channeldict,filename,ta,*args,**kwargs):<br>
<br>
    # set printer values required<br>
    ta.synall()<br>
    printer = transform.partnerlookup(ta.topartner,'attr1')<br>
    jobname = ta.botskey<br>
<br>
    # read the output file<br>
    with open(filename,'r') as content_file:<br>
        content = content_file.read()<br>
<br>
    # send data to the printer<br>
    hPrinter = win32print.OpenPrinter(printer)<br>
    hJob = win32print.StartDocPrinter(hPrinter,1,(jobname,None,'RAW'))<br>
    win32print.WritePrinter(hPrinter,content)<br>
    win32print.EndDocPrinter(hPrinter)<br>
    win32print.ClosePrinter(hPrinter)<br>
</code></pre>