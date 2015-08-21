# Mapping recipes #

<br>
<h2>multiple messages in an edi-file, not split up</h2>
(a grammar without nextmessage)<br>
<ul><li>Using inn.get() gives an error: that "root" of incoming message is empty, etc.<br>
</li><li>You start the mapping script with getloop(); and do get() with results of getloop()</li></ul>

<br>
<h2>Csv messages consisting of only one record type</h2>
<ul><li>use nextmessageblock() to separate the messages<br>
</li><li>see plugin ...