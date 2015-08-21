## Partner dependent syntax ##
For outgoing messages it is possible to specify a partner dependent syntax.<br>
This is especially useful for x12 and edifact, for setting envelope values and partner specific separators.<br>
These parameters override the settings in the message grammar; you only need to specify the partner-specific parameters.<br>
Note: no need to set partner specific separators for incoming messages; bots will figure this out by itself.<br>

To set partner specific syntax parameters, create according to editype used:<br>
<ul><li><i>bots/usersys/partners/x12/partnerid.py</i>
</li><li><i>bots/usersys/partners/edifact/partnerid.py</i></li></ul>

Example file with partner specific setting (x12):<br>
<blockquote><pre><code><br>
syntax = {<br>
'ISA05'                  : 'XX',    #use different communication qualifier for sender<br>
'ISA07'                  : 'ZZ',    #use different communication qualifier for receiver<br>
'field_sep'              : '|',     #use different field separator<br>
}<br>
</code></pre></blockquote>

Example file with partner specific setting (edifact):<br>
<blockquote><pre><code><br>
syntax = {<br>
'merge':False,<br>
'forceUNA':True,<br>
'UNB.S002.0007':'ZZ',        # partner qualifier<br>
'UNB.S003.0007':'ZZ',        # partner qualifier<br>
}<br>
</code></pre></blockquote>

<br>
<h3>Plugin</h3>
Plugin 'demo_partnerdependent' at <a href='http://sourceforge.net/projects/bots/files/plugins/'>the bots sourceforge site</a> demonstrates partner dependent syntax.<br>
<br>
<br>
<h2>Relevant x12 syntax settings</h2>
<table><thead><th> <b>Name</b> </th><th> <b>Default</b> </th><th> <b>Description</b> </th></thead><tbody>
<tr><td>ISA05        </td><td>01              </td><td>Interchange ID Sender Qualifier</td></tr>
<tr><td>ISA07        </td><td>01              </td><td>Interchange ID Receiver Qualifier</td></tr>
<tr><td>ISA15        </td><td>P               </td><td>Testindicator: P(roduction) or T(est); mostly set per message/transaction.</td></tr>
<tr><td>GS07         </td><td>X               </td><td>Responsible Agency Code</td></tr>
<tr><td>version      </td><td>00403           </td><td>As ISA12            </td></tr>
<tr><td>functionalgroup</td><td>                </td><td>As GS01; set this for each x12 messagetype</td></tr>
<tr><td>record_sep   </td><td>~               </td><td>Segment terminator. </td></tr>
<tr><td>field_sep    </td><td> <code>*</code> </td><td>                    </td></tr>
<tr><td>sfield_sep   </td><td>>               </td><td>Sub-field separator (in composites).</td></tr>
<tr><td>merge        </td><td>True            </td><td>Merge messages to envelopes (False: no merging, only envelope).</td></tr>
<tr><td>add_crlfafterrecord_sep</td><td>\r\n            </td><td>Adds CR/LF after each segment.</td></tr></tbody></table>

<br>
<h2>Relevant edifact syntax settings</h2>
<table><thead><th> <b>Name</b> </th><th> <b>Default</b> </th><th> <b>Description</b> </th></thead><tbody>
<tr><td>UNB.S002.0007</td><td>14              </td><td>Identification code qualifier</td></tr>
<tr><td>UNB.S002.0008</td><td>                </td><td>Interchange sender internal identification</td></tr>
<tr><td>UNB.S002.0042</td><td>                </td><td>Interchange sender internal sub-identification</td></tr>
<tr><td>UNB.S003.0007</td><td>14              </td><td>Identification code qualifier</td></tr>
<tr><td>UNB.S003.0014</td><td>                </td><td>Interchange recipient internal identification</td></tr>
<tr><td>UNB.S003.0046</td><td>                </td><td>Interchange recipient internal sub-identification</td></tr>
<tr><td>UNB.S005.0022</td><td>                </td><td>Recipient reference/password</td></tr>
<tr><td>UNB.S005.0025</td><td>                </td><td>Recipient reference/password qualifier</td></tr>
<tr><td>UNB.0026     </td><td>                </td><td>Application reference</td></tr>
<tr><td>UNB.0029     </td><td>                </td><td>Processing priority code</td></tr>
<tr><td>UNB.0031     </td><td>                </td><td>Acknowledgement request</td></tr>
<tr><td>UNB.0032     </td><td>                </td><td>Interchange agreement identifier (eg. EANCOM)</td></tr>
<tr><td>UNB.0035     </td><td>0               </td><td>Testindicator. Mostly set per message.</td></tr>
<tr><td>charset      </td><td>UNOA            </td><td>As S001.0001        </td></tr>
<tr><td>version      </td><td>3               </td><td>As S001.0002        </td></tr>
<tr><td>merge        </td><td>True            </td><td>Merge messages to envelopes (False: no merging, only envelope).</td></tr>
<tr><td>forceUNA     </td><td>False           </td><td>Always use UNA in outgoing edifact, even if not strictly needed.</td></tr>
<tr><td>add_crlfafterrecord_sep</td><td>\r\n            </td><td>Adds CR/LF after each segment.</td></tr>