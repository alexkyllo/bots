## Migrate to version 3.1.0 (from 3.0.0) ##

<br>
<h4>Editype x12: in ISA definition 'ISA11' has to be conditional</h4>
Bots 3.1.0 supports the repeating character (for ISA-versions >= 00403).<br>
If you use this, ISA11 has to be conditional in definition; file usersys/grammars/x12/envelope.py:<br>
was:<br>
<code>['ISA11','M',(1,1),'AN'],</code><br>
becomes in 3.1.0:<br>
<code>['ISA11','C',(1,1),'AN'],</code><br>
This change also works for older ISA-version. Advised is to use this.<br>
<br>
<br>
<h4>Editype x12, edifact, tradacoms: different handling of syntax parameters</h4>
Bots handles the syntax parameters differently. In bots 3.0 and earlier this was somewhat 'fuzzy'.<br>
This works now like:<br>
<i>default syntax parameters are overruled by envelope parameters,</i><br>
are overruled by message parameters,<br>
are overruled by frompartner parameters,<br>
are overruled by topartner parameters.<br>

Most common problem will be for x12: message grammars had by default in syntax parameters:<br>
<code>'version'    :  '00403',</code><br>
Formerly this was not used; now it is used.<br>
This might lead to sending another version of ISA-envelope, this is probably not what you want!<br>
Solution: delete (or uncomment) the 'version' syntax parameter for message grammar.<br>
<br>
Note: the ISA-version you send now is probably in usersys/grammars/x12/x12.py<br>
<br>
<br>
<h4>Editype fixed and idoc: 'startrecordID' and 'endrecordID' not longer used</h4>
Bots calculates this automatically now.<br>
Bots also checks for all used records if this is used the same over all records.<br>
This might lead to errors.<br>
Solution: BOTSID should have correct length in all records and be at correct position.<br>

<br>
<h4>Envelope scripts</h4>
was:<br>
<code>self._openoutenvelope(self.ta_info['editype'],self.ta_info['envelope'])</code><br>
becomes in 3.1.0:<br>
<code>self._openoutenvelope()</code>

<br>
<h4>Route scripting</h4>
Function transform.translate is changed:parameters startstatus,endstatus,idroute,rootidta  have to be explicitly indicated (no more defaults).