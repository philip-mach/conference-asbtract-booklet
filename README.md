#  Conversion of spreadsheet of abstracts to abstracts booklet [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/philip-mach/conference-asbtract-booklet/master?filepath=./Conference-Abstract-Booklet.ipynb)

## Philip Machanick
### 21 June 2020

Free to use under terms of the MIT license: https://opensource.org/licenses/MIT – copyright &copy; Philip Machanick 2020

You can run by clicking **launch binder** on GitHub, otherwise install as described here.

## To install
Either download the project using (on a typical Unix command line, tested on Mac OS 10.13.6):

`git clone https://github.com/philip-mach/conference-asbtract-booklet
cd conference-asbtract-booklet`

Ensure you have Python 3.x and Jupyter installed as well as the required Python dependencies (tested on Python 3.7.4):

`xlrd
numpy
datetime`

## To Run
On GitHub, click **launch binder**. It will take a while to launch as a new environment mist be configured and set up.

Once the notebook launches, in the **File** menu in the Notebook, chose **Open**. This will open a new tab or window and you can view the file system in the binder environment.

Now click on the ``data`` folder to open it then click on the **Upload** button. You can now upload the spreadsheet with your abstracts to the data folder. Once done, close the tab or folder to the data directory and edit the file name in the Notebook to match. Look for the comment:

`# setup for this conference -- all changes for a new event go here`

and edit the `filename` assignment in the next line. Also edit the other conference details below that.

To run locally on Unix command line:

To run locally, copy over the required input Excel spreadsheet to the `data` directory. Then (assuming you `cd` to the correct working directory):

`jupyter-notebook Conference-Abstract-Booklet.ipynb`

Once it opens, edit the file name and conference details as in the run in binder step.

To run the entire Notebook, click in the first cell and then click the **Run** button at the top until you have run the last cell. At this point you can go back to the 

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

You can then process it through LaTeX (or if this is not a thing you do, use [Overleaf](https://www.overleaf.com): you can create a free account, start a new project and upload the `.tex` file. Click on that file and click on **Recompile**. You can download the resulting PDF.

## Usage hints
Ensure that the time field is in text mode because this allowed me to avoid having to do conversion to Numpy time format. You should sort the spreadsheet in order of the date and time to get the abstracts in the correct order; this code does not do so.

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
