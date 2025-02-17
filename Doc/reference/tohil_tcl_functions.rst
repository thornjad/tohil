
.. tohil-tcl-functions:


Tohil Tcl Functions
======================

Once a ``package require Tohil`` has been performed
from Tcl interpreter, the following commands are available:

.. function:: tohil::call [-kwlist list] [obj.]function [arg...]

   *tohil::call* provides a way to invoke a Python function,
   with zero or more positional parameters and zero or more
   named parameters, without having to pass the parameters through
   Python's *eval* or *exec* and running the risk that Python
   metacharacters appearing in the data will cause quoting problems,
   accidental code execution, etc.

   Whatever the Python function returns is returned to Tcl.

   If *-kwlist list* is specified, *list* contains key-value pairs
   that will be passed to the function as named parameters.

.. function:: tohil::eval evalString

   *evalString* contains a valid Python expression.  Tohil
   evaluates the string using the Python interpreter and
   returns to Tcl whatever Python returned.

   If an exception is thrown and not caught by any Python code
   before getting back to Tohil, Tohil traps the exception,
   converts it into a Tcl error, and returns that error to
   the caller.

.. function:: tohil::exec

   *tohil::exec* evaluates the code passed to it, similarly to
   Python's *exec* function.  Nothing is returned.

   If the Python code prints anything, it goes to stdout using Python's
   I/O subsystem.  However you can easily redirect Python's output to go
   to a string, or whatever, in the normal Python manner.
   *tohil::run*, in fact, provides a way to do this.


.. function:: tohil::import module

   Import the specified module into the globals of the Python interpreter.

   The name of the module may be of the form module.submodule.

   You can do the same thing using *exec* and, currently, exercise
   more control, for example ``tohil::exec "from io import StringIO"``.

.. function:: tohil::interact

   We run *tohil::interact* from the Tcl command prompt to enter the Python
   interactive loop.  When we're done, we send end of file (^D) to end the
   Python loop and return to the Tcl one.


.. function:: tohil::run

   tohil::run evaluates the code passed to it as if with Python's *exec*,
   but unlike *tohil::exec*, anything emitted by the Python code to
   Python's stdout (print, etc) is captured by *tohil::run* and returned
   to the caller.
