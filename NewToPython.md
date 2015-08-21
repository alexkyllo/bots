## Some tips when you are new to python ##

### Short Explanation ###
  * Python is an interpreted language. This means for you: edit a python source file (eg mappingscript, grammar), save it and run again. No compilation, no linking.
  * Python source files always have extension '.py'.
  * If you see a '.pyc' file: that is an intermediate file. OK, python does some compilation automatically. Never mind, it is not important. Some systems have '.pyo' files instead. Again, not important.
  * Python does not use curly braces ('{...}') or 'BEGIN...END' for functions, loops etc. Python uses 'indentation' instead. Some people love it, some hate it. For me: this is what I always did with all programming languages; now everybody uses the same layout ;-))
  * Links to more learning about python are in the [page with external links](Links.md)


### Tips ###
  1. Use a good text editor. This is VERY important. It saves you a lot of time. See [in tools page](UsefulTools.md). Three main reasons:
    * a good editor has a feature called 'syntax highlighting'. This makes it is lot easier to work with eg mapping scripts.
    * a good editor can do a python syntax check on the python source file (a check if it is valid python). This will point you directly to any errors you made.
    * make the editor use spaces instead of tabs. This is an important feature when working with python. Never mix tabs and spaces.
  1. Creating grammars and mapping scripts does not require an "in depth" knowledge of Python, but you need to at least understand general principles of:
    * [variables and expressions](http://www.greenteapress.com/thinkpython/html/thinkpython003.html)
    * [functions](http://www.greenteapress.com/thinkpython/html/thinkpython004.html)
    * [strings](http://www.greenteapress.com/thinkpython/html/thinkpython009.html)
    * [lists](http://www.greenteapress.com/thinkpython/html/thinkpython011.html), [dicts](http://www.greenteapress.com/thinkpython/html/thinkpython012.html) and [tuples](http://www.greenteapress.com/thinkpython/html/thinkpython013.html)
  1. Start with a plugin or example
    * most grammars are "similar" (csv, fixed are simple; edifact, x12 are more complex)
    * most mappings are "similar" (same functions are used, only "mpaths" change)
    * find something close to what you need, see how it works, adapt it.


### Installing extra libraries/dependencies ###
  * For linux lots of [information about installing libraries is here](StartInstalllinux.md). Think this is also useful for windows.
  * A advanced method is [using virtualenv](DeploymentMultipleEnvironmentsVirtual.md)

### Feedback ###
Please share your experiences and tips via the [mailing list](http://groups.google.com/forum/#!forum/botsmail)!