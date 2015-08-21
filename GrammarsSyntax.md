## Syntax parameters ##
Syntax contains parameters that are used in reading or writing edi-files.<br>
The complete list of syntax parameters including default values is in <i>bots/grammars.py</i> (in the classes of the editypes).<br>
Syntax is a python dict (dictionary).<br>
Example of syntax parameters:<br>
<pre><code>syntax = { <br>
        'charset'                  : 'uft-8', #character set is utf-8<br>
        'checkfixedrecordtooshort' : True,    #check if fixed record is to short<br>
        'indented'                 : True,    #xml: produced indented output<br>
        'decimaal'                 : ',',     #decimal sign is ', '<br>
        }<br>
</code></pre>


<br>
<h2>Syntax parameters usage and overriding</h2>
Syntax parameters can be set at different places; these settings override (somewhat luke CSS).<br>
The order in which overriding is done:<br>
<ul><li>default values are in <i>bots/grammars.py</i> (per editype). Do not change these values!<br>
</li><li>envelope grammar (eg for x12: <i>bots/usersys/grammars/x12/x12.py</i>, for edifact: <i>bots/usersys/grammars/edifact/edifact.py</i>)<br>
</li><li>message grammar<br>
</li><li>frompartner grammar (eg in <i>bots/usersys/partners/x12/partnerID.py</i>)<br>
</li><li>topartner grammar (eg in <i>bots/usersys/partners/x12/partnerID.py</i>)</li></ul>

<h4>Example 1: edifact charset</h4>
<ul><li>default value is UNOA<br>
</li><li>value in envelope (edifact.py) is UNOA<br>
</li><li>for invoices: a description is used so the message grammar for invoices has charset UNOC<br>
</li><li>retailer ABC insists on receiving invoices as UNOA, so this is indicated in the topartner grammar.</li></ul>

<h4>Example 2: x12 element separator</h4>
<ul><li>in grammar.py: 'field_sep':'<code>*</code>' (bots default value)<br>
</li><li>in x12.py: 'field_sep':'|' (default value company uses when sending x12)<br>
</li><li>retailer ABC insists: 'field_sep':'\x07' (that is \a, or BEL)</li></ul>


