.. _transition_to_pydicom1:

=========================
Transition to pydicom 1.x
=========================

.. rubric:: Important information on differences in pydicom post 1.0 vs pre-1.0

Introduction
============

As is often the case for major software version number changes, pydicom 1.0 breaks with the 
previous release of pydicom (0.9.9) in several ways.  These require changes to user code 
to target the pydicom >= 1.0 package, or to check and deal with the differences between
the versions.

Backwards-compatible changes post 1.0
  * the library is no longer ``dicom`` but is ``pydicom``, to match the package name 
  * short-form names such as ``Beams`` are no longer allowed;  use the full keyword e.g. ``BeamSequence``
  * some less-used modules within pydicom have been renamed, e.g. ``dicom.UID`` is now ``pydicom.uid``
  
Why was the package name changed?  There are several reasons for this change:

  * it is standard python practice for the package and the installed library to have the same name
  * first-time users expect to be able to type ``import pydicom`` rather than ``import dicom``, which has caused confusion
  * it makes sense for search engines - with the correct name it is much easier to find relevant questions and example code online
  
The decision wasn't taken lightly, but with a great deal of discussion on the github issues list.  Having made the leap,
the rest of this guide should help smooth the way...

For authors of packages requiring pydicom < 1.0
===============================================
The old pydicom releases have been split off into their own package, called ``dicom``, which is now hosted on PyPI. This allows the old library ``dicom`` to co-exist alongside the new library ``pydicom``.

The main things to do, to ensure your old pydicom code will remain functional, are:
   
   (a) you should ``pip uninstall pydicom`` and ``pip install dicom`` in your existing pydicom installs
   (b) If you have ``requirements.txt`` files, change the pydicom line from "pydicom" to "dicom"
     e.g. 
       ``pydicom==0.9.9``
     becomes
       ``dicom==0.9.9``
   (c) Change your instructions to users to ``pip install dicom`` rather than ``pip install pydicom``


Error messages relating to the pydicom transition
=================================================
This section is here in the hopes of people getting directed to this page on searches.  If that's you,
then welcome!  Hopefully the information here can get things going quickly for you.

For those with pydicom < 1.0 installed, on trying to import pydicom, they will get an ImportError message:

    >>> import pydicom
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    ImportError: No module named pydicom
    >>>
    
Your choice then is to update to pydicom >=1.0 (see Installing pydicom section), or to instead
use ``import dicom`` and follow old-style pydicom syntax.

Conversely, if pydicom >= 1.0 is installed, the error message for ``import dicom`` will look like:

    >>> import dicom
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    ImportError: No module named dicom
    >>> 

In this case you likely have installed pydicom >= 1.0, and so ``dicom`` library does
not exist.  You can simply ``import pydicom`` instead, and continue with the new pydicom, or, 
if you really need the old pydicom, then you should:

  pip install dicom
  
and you should be good to go.
  
