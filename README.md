CommcareTranslationChecker
==========================

https://github.com/dimagi/CommcareTranslationChecker

A command-line tool (and Python library) to check multiple columns of a [Bulk Translation File](https://confluence.dimagi.com/display/commcarepublic/Form+Bulk+Translation) against each other, to ensure that output value tags are being used consistently between columns.

Installation
--------------------------

0a\. Install Python and `pip`. This tool is tested with Python 2.7, and 3.6.

1\. Install CommCare Translation Checker via `pip`

```
$ pip install CommcareTranslationChecker
```


Basic Command-line Usage
------------------------

The basic usage of the command-line tool is with a saved Excel file. This can either be configured for [Form Translation](https://confluence.dimagi.com/display/commcarepublic/Form+Bulk+Translation) or [Application Translation](https://confluence.dimagi.com/display/commcarepublic/Bulk+Application+Translations)

```
$ CommcareTranslationChecker    --file <relative or absolute path to translation file>
```

By default, this will read the specified file, and check all columns whose names start with "default_" against the left-most "default_" column. If any discrepancies are found between the list of "output value" tags in any of the columns, a file will be generated in the folder "commcareTranslationChecker_output." If no such folder exists relative to the current path, it will be created. This file will be an exact copy of the data in the input file, with an additional column "mismatchFlag" appended to each sheet. This column will be flagged "Y" in all rows for which a disprepancy was detected, and "N" otherwise. In addition, all cells whose "output value" tags differ from the left-most column's will be red-filled, for easy visual reference.

After the file has been created, a summary will be printed outlining how many rows were found to have discrepancies per sheet.


Advanced Command-line Usage
---------------------------
In addition to the basic usage outlined, there are a number of optional parameters that will provide a more customized experience.

```
$ CommcareTranslationChecker    --file <relative or absolute path to translation file> \
                                --columns <comma-separated list of column names to check> \
                                --base-column <name of column to be compared against, if different from left-most> \
                                --output-folder <relative or absolute path to folder in which to save output file> \
                                --ignore-order \
                                --verbose \
                                --no-output-file \

                                
```

The three options that do not include an input parameter are described below:
* **--ignore-order** If passed, the order in which output value tags appear will not be considered when comparing cells against each other. This is useful if the order of the output value tags is different between columns because of differences in word orders between the languages involved.
* **--verbose** If passed, output will be printed to the screen pointing out which rows of the file have issues.
* **--no-output-file** If passed, no output file will be created.

See `CommcareTranslationChecker --help` for the full list of options.



Release process
---------------

1\. Create a tag for the release

```
$ git tag -a "X.YY.0" -m "Release X.YY.0"
$ git push --tags
```

2\. Create the source distribution

Ensure that the archive has the correct version number (matching the tag name).
```
$ python setup.py sdist
```

3\. Upload to pypi

```
$ pip install twine
$ twine upload dist/CommcareTranslationChecker-X.YY.0.tar.gz
```

4\. Verify upload

https://pypi.python.org/pypi/CommcareTranslationChecker

5\. Create a release on github

https://github.com/dimagi/CommcareTranslationChecker/releases