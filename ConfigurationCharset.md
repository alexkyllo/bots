## edifact character-sets (UNOA, UNOB, etc) ##

Edifact uses its own naming of character-sets.<br>
And some character-sets quite typical or old.<br>
<br>
Bots has 2 ways of supporting these edifact character-sets:<br>
<ol><li>via specific character-sets UNOA and UNOB in <i>bots/usersys/charsets</i>
</li><li>in bots.ini aliases are giving for edifact character-sets, eg: UNOC=latin1=iso8859-1</li></ol>

<br>
There are some problems with character-sets UNOA and UNOB:<br>
<ul><li>this is not always handle correct by some, eg they send UNOA with lower-case characters.<br>
</li><li>in practice often <CR/LF> is send; officially these are not in UNOA or UNOB.<br>
</li><li>etc</li></ul>

A default bots installation includes by default the UNOA and UNOB character set. These are not strict interpreted, but 'tuned to reality', so that they will not often lead to problems.<br>
In the download 'charsetvariations' on <a href='http://sourceforge.net/projects/bots/files/grammars/edifact%20grammars/'>sourceforge site</a> are some variations on these character-sets (stricter, less strict). Read the comments in these files first.<br>
<br>
