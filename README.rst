==============
Gender Guesser
==============

.. image:: https://travis-ci.org/lead-ratings/gender-guesser.svg?branch=master
    :target: https://travis-ci.org/lead-ratings/gender-guesser


This package uses the underlying data from the program "gender" by Jorg Michael (described `here <http://www.autohotkey.com/community/viewtopic.php?t=22000>`_).  Its use is pretty straightforward::

    >>> import gender_guesser.detector as gender
    >>> d = gender.Detector()
    >>> print(d.get_gender(u"Bob"))
    male
    >>> print(d.get_gender(u"Sally"))
    female
    >>> print(d.get_gender(u"Pauley")) # should be androgynous
    andy

The result will be one of ``unknown`` (name not found), ``andy`` (androgynous), ``male``, ``female``, ``mostly_male``, or ``mostly_female``. The difference between ``andy`` and ``unknown`` is that the former is found to have the same probability to be male than to be female, while the later means that the name wasn't found in the database.

I18N is fully supported::

    >>> print(d.get_gender(u"\xc1lfr\xfan"))  # u"Álfrún"
    female

Additionally, you can give preference to specific countries::

    >>> print(d.get_gender(u"Jamie"))
    mostly_female
    >>> print(d.get_gender(u"Jamie", u'great_britain'))
    mostly_male

Additionally, you can create a detector that is not case sensitive (default *is* to be case sensitive)::

    >>> d = gender.Detector(case_sensitive=False)
    >>> print(d.get_gender(u"sally"))
    female
    >>> print(d.get_gender(u"Sally"))
    female

Try to avoid creating many Detectors, as each creation means reading the data file.

Licenses
========

The generator code is distributed under the GPLv3.  The data file nam_dict.txt is released under the GNU Free Documentation License.


Changelog
=========

0.4.0 (2016-12-05)
******************

* Fix bug where spaces in composite names were shadowing other names


0.3.0 (2016-07-02)
******************

* Remove ``unknown_value`` init option, since it can be implemented very easily with a wrapper if needed.
* Return ``unknown`` when name is not found and ``andy`` when it is valid equally for both male and female.
* Test README examples as doctests.
* Fix incorrect country-wise gender detection for non-iso886-15 names coming from line length change after data file conversion to UTF-8. See #gh2. Thanks @miquelcamprodon.


0.2.0 (2015-12-06)
******************

* Wire in ``tox`` to test in both Python 2 and Python 3.
* Python 2 and 3 compatibility.
* Remove obsolete character mapper code.

For previous versions, see `sexmachine <https://github.com/ferhatelmas/sexmachine/>`_.


Credits
=======

This is a fork of the ``SexMachine`` package by `Ferhat Elmas <https://github.com/ferhatelmas>`_. It was created to be able to publish a Python 3 compatible version to PyPI and to be able add some more improvements without bugging the original author.
