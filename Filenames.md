# Filenames #
In a perfect world, filenames are unimportant in the EDI flow. All that is required is that they are unique so no file is ever overwritten. Bots takes care of this automatically by default when creating files, by using counters to generate unique numeric filenames.

But sometimes in the "real world" implementation of system interfaces, you want or need to have specific filenames:
  * because your trading partner requires it
  * limitations of other systems regarding filenames
  * to provide easy identification of files
  * nicer for end users (eg. when emailing attachments)

<br>
<h3>Input filenames</h3>
Bots uses <a href='http://docs.python.org/library/fnmatch.html#module-fnmatch'>filename pattern matching</a> to select input files. This allows you to select all files, or only specific files, from the channel path. Some points to consider:<br>
<ul><li>Many types of channel (eg. ftp) are case sensitive. <code>*</code>.TXT is not the same as <code>*</code>.txt<br>
</li><li>Files with and without extensions may be treated differently; <code>*</code> is not the same as <code>*</code>.<code>*</code>
</li><li>for "safety" you should use a partially specified name if possible. This prevents accidentally picking up files that should not be there. eg. use ORDER<code>*</code>.TXT rather than <code>*</code>.<code>*</code>
For an in-channel with type=file a wild-card can be used in the path.<br>
If directory structure is like this:<br>
- botssys/infile/partner1<br>
- botssys/infile/partner2<br>
- botssys/infile/partner3<br>
use path botssys/infile/<code>*</code> to read the files in all these directories.<br></li></ul>



<br>
<h3>Output filenames</h3>
<ul><li>A unique name can  be generated with an asterisk; the asterisk is replaced by an unique number. Eg: order<code>_*</code>.edi -> order1.edi, order2.edi, order3.edi etc<br>
</li><li>(bots > = 3.0) Any <b>ta</b> value can be used; eg. `{botskey}, {alt}, {editype}, {messagetype}, {frompartner}, {topartner}, {fromchannel}, {tochannel}, {idroute}.<br>
</li><li>(bots > = 3.0) Date/time using <code>{datetime}</code> with any valid <a href='http://docs.python.org/library/time.html#time.strftime'>date or time format</a> specification; eg. <code>{datetime:%Y%m%d}, {datetime:%H%M%S}</code> etc.<br>
</li><li>(bots > = 3.0) Incoming filename can be used (name and extension, or either part separately); eg. <code>{infile}, {infile:name}, {infile:ext}</code>
</li><li><b>Warning:</b> Do not change out.ta_info['filename'] in your scripts. Although it may appear to work, it messes up Bots internal file storage.</li></ul>

<ul><li>Some examples are shown in the table below.</li></ul>

<table><thead><th> <b>Channel filename</b> </th><th> <b>Description</b> </th><th> <b>Example filename generated</b> </th></thead><tbody>
<tr><td><code>*</code> or blank  </td><td>create a unique name, no extension</td><td><code>39724</code>                 </td></tr>
<tr><td><code>*.txt</code>       </td><td>create a unique name with .txt extension</td><td><code>39724.txt</code>             </td></tr>
<tr><td><code>{botskey}.txt</code></td><td>use incoming <a href='ConfigurationBotskey.md'>botskey</a> value (eg. order number) with .txt extension. Note: {botskey} can only be used if merge is False for the messagetype</td><td><code>BA7358-0.txt</code>          </td></tr>
<tr><td><code>{infile}</code>    </td><td>passthrough incoming filename & extension to output</td><td><code>Order001.edi</code>          </td></tr>
<tr><td><code>{infile:name}.txt</code></td><td>passthrough incoming filename but change extension to .txt</td><td><code>Order001.txt</code>          </td></tr>
<tr><td><code>{editype}_{messagetype}_{datetime:%Y%m%d}_*.{infile:ext}</code></td><td>use editype, messagetype, date and unique number with extension from the incoming file</td><td><code>edifact_ORDERSD93AUN_20120926_39724.edi</code></td></tr>
<tr><td><code>{frompartner}/{editype}/{infile}</code></td><td>You can also use subdirectories in the filename, but they must already exist. These will be appended to the path.</td><td><code>KMART/edifact/Order001.edi</code></td></tr>
<tr><td><code>{frompartner}/INPUT/ORDER_{botskey}.csv</code></td><td>Fixed values can also be included as part of the directory structure or filename</td><td><code>KMART/INPUT/ORDER_BA7358-0.csv</code></td></tr>
<tr><td><code>{overwrite}daily_report.txt</code></td><td>Force overwriting of a file if it exists. <b>Use this with caution; make sure it is really what you want!</b> May be required on some sftp servers that do not support append mode.</td><td><code>daily_report.txt</code>      </td></tr>
<tr><td><code>{infile[4]}{infile[5]}{infile[6]}{infile[7]}.xml</code></td><td>This functionality uses the Python <a href='http://docs.python.org/2/library/string.html#formatstrings'>Format String Syntax</a> which does not have support for "slicing", but you can use this workaround to pick a range of single characters. <b>Beware: this does not check for wrong string positions.</b> </td><td>infile: <code>INV_7389.txt</code> generates: <code>7389.xml</code></td></tr></tbody></table>

<br>
<h3>User scripting for output filenames</h3>
Bots has the capability to set output filenames with a <a href='ChannelsScripting.md'>communicationscript</a>; however this requires a new script for each channel and is somewhat complex. Prior to version 3.0 this was the only method available. It can still be used for difficult requirements (but let us know about your needs through the mailing list, we may be able to integrate it).