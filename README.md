# latex-mscgen
LaTeX package to interface with mscgen (exe)

Source : https://github.com/Kochise/latex-mscgen

## installation

Get 'mscgen' for Windows : http://www.mcternan.me.uk/mscgen/<br>
Uncompress/install it where you need.<br>
Add it in your global/local/session PATH variable.<br>

```batch
\>set PATH=%PATH%;<mscgen>\Msc-generator

xcopy /c /h /e /r /q /y latex-mscgen <miktex>\texmfs\install\tex\latex\mscgen
start "" "<miktex>\miktex-portable.cmd"
```

Refresh the filename database.<br>
Update the package database.<br>
You should be ready to go.<br>

Alternatively, you can use https://github.com/Kochise/win_portable

## usage

See http://msc-generator.sourceforge.net/help/<br>

In your preamble :

```latex
\def\imagepath{./images}
\graphicspath{{\imagepath/}}
\usepackage[imagepath=\imagepath]{mscgen}
```

In your document :

```latex
% http://msc-generator.sourceforge.net/help/5.4/Text-Formatting.html
%\begin{mscgen}[width]{caption}{refname}
msc {
  hscale = "2";

  a,b,c;

  a->b [ label = "ab()" ] ;
  b->c [ label = "bc(TRUE)"];
  c=>c [ label = "process(1)" ];
  c=>c [ label = "process(2)" ];
  ...;
  c=>c [ label = "process(n)" ];
  c=>c [ label = "process(END)" ];
  a<<=c [ label = "callback()"];
  ---  [ label = "If more to run", ID="*" ];
  a->a [ label = "next()"];
  a->c [ label = "ac1()\nac2()"];
  b<-c [ label = "cb(TRUE)"];
  b->b [ label = "stalled(...)"];
  a<-b [ label = "ab() = FALSE"];
}
\end{mscgen}
```

## options

What is available through 'mscgen.exe' (which is a lot) :

```
% Puts msc-generator into text editor integration mode
--tei-mode

% Output file type (default is 'png')
-T [png/eps/pdf/svg/ismap/lmap/csh/emf]

% Embed the chart text into 'png' file as an iTXt chunk (uncompressed)
-e

% Output file (png, eps, pdf, svg, emf)
-o outfile

% Input file
-i infile

% Forces the input file to be interpreted as as a specific type of chart
-S <signalling/graph>

% Forces the input file to be interpreted as UTF-16, even if it looks like UTF-8 or ASCII
--utf16

% Forces the input file to be interpreted as UTF-8, even if it does not look like it
--utf8

% Full-page output ('p' or an 'l' for portrait and landscape)
-p=[A0-A6/letter/legal/ledger/tabloid][l/p]

% Specifies the margin in full-page output (in inches -number only- or in centimeters -appended with 'cm')
-m{lrud}=‘margin'

% Set the vertical alignment within a page for full-page output
-va=[center/up/down]

% Set the horizontal alignment within a page for full-page output
-ha=[center/left/right]

% Automatic pagination
-a[h]

% Width (in pixels)
-x=width

% Height (in pixels)
-y=height

% Scale chart size up or down
-s=scale

% Use specified font (must be available in the local system)
-F font

% Load additional chart design definitions
-D design_file

% Don't load design files
--nodesigns

% Chart option
--chart_option=value

% Chart's design pattern
--chart_design

% No warnings displayed
-Wno

% Additional Technical Info is printed about compilation
-TI

% No progress indicator displayed
-Pno

% Display program licence and exit
-l

% Display program help and exit
-h, --help

% Display version information and exit
--version
```

Options specific to Signalling Charts:

```
% Forces the chart to be interpreted in mscgen mode
--force-mscgen

% Prevents the chart to be interpreted in mscgen mode
--prevent-mscgen

% Disables warnings for deprecated constructs for backwards compatibility
-Wno-mscgen

% Enforces stricter language interpretation
--pedantic
```

Cannot be specified on a group basis, only in the preamble.<br>
Just add the requested parameters without the leading dash(es).<br>

```latex
\usepackage[ha={center}]{mscgen}
```

Avoid :

```
i		: because used by the provided text
o		: because using the refname
T		: because set to 'eps' (vector) as default
utf8	: because cannot use numbers
utf16	: because cannot use numbers
```

For UTF specification, use the following format :

```latex
\usepackage[utf={8}]{mscgen}
```

## limitations

Your imagination.

## greetings

Based on https://github.com/dakusui/latex-ditaa<br>
Based also upon https://github.com/unjello/msctexen<br>
Help from the community https://tex.stackexchange.com/questions/570758/verbatimout-newenvironment-and-removing-characters/<br>
Also interested into https://github.com/sile-typesetter/sile<br>
