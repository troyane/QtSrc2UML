## QtSrc2UML

Basically it is answer to [StackOverflow question](https://stackoverflow.com/questions/56158183/qt-c-class-diagrams/56165687#56165687).

This repository contains:

* [`Doxyfile`](https://github.com/troyane/QtSrc2UML/blob/master/Doxyfile) to generate UML class diagram with all documentation, and
* Result of `doxygen` work:
  * [Documentation itself](https://troyane.github.io/QtSrc2UML/docs/html/index.html),
  * [UML diagram](https://troyane.github.io/QtSrc2UML/docs/html/inherits.html).


### Prepare docs

Since Qt has well documented source code and this code is [qDoc](https://doc.qt.io/qt-5/01-qdoc-manual.html)-powered (which is compatible with [doxygen](http://www.doxygen.nl/)). You may generate required diagrams by yourself. 

*(I'm not sure how much time will it take you, but probably get some popcorn beforehand)*

I'll show you example how to prepare diagrams for `QtConcurrent` module only (doxygen work took me ~8s on i7-6820HQ).
1. Install doxygen. Typically:
```
sudo apt install doxygen
```
2. Get and unpack Qt sources (http://download.qt.io/official_releases/qt/5.12/5.12.3/single/).
3. Use console and navigate to `qt-everywhere-src-5.12.3/qtbase/src/`.
4. Generate standard `Doxygen` file by command:
```
doxygen -g
```
5. Edit `qt-everywhere-src-5.12.3/qtbase/src/Doxygen`. 
Append next lines (or make sure that everywhere in `Doxyfile` any assignments of these variables are commented):

```
EXTRACT_ALL          = YES
CLASS_DIAGRAMS       = YES
HIDE_UNDOC_RELATIONS = NO
HAVE_DOT             = YES
CLASS_GRAPH          = YES
COLLABORATION_GRAPH  = YES
UML_LOOK             = YES
UML_LIMIT_NUM_FIELDS = 50
TEMPLATE_RELATIONS   = YES
DOT_GRAPH_MAX_NODES  = 100
MAX_DOT_GRAPH_DEPTH  = 0
DOT_TRANSPARENT      = YES
```
According to [this answer](https://stackoverflow.com/a/38322858/867349).

Find `INPUT` section and put:
```
INPUT                  = concurrent
```
Find `GENERATE_LATEX` section and change to :
```
GENERATE_LATEX         = NO
```
**NOTE:** If you are familiar with `doxygen`, edit `Doxyfile` as you wish -- there are plenty of possible settings like logo, additional texts, file patterns, excludes etc. 

6. To generate doxygen documentation just run `doxygen`.

As a result you'll get folder `qt-everywhere-src-5.12.3/qtbase/src/html` with generated documentation. Open `index.html`.

To see the result [click here](https://troyane.github.io/QtSrc2UML/docs/html/index.html).