<br>
<h2>List of most useful syntax parameters</h2>
<table><thead><th> <b>Parameter</b> </th><th> <b>In or out</b> </th><th> <b>Description</b> </th></thead><tbody>
<tr><td>add_crlfafterrecord_sep</td><td>Out               </td><td>put <b>extra</b> character after a record/segment separator. Value: string, typically '\n' or '\r\n'. I use this for x12/edifact while testing: output is better to read. Most partenrs can handles these file, but they are slightly bigger. See also parameter 'indent'.</td></tr>
<tr><td>acceptspaceinnumfield</td><td>In                </td><td>Do not raise error when numeric field contains only spaces but assume value is 0</td></tr>
<tr><td>allow_lastrecordnotclosedproperly</td><td>In                </td><td>(csv) allows last record not to have record separator</td></tr>
<tr><td>charset           </td><td>In                </td><td>charset to use; (edifact, xml) is overridden by charset-declaration in content.</td></tr>
<tr><td>                  </td><td>Out               </td><td>charset to use in output. Bots is quite strict in this.</td></tr>
<tr><td>checkcharsetin    </td><td>In                </td><td>what to do for chars not in charset. Possible values 'strict' (gives error) or 'ignore' (skip the characters not in the charset)  or 'botsreplace' (replace with char as set in bots.ini; default is space)</td></tr>
<tr><td>checkcharsetout   </td><td>Out               </td><td>what to do for chars not in charset. Possible values 'strict' (gives error),  'ignore' (skip the characters not in the charset) or 'botsreplace' (replace with char as set in bots.ini; default is space)</td></tr>
<tr><td>checkfixedrecordtoolong</td><td>In                </td><td>(fixed): warn if record too long. Possible values: True/False, default: True</td></tr>
<tr><td>checkfixedrecordtooshort</td><td>In                </td><td>(fixed): warn if record too short. Possible values: True/False, default: False</td></tr>
<tr><td>checkunknownentities</td><td>In/out            </td><td>(xml,JSON) skip unknown attributes/elements (instead of raising an error)</td></tr>
<tr><td>contenttype       </td><td>Out               </td><td>content-type of translated file; used as mime-envelope of email</td></tr>
<tr><td>decimaal          </td><td>In/Out            </td><td>decimal point; default is '.'. For edifact: read from UNA-string if present.</td></tr>
<tr><td>endrecordID       </td><td>In                </td><td>(fixed) end position of record ID; value: number, default 3. See startrecordID</td></tr>
<tr><td>envelope          </td><td>Out               </td><td>envelope to use; if nothing specified: no envelope - files are just copied/appended. For csv output, use the value 'csvheader' to include a header line with field names.</td></tr>
<tr><td>envelope-template </td><td>Out               </td><td>(template/html) the template for the envelope.</td></tr>
<tr><td>escape            </td><td>In/out            </td><td>escape character used. Default: edifact: '?'.</td></tr>
<tr><td>field_sep         </td><td>In/out            </td><td>field separator. Default: edifact: '+'; csv: ':'  x12: '<b>')</b></td></tr>
<tr><td>forcequote        </td><td>Out               </td><td>(csv) Possible values: 1 (quote only if necessary); 1 (always quote), 2 (quote only alfanum). Default is 1 </td></tr>
<tr><td>forceUNA          </td><td>Out               </td><td>(edifact) Always use UNA-segment in header, even if not needed. Possible values: True, False. Default: False.</td></tr>
<tr><td>indented          </td><td>Out               </td><td>(xml, json) Indent message for human readability. Nice while testing. Indented messages are syntactically OK, but are much bigger. Possible values: True, False. Default: False. See also add_crlfafterrecord_sep</td></tr>
<tr><td>merge             </td><td>Out               </td><td>if merge is True: merge translated messages to one file (for same sender, receiver, messagetype, channel, etc). Related: envelope. Possible values: True, False.</td></tr>
<tr><td>namespace_prefixes</td><td>Out               </td><td>(xml) to over-ride default namespace prefixes (ns0, ns1 etc) for outgoing xml. is a list, consisting of tuples, each tuple consists of prefix and uri. Example: 'namespace_prefixes':[('orders','<a href='http://www.company.com/EDIOrders'>http://www.company.com/EDIOrders</a>'),]</td></tr>
<tr><td>noBOTSID          </td><td>In/Out            </td><td>(csv) use if records contain no real record ID.</td></tr>
<tr><td>output            </td><td>Out               </td><td>(template) values: 'xhtml-strict'</td></tr>
<tr><td>pass_all          </td><td>In                </td><td>(csv, fixed) if only one recordtype and no nextmessageblock; False: pass record for record to mapping; True: Pass all records to mapping.</td></tr>
<tr><td>quote_char        </td><td>In/Out            </td><td>(csv) char used as quote symbol</td></tr>
<tr><td>record_sep        </td><td>In/out            </td><td>char used as record separator. Defaults: edifact: ''' (single quote);  fixed:  '\n'; x12: '~'</td></tr>
<tr><td>record_sep        </td><td>In/out            </td><td>char used as record separator. Defaults: edifact: ''' (single quote);  fixed:  '\n'; x12: '~'</td></tr>
<tr><td>record_tag_sep    </td><td>Out               </td><td>(tradacoms) separator used after segment tag. Defaults: '='</td></tr>
<tr><td>replacechar       </td><td>Out               </td><td>(x12) if a separator value is found in the data, replace with this character. Default: '' (raise error when separator value in data).</td></tr>
<tr><td>skip_char         </td><td>In                </td><td>char(s) to skip, not interpreted when reading file. Typically '\n' in edifact.</td></tr>
<tr><td>skip_firstline    </td><td>In                </td><td>(csv) skip first line (often contains field names). Possible values: True/False/Integer number of lines to skip, default: False. True skips 1 line.</td></tr>
<tr><td>startrecordID     </td><td>In                </td><td>(fixed) start position of record ID; value: number, default 0. See endrecordID</td></tr>
<tr><td>template          </td><td>Out               </td><td>(template) Template to use for HTML-output.</td></tr>
<tr><td>triad             </td><td>In                </td><td>triad (thousands) symbol used (e.g. '1,000,048.35'). If specified, this symbol is skipped when parsing numbers. By default numbers are expected to come without thousands separators.</td></tr>
<tr><td>version           </td><td>Out               </td><td>(edifact,x12) version of standard generate. Value: string, typically: '3' in edifact or '004010' for x12.</td></tr>
<tr><td>wrap_length       </td><td>Out               </td><td>Wraps the output to a new line when it exceeds this length. value: number, default 0. Typically used in conjunction with 'add_crlfafterrecord_sep':'' (blank). Note: does not affect envelope of message.</td></tr>