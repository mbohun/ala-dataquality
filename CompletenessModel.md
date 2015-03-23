# Completeness models #

> Completeness analysis puts the mapping and design process on rails. <br><i>A. Tindall</i></li></ul>

The quality completeness model (completeness model, or <i>CM</i>) is a first step toward analysing the <i>fitness for use</i>, or improving the <i>quality at source</i>, of a data export. Completeness analysis allows a user to look at the availability of supporting information, without specifically delving into <i>content analysis</i> (<i>i.e.</i> looking at the values in the data).<br>
<br>
Each model is tied to a specific biodiversity informatics' data standard; there are two in the works:<br>
<ul><li>Darwincore 2.6, with 2.7 being prototyped - <a href='CompletenessModelDwC.md'>DwC (CompletenessModelDwC)</a>
</li><li>HISPID 5 in planning phase - <a href='CompletenessModelHISPID.md'>HISPID (CompletenessModelHISPID)</a></li></ul>

The models generally don't cover their respective specifications entirely (<i>i.e.</i> don't reference all fields in the data standard). They can be considered a tool to aid in a deeper understanding of the source data, as well as the desired transformation standard.<br>
<br>
<br>
<h2>Quick start summary for a new completeness model ##

### New DwC completeness model ###
_(Note: visit [CompletenessModelDwC](CompletenessModelDwC.md) for details...)_

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

### New HISPID completeness model ###
**2011/12/21** - tba... finger out !


## Physical implementation ##

The models manifest themselves as a google docs spreadsheet with the following parts:
  * schedule of source to target fields (_Mapping_, first sheet),
  * a table of these terms with additional information _QualityRelationships_, second sheet), and
  * a set of rules that highlight potentially absent data (completeness tests).

The _QualityRelationships_ sheet cross-references data-source information in the _Mapping_ sheet with two distinct, logical, groupings of terms from the data standard. It is designed to aid the user in better understanding their source-data and its mapping to the standard. It also includes value metadata and pointers to other related terms.

The completeness tests are a series of logic that highlights potentially absent data by working through the mapping and relationship sheets...  see the _Implementation details_ section in the details document for [DwC (CompletenessModelDwC)](CompletenessModelDwC.md) or [HISPID (CompletenessModelHISPID)](CompletenessModelHISPID.md) for more info.


### Completeness test example ###

A notable example of a completeness test would be the datum that is associated with geographical coordinates, or the projection that is associated with a grid-reference.
_see: Handling spatial location data - http://goo.gl/7Dwrl for more details on this topic_

Without the _datum_ or _projection_, there is an additional level of uncertainty inherent in the coordinates when a data consumer beings an analysis. Including this additional information (_i.e. metadata_) improves the overall fitness for use.

Tests also exist for:
  * ensuring the logical components of a record can be uniquely identified,
  * institutional (custodian?) and researcher (owner?) provenance,
  * data usage rights and attribution,
  * spatial and temporal data,
  * research methodology and publication,
  * taxonomy,
  * ...


## Potential uses ##

When planning a data export overall completeness could be considered best practise, however, the source data might not allow for this.

This highlights a number of other potential uses for a completeness analysis:
  1. new data store design,
  1. existing data store and data-capture process enhancement,
  1. historical gap analysis & automated quality-assessment,
  1. supplementary data export planning,
  1. ...



---



# Existing completeness models #

## DwC files ##
google docs -> CompletenessDwC
http://goo.gl/WZj7Z _-or-_
https://docs.google.com/open?id=0ByNWJFdh4pHZZTExOTU5ZTMtNjE4Yy00ODk0LWIxNzktOGRhZTczZDgxMmUz

## HISPID files ##
google docs -> CompletenessHISPID
http://goo.gl/TPsTb _-or-_
https://docs.google.com/open?id=0ByNWJFdh4pHZZDMzNDA2ZWEtOTQ5OS00MDZjLTg2MDItMGZlYmE0NjU4MzYw



---



# Future plans for completeness models #