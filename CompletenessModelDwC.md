# Introduction #

This model is a first step toward analysing the completeness of a dwc export; it doubles as a tool to help people out with designing new data stores, and documenting the decisions & compromises made as exports evolve.

this analysis tool lives in the spreadsheet linked below; it's used to see what other data might be added to an export to enhance its usage potential (it doesn't do any content analysis)

the executive summary of the spreadsheet is this:
  * there is a table with all of the terms in your export (first worksheet 'mapping')
  * and there is a table of all the darwincore terms (second worksheet 'quality relationships')
  * in the latter, there is an indicative column (E) that references the former, or blank if the term is not found in the 'mapping'
  * the terms also have their relevant dwc group next to them (C)
  * they also have an ala-applied grouping called 'quality facet' (A)
  * this so-called 'quality facet' also happens to be a series of steps - a logical process one can follow in order to complete a dwc analysis

**Please note:** a general introduction to the concepts referred to in this page lives at [CompletenessModel](CompletenessModel.md); _(this is also part of a series of pages relating to [data mobilisation](http://code.google.com/p/ala-datamob/))_


## Create a new DwC completeness model ##

  1. open the master spreadsheet:
    * https://docs.google.com/spreadsheet/ccc?key=0AiNWJFdh4pHZdHJnQU01bXlDeUdaMkJ5Z1EwN01HaGc&hl=en_US#gid=0 _-or-_ http://goo.gl/XNehZ
  1. create a copy: File menu -> Make a copy...
  1. store your existing (or planned) mapping in a new file somewhere:
    * create a spreadsheet using excel, google docs, openoffice caclc, etc...
    * fill _column a_ with the target dwc term, and if possible, _column b_ with the source field (optional)
      * _tip if you have an existing export_ that you want to analyse, copy the header row and 'paste special->transpose' (or equivalent) into a new spreadsheet; this should transform the fields from 'one field-name per column' to 'one field name per row'...
    * export this list of fields to a new text file, tab-delimited
  1. go back to your new google docs spreadsheet and import the column names into the mapping sheet:
    * File menu -> Import...
    * select the file you created earlier, and choose _Append rows to current sheet_



---



# Implementation details: _Mapping_ and _QualityRelationships_ sheets #

## Mapping sheet ##
_description of the mapping sheet..._

<wiki:gadget url="http://hosting.gmodules.com/ig/gadgets/file/117808631063490062819/url.xml" up\_Url="https://docs.google.com/spreadsheet/ccc?key=0AiNWJFdh4pHZdHJnQU01bXlDeUdaMkJ5Z1EwN01HaGc&hl=en\_US#gid=0" up\_Title="DwC quality completeness v2.6 - master copy.Mapping" up\_height=460 width="840" up\_refresh=6000 />

_DwC quality completeness v2.6 - master copy.Mapping sheet_

### TargetField ###
This should be a data-standard term's (short) name; it must be exact for the lookup algortithm in QualityRelationships to match this row.

### SourceField ###

If this column has no value but a matching column a value, the following behaviour occurs in _QualityRelationships_ :
  * _Mapped column_ will show a reference to this cell, _e.g._ Mapping!B89, and
  * the text will be bright red

Otherwise, values entered here will appear in the _QualityRelationships.Mapped column_ field. There are some special strings in this cell that impact on the conditional formatting in _QualityRelationships_ :
  * _nonDwC_
  * _see:_
  * _!_
  * _?_
  * _excl:_
  * _proposed:_


### Status, last update ###

### Other ###


## QualityRelationships sheet ##

_description of the qr sheet..._

<wiki:gadget url="http://hosting.gmodules.com/ig/gadgets/file/117808631063490062819/url.xml" up\_Url="https://docs.google.com/spreadsheet/ccc?key=0AiNWJFdh4pHZdHJnQU01bXlDeUdaMkJ5Z1EwN01HaGc&hl=en\_US#gid=1" up\_Title="DwC quality completeness v2.6 - master copy.!QualityRelationships" up\_height=460 width="840" up\_refresh=6000 />

_DwC quality completeness v2.6 - master copy.QualityRelationships sheet_


### ALA quality facet ###
The completeness model introduces a complementary method for grouping the DwC terms – quality facets. These facets prove common to most of the existing logical groups already defined (see _DwC group link_).

As a result of this commonality, the quality facets can also be seen as a series of steps for mapping to, or assessing completeness of, each DwC group.

This completeness assessment encourages 'quality at source', and is a pre-cursor to more comprehensive analysis of the content.

Both the completeness assessment and the content analysis contribute to an overall assessment of the data quality, and for the end user to determine fitness for use.

Current values are:
  1. **basis** - founds the digital record: 1. as unique within a system, 2. as related to other versions of the same
  1. **precision** - term is used as an indicator of the precision in the DwC group; and **uncertainty** - a statement about the uncertainty of data in the DwC group
  1. **spatial** - place/space pointer; and **temporal** - time pointer
  1. **verbatim** - storing the raw data if any parsing/processing has occurred (allowing for reproduction/reinterpretation)
  1. **notes** - free(er) text, related to some concept, in a particular DwC group; and **verification** - pertaining to the veracity of the DwC group
  1. **ID** - system-unique identifier of a concept related to the DwC group

### Type ###
  1. area - value identifies an area in some spatial standard
  1. date - value is a date in some temporal standard
  1. elevation - value identifies an elevation (+/-) in some spatial standard
  1. multiple - values, separated according to dwc spec.
  1. point - value defines a single point in space using some standard
  1. range - value is a range defined according to dwc spec.
  1. referent - an entity external to these system(s), eg: a person, publication, organisation
  1. unique - value must be unique within this basis (see quality facet: basis)
  1. uri - a digital reference to a concept arbitered in/by another system (implies a constrained set of valid values)
  1. value - no specific restrictions, but spec. may define 'best practise'
  1. vocab - recommended controlled vocab

### DwC group link ###
The darwin core grouping of terms, linked to the wiki discussion on the TDWG website.

### DwC term link ###

### Mapped column ###
The field in the 'mapping' sheet associated with this dwc term.

### Verbatim term ###

### Quality rel terms ###

### Other columns ###
#### Mapped-not-null ####



---



# Implementation details: Completeness tests #