#  Conversion of spreadsheet of abstracts to abstracts booklet [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/philip-mach/conference-asbtract-booklet/master?filepath=./Conference-Abstract-Booklet.ipynb)

## Philip Machanick
### 18 June 2020

Free to use under terms of the MIT license: https://opensource.org/licenses/MIT – copyright &copy; Philip Machanick 2020

## Input

Assume data to create an abstract booklet is in a spreadsheet structured as follows (“|” separates fields):

`\# | track # | track name | title | authors | submitted | last updated | form fields | keywords | decision | notified |	reviews sent | abstract | day | time`

as created by EasyChair but with the addition of fields for conference `day` and `time`. You also need to sort in order of presentation.

Only those with exact text “`accept`” in the decision field are included.

## Output
Output is a LaTeX file; to access it, use the **File** menu and select *Open* – the file name is as set in the initialization code in the cell that starts with the comment
`# setup for this conference`
(variable `texfile`).

You can also send the output to the screen by making the file name the empty string. See the comment line starting with
`# if you want the final LaTeX to go to a file`

Save the file locally if running off the repository: binders time out relatively quickly.

## Usage hints
The time field is in text mode to avoid having to do conversion to Numpy time format. You should sort the spreadsheet in order of the date and time to get the abstracts in the correct order; this code does not do so.

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

Note: if position of the times on the abstracts are garbled, run LaTeX again (up to three runs may be required).

### Source
LaTeX template based on https://www.overleaf.com/latex/examples/a-basic-conference-abstract-booklet/tkjfcvzgjrnd
