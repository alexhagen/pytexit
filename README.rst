
.. image:: https://readthedocs.org/projects/pytexit/badge/
    :target: https://pytexit.readthedocs.io/en/latest/?badge=latest
    :alt: Documentation Status
  
.. image:: https://img.shields.io/pypi/v/pytexit.svg
    :target: https://pypi.python.org/pypi/pytexit
    :alt: PyPI
    
.. image:: https://img.shields.io/travis/erwanp/pytexit.svg
    :target: https://travis-ci.org/erwanp/pytexit
    :alt: Tests

.. image:: https://codecov.io/gh/erwanp/pytexit/branch/master/graph/badge.svg
    :target: https://codecov.io/gh/erwanp/pytexit
    :alt: Coverage

=======
pytexit
=======

Convert a Python expression in a LaTeX formula

Install
-------

``pytexit`` is on PyPi::

    pip install pytexit

	
Use
---

``pytexit`` features the :func:`~pytexit.pytexit.py2tex`, :func:`~pytexit.pytexit.for2tex`
and :func:`~pytexit.core.fortran.for2py` functions.

In a Terminal, use ``py2tex``::

    py2tex 'x = 2*sqrt(2*pi*k*T_e/m_e)*(DeltaE/(k*T_e))**2*a_0**2'

In a Python console, use :func:`~pytexit.pytexit.py2tex`::

    from pytexit import py2tex
    py2tex('x = 2*sqrt(2*pi*k*T_e/m_e)*(DeltaE/(k*T_e))**2*a_0**2')

returns the corresponding LaTeX formula (to re-use in papers)::

    $$x=2\\sqrt{\\frac{2\\pi k T_e}{m_e}} \\left(\\frac{\\Delta E}{k T_e}\\right)^2 a_0^2$$
    
and (in ipython console only) prints the equation:

.. image:: https://github.com/erwanp/pytexit/blob/master/docs/output.png

	
Notes
-----
	
This module isn't unit aware and isn't designed to perform calculations. It is 
a mere translator from Python expressions into LaTeX syntax. The idea behind it
was I wanted my Python formula to be the same objects as the LaTeX formula I 
write in my reports / papers. It allows me to gain time (I can write my LaTeX 
formulas directly from the Python expression), and check my Python formulas are correct
(once printed LaTeX is much more readable that a multiline Python expression)


``pytexit`` can also convert FORTRAN formulas to Python (:func:`~pytexit.for2py`) 
and LaTeX (:func:`~pytexit.for2tex`)::

	from pytexit import for2tex
	for2tex(r'2.8d-11 * exp(-(26500 - 0.5 * 1.97 * 11600 )/Tgas)')

Finally, ``pytexit`` output can be made compatible with Word equation editor with 
the ``output='word'`` option of :func:`~pytexit.pytexit.py2tex`::

	from pytexit import py2tex
	py2tex(r'2*sqrt(2*pi*k*T_e/m_e)*(DeltaE/(k*T_e))**2*a_0**2', output='word')
	
The latest output will typically replace all brackets {} with parenthesis () that are correctly
interpreted by Word, and keep keywords that are correctly evaluated by Word (`\pi` or `\cdot`) 


References
----------

Based on a code sample from Geoff Reedy on `StackOverflow <http://stackoverflow.com/questions/3867028/converting-a-python-numeric-expression-to-latex>`__


You may also be interested in the similar development from `BekeJ <https://github.com/BekeJ/py2tex>`__ that was built
on top of the same sample. 
BekeJ's code is designed to be used exclusively in an iPython console using 
%magic commands to perform unit aware calculations and return result in a nice
LaTeX format. 

Sympy also has some nice LaTeX output, but it requires declaring your symbolic
variables and isn't as fast as a one-line console command in pytexit.

Current Features
----------------

Successfully deal with most of the one or two parameter functions. Run the 
_test() function to have an idea of what's possible. 

Arbitrary syntax:

- Variables named after Greek names are turned into LaTeX syntax

- 'numpy.sin / math.sin / np.sin' syntax still work as expected (all standard 
  scientific module names are removed beforehand)

- quad() is converted into integrals

- list comprehensions are converted into LaTex syntaX. 

- 'a_p' variables are converted with "p" as subscript

Also note that iPython uses auto-completion to convert most of the latex 
identifiers in their Unicode equivalent::

    \alpha --> [Tab] --> α
    
- pytexit will recognize those Unicode characters and convert them again in 
  latex expressions

- there is a mode to output Python expressions in Word syntax. From version 2007
  Word converts most LaTeX expressions in its own graphical representation. The 
  Word mode here was just about replacing those LaTeX {} with Word ()::

    py2tex('sqrt(5/3)',output='word')


Test
----

In order to enforce cross-version compatibility and non-regression, `pytexit` is 
now tested with `pytest` and Travis. Run the test suite locally from a terminal with::

    pip install pytest 
    pytest 


Changes
-------

- 0.2.1 : full Python 2 support, added automated tests with pytest and Travis

- 0.1.11 : make it reliable: added pytest, Travis, code coverage

- 0.1.8 : fixed console script on Unix systems

- 0.1.4 : partial Python 2 support


Still WIP
---------

Todo:

- allow syntax "a*b = c" (not a valid Python expression, but convenient to type 
  some LaTeX formula)
    
- code for numbered equations

- export all the conversions on an external text file 
    
	
Links
-----

- Github: https://github.com/erwanp/pytexit
- Documentation: https://pytexit.readthedocs.io
    