Notes:
  * Most edi files are just a few kilobyes. An edi file of 5Mb is very large (edifact, x12). If you encounter larger ones: please let me know.
  * AFAIK there are no issues with performance. If you run into this: please inform me eg via mailing list.

<br>
<h3>More performance</h3>
<ol><li>(Bots >= 2.2.0) Cdecimals (Extern library) speeds up bots. This library will be included in python 3.3, but can be installed in earlier python versions. See <a href='http://www.bytereef.org/mpdecimal/index.html'>website</a>
</li><li>(bots >= 3.1) Do not use get_checklevel=2 in config/bots.ini. This does extended checking of mpath's, use this during development only.<br>
</li><li>(bots >= 3.0) Schedule bots-engine via the <a href='Jobqueue.md'>job queue server</a>.<br>
</li><li>For xml: check if the c-version of python's elementtree is installed and used.<br>
</li><li>Enough memory is important for performance: disk-memory swapping is slow! Actual memory usage depends on size of edi-files.<br>
</li><li>Check mappings for slow/inefficient algorithms.<br>
</li><li>Bots works with [www.pypy.org pypy], see below on this page.<br>
</li><li>Use SSD for faster reading/writing. In config/bots.ini the botssys-directory can be set, in config/settings.py the place of the SQLite-database.</li></ol>


<br>
<h3>Strategy for bigger edi volumes</h3>
<ol><li>Best strategy is to <a href='DeploymentEngine.md'>schedule</a> bots-engine more often.<br>
</li><li>(bots >= 3.0) Schedule bots-engine via the <a href='Jobqueue.md'>job queue server</a>.<br>
</li><li>Routes can be <a href='DeploymentEngineOverview.md'>scheduled independently</a>.<br>
</li><li>Set-up good scheduling, keeping volumes in mind.<br>
<ul><li>edi in the real world has often large peaks.<br>
</li><li>some edi transactions are time critical (eg orders), others not so much (eg invoices)<br>
</li><li>check where the large volumes are (size and number of edi-transactions)<br>
</li><li>look at the sending pattern of your customers. Often edi is send in night jobs, so you might receive lot of volume early in the morning.<br>
</li><li>check where you send large volumes. Send this at a time that does not interfere with other flows.<br>
</li></ul></li><li>Incoming volumes can be limited per run. This way the time bots-engine runs is predictable. The max time a channel fetches incoming files is a parameter for each channel. Note: this is dependent upon the communication type used; eg file system I/O is much faster than SFTP. Files "left behind" will be fetched on subsequent runs.<br>
</li><li>(Bots >= 3.0) Limit for max file-size (set in bots.ini). If an incoming file is larger, bots will give error. This is to prevent 'accidents'.</li></ol>


<br>
<h3>Performance/throughput testing</h3>
<ol><li>Tests are done using file system I/O (no testing of communication performance).<br>
</li><li>Tests done in one run of bots-engine.<br>
</li><li>Test system: Intel Q9400 2.66GHz; 4Gb memory; ubuntu 10.04(lucid); python 2.7; default SQLite database.<br>
</li><li>Please note that these tests are 'artificial': if you have such high volumes and big files look at good scheduling!<br>
</li><li>test are with edifact; x12 performance is the same.</li></ol>

<table><thead><th> </th><th>  </th><th> </th><th> </th><th> <b>bots2.0</b> </th><th> </th><th> <b>bots2.2</b> </th><th> <b>(cdecimal)</b></th><th> <b>bots3.2</b> </th><th> </th></thead><tbody>
<tr><td> <b>description</b> </td><td> <b>#file</b> </td><td> <b>vol</b> </td><td> <b>#mess.</b> </td><td> <b>time</b>    </td><td> </td><td> <b>time</b>    </td><td>                  </td><td> <b>time</b>    </td><td> </td></tr>
<tr><td>01 edifact2fixed</td><td>32 </td><td>305Mb </td><td>32</td><td>1:01:39         </td><td>82 kb/s</td><td>0:50:57         </td><td> 100 kb/s         </td><td>0:44:01         </td><td> 115 kb/s</td></tr>
<tr><td>02 edifact2fixed</td><td>116</td><td>300Mb</td><td>116</td><td>1:14:18         </td><td>68 kb/s</td><td>0:36:20         </td><td>137 kb/s          </td><td>0:37:25         </td><td> 133 kb/s</td></tr>
<tr><td>03 edifact2fixed</td><td>94048</td><td>295Mb</td><td>141072</td><td>0:47:21         </td><td>104 kb/s </td><td>0:39:54         </td><td>125 kb/s          </td><td>0:42:30         </td><td> 115 kb/s</td></tr>
<tr><td>04 fixed2edifact</td><td>14244</td><td>300Mb</td><td>78342</td><td>1:04:11         </td><td>78 kb/s</td><td>0:33:21         </td><td>150 kb/s          </td><td>0:32:40         </td><td> 153 kb/s</td></tr>
<tr><td>05 xml2edifact</td><td>17424</td><td>300Mb</td><td>17424</td><td>0:41:24         </td><td>121 kb/s </td><td>0:35:48         </td><td>139 kb/s          </td><td>0:35:20         </td><td> 141 kb/s</td></tr>
<tr><td>06 edifact2xml(1to1)</td><td>14609</td><td>300Mb</td><td>74919</td><td>1:23:03         </td><td>60 kb/s </td><td>0:58:19         </td><td>85 kb/s           </td><td>0:44:38         </td><td> 112 kb/s </td></tr></tbody></table>

<br>
<b>Conclusions of performance measurements</b>
<ol><li>Memory usage is stable (no leakage).<br>
</li><li>Memory usage is directly related to the size of the edi-files. In test 01 (edifact files of 9.5Mb) bots-engine uses 1.5Gb memory.<br>
</li><li>Tested with edifact files of 120Mb; memory usage is stable at 4.5Gb.<br>
</li><li>Performance is reasonably independent from the size of edi-files/messages.<br>
</li><li>an edifact file of 9.5Mb takes about 85sec to be processed.<br>
</li><li>for outgoing edi files: writing to one file or multiple file does not significantly affect performance.</li></ol>

<br>
<h3>Testing with pypy</h3>
[www.pypy.org Pypy] is a python implementation that is faster by using a JIT (that is one of their achievements...).<br>
Results of the first tests with pypy (beta-versions of pypy 2.0):<br>
<ul><li>Bots works with pypy.<br>
</li><li>Comparing some stress tests: much faster, 2-3 times faster.<br>
</li><li>Did not run all test-sets. Probably I will do that with definitive version of pypy 2.0 and/or release of bots 3.1.<br>
</li><li>Problem might be that not all libraries/dependencies work with pypy.<br>
<ul><li>SQLite3 database connector: OK<br>
</li><li>MySQL database connector: version 1.2.5 does. Note that bots 3.1.0 gave am error with this version, a patch was easy.<br>
</li><li>paramiko (for SFTP/SSH): no, dependency pycrypto is not supported.<br>
This looks like a very interesting development!