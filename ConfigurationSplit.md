# Splitting edi files #

One edi-file can contain several edi-message. Eg:
  * one edifact file, multiple ORDERs.
  * one x12 file, multiple 850's.
  * export routine of your ERP software puts all exported invoices in one file
  * email with multiple edi-attachments

<br>
A bots mapping works best for one message (one order, one invoice).<br>
So Bots splits up edi-files:<br>
<ul><li>Incoming email: different attachments are saved as a separate edi-files.<br>
</li><li>Receiving zipped edi files: the files in the zip-file as saved as separate edi-files.<br>
</li><li>For edifact, x12, tradacoms: interchanges are being split up to separate files.<br>
</li><li>Incoming edi-files are being fed to the mapping-script as messages. This is done  by 'nextmessage' in the grammar syntax, see <a href='GrammarsNextmessage.md'>Nextmessage</a>.<br>
</li><li>Spit within a mapping script. Think of eg splitting up a shipment to the different orders. There are 2 ways of doing this:<br>
<ol><li>Write multiple message to the same file .<br>
</li><li>Write each generated message to the same file, using alt translations.