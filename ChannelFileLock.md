## Safe file writing/lockings ##

### Problem ###
  * ERP writes an in-house file; bots starts to read this before the file is completely written.
  * Bots writes file over FTP, but file is read before Bots finishes writing.
Bots provides some options in channels to handle this.

<br>
<h3>Ways to handle this</h3>
1. Tmp-part file name: bots writes a filename, than renames the file.<br>
<blockquote>Example 1. In channel: filename is "myfilename<code>_</code><code>*</code>.edi.tmp", tmp-part is ".tmp"<br>
Bots writes: "myfilename_12345.edi.tmp"<br>
Bots renames: "myfilename_12345.edi"<br>
2. System lock: use system file locks for reading or writing edi files (windows, <code>*</code>nix).<br>
3. Lock-file: Directory locking: if lock-file exists in directory, directory is locked for reading/writing. Both eader and writer should check for this.