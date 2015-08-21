## Characters sets, encoding and unicode ##
The good news: in general Bots handles character sets well.<br>
Incoming files are read using the character-set specified in the 'incoming' syntax, outgoing files are written using the character-set as specified in the 'outgoing' syntax. You do not need to do anything in the mapping, Bots does the character-set conversion automatically.<br>
<br>
Notes:<br>
<ul><li>Lots of information about this topic can be found on <a href='http://en.wikipedia.org/wiki/Character_encoding'>wikipedia</a>.<br>
</li><li>Information about the different character-sets in python is <a href='http://docs.python.org/2/library/codecs.html#standard-encodings'>at python site</a>.<br>
</li><li>Outgoing character sets can be set in syntax; this can be done on envelope level, messagetype level of per partner.<br>
</li><li>Sometimes character-set conversion is not possible, eg uft-8->ascii, as uft8 can contain characters not in utf8.<br>
</li><li>For edifact there is an option to do character-set mapping (eg é->e); this is also possible for x12 (bit more work).<br>
</li><li>Note that x12 can be tricky: the separators used can not be in the data. There is no good workaround for this, best way is to change the separators used.</li></ul>

<br>
<h3>Specifics of different character-sets</h3>
<ul><li>Most used in edi is ascii, iso-8859-1, uft-8 (xml!).<br>
</li><li>Most familiar is ascii. Note that ascii has only 128 characters! One character is one byte.<br>
</li><li>The extended asccii character-sets.<br>
<ul><li>One character is always one byte.<br>
</li><li>The upper 128 (above ascii) are used as special characters (eg éëè).<br>
</li><li>These different character-sets are about displaying (on screen, print etc). If the texts is in iso-8859-1, but displayed as eg IBM850 is looks 'wrong'. Note that the content is still the same, it's only the display that is different.<br>
</li><li>In general these extended ascii character-sets will not be problematic in translations, as segment ID's/tags are in ascii and one character is one byte. In Bots the content of the message will just be fetched and passed to the outgoing message. So if a iso-8859-3 is handled as iso-8859-1 that will generally not be problematic.<br>
</li><li>Examples: iso-8859-1, windows-1252, iso-8859-2, iso-8859-3, IBM850, UNOC, latin1.<br>
</li></ul></li><li>Unicode.<br>
<ul><li>Examples: utf-8, utf-16, utf-32, UCS-2<br>
</li><li>Unicode is designed at accommodate much more characters, think of eg Greek, Japanese, Chinese and Klingon characters.<br>
</li><li>One character is not one byte. (the different Unicode characters-sets use different representation schemes.<br>
</li><li>Much used is utf-8. Advantage of utf-8 is that the first 128 ascii characters are one byte; this is way uft-8 is 'upward compatible' with ascii: a file with only ascii characters is the same in ascii and uft-8.<br>
</li><li>In Microsoft environments often utf-16 and utf-32 is used.<br>
</li><li>Fixed files can not have utf-8 character-set, as one character might be more than one byte.<br>
</li></ul></li><li>EBCDIC :related to (extended) ascii: one character is one byte. There are some variations of EBCDIC (eg extended EBCDIC).</li></ul>

A nasty situation is eg when one partner sends Unicode (eg utf-8), and another sends extended ascii (eg iso-8859-1). These extended characters work quite differently: Bots has to know what character-set is used before reading them, as these character-sets are treated quite differently. Best way to solve this is to have receive these files via different route(parts). Bots does no 'guessing of character-sets', as this is not appropriate for business data.<br>
<br>
<br>
<h3>x12 incoming</h3>
Character set as in envelope is used (if not set here default value of grammar.py is used (ascii)).<br>
<br>
Some typical issues and solutions:<br>
<ul><li>if partner sends x12 as eg iso-8859-1, just specify this in the syntax of the envelope (<i>usersys/grammars/x12/x12.py</i>). Note that this is a system-wide setting, this will be used for all incoming 12. Should not be a problem, iso-8859-1 is a superset of ascii. The character-set of outgoing files should also be set to handle the extended characters. Also check your ERP software: what can it handle?<br>
</li><li>same solution works for utf-8<br>
<br>
<h3>edifact incoming</h3>
Edifact has its own character-sets: UNOA, UNOB, UNOC, etc.<br>
In default bots setup:<br>
</li><li>UNOA and UNOB have own character-set mapping in <i>usersys/charsets</i>.<br>
</li><li>other edifact character-sets are aliased in <i>config/bots.ini</i>, section charsets.<br>
</li><li>default UNOA and UNOB are not 100% strict but allow some extra characters like <CR/LF>.<br>
</li><li>there are some variations of default UNOA/UNOB in <a href='http://http://sourceforge.net/projects/bots/files/edifact%20character%20sets/'>sourceforge downloads</a>.</li></ul>

Some typical issues and solutions:<br>
<ul><li>edifact files have 'UNOA' in them, but in fact they send more (UNOC). Solution: use 'unoa_like_unoc.py' from downloads, save in  <i>usersys/charsets</i> and rename to unoa.py<br>
</li><li>partner sends UNOC character-set, but my system can only handle ascii. Solution: use 'unoa_like_unoc.py' from downloads; if you open this file you can see a character mapping (note that incoming is a different character mapping as outgoing). You can map eg incoming é->e (etcetc)<br>
</li><li>our system uses iso-8859-1, but partner can handle only UNOB. Solution: use 'unoa_like_unoc.py' from downloads; if you open this file you can see a character mapping (note that incoming is a different character mapping as outgoing). You can map eg outgoing é->e (etc etc)