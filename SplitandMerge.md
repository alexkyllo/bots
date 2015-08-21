# Splitting and merging edi files #

## Introduction ##
It would be easiest if one edi-file always contains one message (eg one order). But this is not always the case, eg:
  * in edifact or x12 traditionally multiple messages are 'enveloped'. (there was a time this was less expensive to send over networks). For some VAN's this is still true.
  * use of multiple envelopes in a file. Maybe they shouldn't do this, but they do.
  * the export routine of your ERP software puts all exported invoices in one file
So Bots has to split up edi-files, and has to be able to envelope and merge edi-files.<br>
This wiki page gives an overview of all the possible splitting and merging in Bots.<br>
<br>
<br>
<h2>Splitting</h2>
<ul><li>Incoming email: different attachments are saved as a separate edi-files.<br>
</li><li>Receiving zipped edi files: the files in the zip-file as saved as separate edi-files.<br>
</li><li>For edifact, x12, tradacoms: interchanges are being split up to separate files.<br>
</li><li>Incoming edi-files are being fed to the mapping-script as messages. This is done  by 'nextmessage' in the grammar syntax, see <a href='GrammarsNextmessage.md'>Nextmessage</a>.<br>
</li><li>Spit within a mapping script. Think of eg splitting up a shipment to the different orders. There are 2 ways of doing this:<br>
<ol><li>Write multiple message to the same file .<br>
</li><li>Write each generated message to the same file, using alt translations.</li></ol></li></ul>

<h2>Merging</h2>
<ul><li>Merging: if the 'merge' parameter is set in the syntax of the outgoing message, bots will try to merge the seperate messages to one fiel. Messages are only merged if: same from-partner, same to-partner, same editype, same messagetype, same testindicator, same characterset, same envelope.<br>
</li><li>Enveloping: (edifact, x12, tradacoms) bots will envelope these messages (add UNB-UNZ for edifact, ISA-GS-GE-IEA for x12). Enveloping is independent from merging: bots can envelope without merging, or merge without enveloping.<br>
</li><li>Write to a message-queue in outgoing channel: if you use a fixed filename in an outgoing channel, bots will append all messages to this file. This is often used in eg a set-up where all orders go to one file containing all incoming orders in fixed file format.