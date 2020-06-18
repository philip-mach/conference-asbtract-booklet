#  Conversion of spreadsheet of abstracts to abstracts booklet [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/philip-mach/conference-asbtract-booklet/master?filepath=./Conference-Abstract-Booklet.ipynb)

## Philip Machanick
### 18 June 2020

Free to use under terms of the MIT license: https://opensource.org/licenses/MIT – copyright &copy; Philip Machanick 2020

Assume an abstract booklet is in a spreadsheet structured as follows (“|” separates fields):

`\# | track # | track name | title | authors | submitted | last updated | form fields | keywords | decision | notified |	reviews sent | abstract`

as created by EasyChair; assume also that all are accepted -- though it would be easy enough to process the decision field.

A trick to make it all work: added additional fields for conference day and time. The time field is in text mode to avoid having to do conversion to Numpy time format. You should sort the spreadsheet in order of the date and time to get the abstracts in the correct order; this code does not do so.

It is worth checking for stray hyphens as some authors copy and paste from the PDF of their paper’s abstract and don’t notice that they have left in hyphens that should only be there for a line break.

Note also that LaTeX in Unicode (UTF-8) mode should be able handle extended character sets but something can be lost in translation – e.g., saving a text file may not reliably record the character set mode. To be safe, in the Excel file systematically change all:

* “ –> `` (open single quote)
* ” –> '' (close double quote)
* ‘ –> ` (open single quote)
* ’ –> ' (close single quote)
* – –> -- (end dash)
* — –> --- (em dash)
* ﬁ –> fi (fi ligature)
* ﬂ –> fl (fl ligature)
* ﬀ –> ff (fl ligature) … and others like that

Accented characters should also be searched for and replaced: a table of them can be found here: https://en.wikibooks.org/wiki/LaTeX/Special_Characters (the enclosing { } is not stricrly necessary in the main body of the document but is in BibTeX – for example, you can write \'e to get é and \'{e} should get the same result). You may also need to search for special symbols (degrees, Greek letters, mathematical notation, etc.).

This could be coded easily in Python (see use of replace in the code below) but the benefit of doing it in the spreadsheet is you would be more inclined to check. To be sure you do this right, copy and past the before and after characters into the Excel search and replace box.

LaTeX template based on https://www.overleaf.com/latex/examples/a-basic-conference-abstract-booklet/tkjfcvzgjrnd

Note: if position of the times on the abstracts are garbled, run LaTeX again. Possibly up to 3 times.

## Run online in a Binder
Click **launch binder** and run (it will take a while to start). If you create a LaTeX file you can delete the
notebook name from the path and find the LaTex file you created there.

## Installation
Clone (or download) the repository and use a terminal to install using 

```bash
>> git clone https://github.com/philip-mach/conference-asbtract-booklet
>> cd conference-asbtract-booklet
```

The abstract booklet builder requires:

- Jupyter Notebook
- Python 3.x, including xlrd, numpy and datetime

## Data sources

A fake conference spreadsheet is included as is the LaTeX preamble in the ``data``
directory. The spreadsheet is based on one downloaded from EasyChair with
date and time columns added and sorted in order of presentation. To recreate
this format, you will need to add the date and time columns and sort.


## License
This code is released under the [MIT license](http://opensource.org/licenses/MIT). Feel
free to share.
