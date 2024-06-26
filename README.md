# Installation
Once you have installed [Python](https://www.python.org/downloads/) and its packages manager [pip](https://pip.pypa.io/en/stable/installation/),
depending on if you want only this tool, the full set of PNU tools, or PNU plus a selection of additional third-parties tools, use one of these commands:

pip install [pnu-adsv](https://pypi.org/project/pnu-adsv/)
<br>
pip install [PNU](https://pypi.org/project/PNU/)
<br>
pip install [pytnix](https://pypi.org/project/pytnix/)

# ADSV(1)

## NAME
adsv - Analyze delimiter-separated values files

[![Servier Inspired](https://raw.githubusercontent.com/servierhub/.github/main/badges/inspired.svg)](https://github.com/ServierHub/)

## SYNOPSIS
**adsv**
\[-d|--delimiter CHAR\]
\[-e|--encoding STRING\]
\[-f|--fields LIST\]
\[-F|--flatten\]
\[-h|--hide INT\]
\[-m|--min INT\]
\[-M|--max INT\]
\[-t|--top INT\]
\[--debug\]
\[--help|-?\]
\[--version\]
\[--\]
filename
\[...\]

## DESCRIPTION
The **adsv** utility analyzes [delimiter-separated values](https://en.wikipedia.org/wiki/Delimiter-separated_values) files, such as  [Comma-Separated Values .csv](https://en.wikipedia.org/wiki/Comma-separated_values) or [Tab-Separated Values .tsv](https://en.wikipedia.org/wiki/Tab-separated_values) files, and either prints information about their structure and the data in each of their fields, or prints a selection of fields in the order requested.

The information gathered are:
* for the file:
  * the character set encoding
  * the [CSV dialect](https://specs.frictionlessdata.io/csv-dialect/) (characters used for delimiting, quoting, escaping or lines terminating. Plus the use or not of double quoting)
  * the presence or not of a headers line
  * the number of lines and fields
* for each field:
  * its number and header
  * the number of distinct values
  * the values type (strings, integers, floating numbers, complex numbers, date and time (whatever their format))
  * the values by descending count
  * the values range by ascending order using the detected type (useful for numbers and dates)

When analyzing a DSV dataset, this allows for a quick and automated way of getting global information about the contents, and explore any oddities...

There are options:
* to control and limit what is printed (*-h|--hide*, *-m|--min*, *-M|--max* and *-t|--top*), 
* to avoid (or correct) the detection of the character set encoding and delimiter (*-d|--delimiter*, *-e|--encoding*):
  * the character set detection can take a long time with big files, so if you know that the file is in "Windows-1252" or "utf-8" encoding, it's quicker to say it...

If you use the *-f|--fields* option, you'll skip printing the file analysis, and instead print the selected fields in the order requested, using the detected delimiting, quoting and escaping characters.

If you encounter multi-lines fields and want to "flatten" them to single lines, you can use the *-F|--flatten* option for that.

### OPTIONS
Options | Use
------- | ---
-d\|--delimiter CHAR|Specify delimiter to be CHAR
-e\|--encoding STRING|Specify charset encoding to be STRING (because detecting encoding can take a long time!)
-f\|--fields LIST|Extract LISTed fields values in given order (ex: 6,2-4,1 with fields numbered from 1)
-F\|--flatten|Make multi-lines fields single line
-h\|--hide INT|Hide the display of distinct values above INT % (default is 20%)
-m\|--min INT|Only display distinct values whose count >= INT (default is to display all distinct values)
-M\|--max INT|Only display INT lines of distinct values (default is to display all distinct values, within the hide limit)
-t\|--top INT|Only display the top/bottom INT lines of values (default is to display the 5 bottom and top lines)
--debug|Enable debug mode
--help\|-?|Print usage and a short help message and exit
--version|Print version and exit
--|Options processing terminator

## ENVIRONMENT
The ADSV_DEBUG environment variable can also be set to any value to enable debug mode.

## EXIT STATUS
The **adsv** utility exits 0 on success, and >0 if an error occurs.

## SEE ALSO
[cut(1)](https://www.freebsd.org/cgi/man.cgi?query=cut),
[file(1)](https://www.freebsd.org/cgi/man.cgi?query=file)

## STANDARDS
The **adsv** utility is not a standard UNIX command.

This implementation tries to follow the [PEP 8](https://www.python.org/dev/peps/pep-0008/) style guide for [Python](https://www.python.org/) code.

The DSV dialects that can be handled are those compatible with [RFC 4180: Common Format and MIME Type for Comma-Separated Values (CSV) Files](https://www.rfc-editor.org/rfc/rfc4180).

## PORTABILITY
Tested OK under Windows.

## HISTORY
This implementation was made for the [PNU project](https://github.com/HubTou/PNU).

I do this kind of analysis with each dataset I have to work with.
Last time I did that, I decided that it was about time to fully automate the process, especially as I was working with fields containing multi-lines values...

## LICENSE
It is available under the [3-clause BSD license](https://opensource.org/licenses/BSD-3-Clause).

## AUTHORS
[Hubert Tournier](https://github.com/HubTou)

## CAVEATS
Using "Sep=X" as a first line in order to set the X character as a delimiter is not supported.

There is no support either for potential commented lines inside the data (for example, with */etc/passwd* files under Unix), but it's not part of any recognized DSV dialect anyway.
