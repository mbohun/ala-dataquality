
---

|Name|UNCERTAINTY\_NOT\_SPECIFIED|
|:---|:--------------------------|
|Code|27|
|Description|Uncertainty was not supplied with the record|
|Severity/Verification/Metric|Warning|
|Failure implication|_See discussion below_|
|Revision Date|Extensively revised 28 October 2011|

#### _How should we represent spatial uncertainty of occurrence records when precision and/or extent of location are not supplied?_ ####
Occurrence locations are typically represented using the point–radius method with latitude/longitude (DwC:decimalLatitude/DwC:decimalLongitude) being the centre point of the location, and coordinate uncertainty (DwC:coordinateUncertaintyInMeters) representing the radius of a circle that covers the whole location, including the extent of the location and ALL errors and uncertainties associated with determining the coordinates.

DwC:coordinateUncertaintyInMeters is exactly equivalent to Maximum Error Distance used in some georeferencing tools (J. Wieczorek _in litt_.).

---

In a typical Australian situation coordinateUncertaintyInMeters would often be calculated by adding the four following terms:
  * extent of the location (ALA:locationExtent) – the radius of a circle encompassing the actual location or survey plot (not including other errors and uncertainties). Note that there is no explicit Darwin Core term for extent of location even though it is often included in the calculation of DwC:coordinateUncertaintyInMeters;
  * uncertainty associated with geocoding method – this relates to GPS accuracy or scale of map used to determine coordinates;
  * coordinate precision (DwC:coordinatePrecision) - the decimal representation of the precision of the coordinates, converted to metres;
  * potential datum shift  - where the datum (DwC:geodeticDatum) is unknown an additional error term needs to be added.

See [example](http://maps.google.com.au/maps/ms?msa=0&msid=216137528778546574111.0004a9191149ef64133f4&ie=UTF8&t=h&z=18&vpsrc=1).

---


In Australia there has been considerable confusion regarding spatial precision and uncertainty, with the terms sometimes used interchangeably. DwC:coordinateUncertaintyInMeters has often been interpreted to be just the extent of the location, rather than the extent plus all other errors and uncertainties associated with determining the coordinates e.g. georeferencing method; DwC:coordinatePrecision and DwC:geodeticDatum. This confusion probably relates to there being no Darwin Core term for the actual extent of the location, and that the Darwin Core description of coordinateUncertaintyInMeters does not explicitly mention that is it is inclusive of all uncertainty metrics: "The horizontal distance (in meters) from the given decimalLatitude and decimalLongitude describing the smallest circle containing the whole of the Location. Leave the value empty if the uncertainty is unknown, cannot be estimated, or is not applicable (because there are no coordinates). Zero is not a valid value for this term".


---

#### _With regard to spatial uncertainty, it is proposed that_ ####
1. Where recorded the extent of the location should be explicitly entered in a term new called locationExtent. Examples of location extent are the many millions of observational occurrences contained in the BA Bird Atlas data collected from 2ha, 500m and 5km survey plot locations, and historically from 10’ and one degree location grids. It is proposed that ALA nominated locationExtent be added as a term to the Darwin Core standard.

2. Where provided DwC:coordinatePrecision and DwC:coordinateUncertaintyInMeters (the overall metric) be also be saved as verbatim values in fields verbatimCoordinateUncertaintyInMeters and verbatimCoordonatePrecision. This will ensure consumers are aware of the original resolution of the data.

3. Where coordinates are generalized for the ALA Sensitive Data Service (typically by dropping decimal places from the coordinates, i.e. affecting the coordinatePrecision) then the Dwc:dataGeneralizations field be appropriately annotated; and DwC:coordinatePrecision and DwC:coordinateUncertaintyInMeters be adjusted thus:

Where verbatimCoordinateUncertaintyInMeters is explicitly available then:
> DwC:coordinateUncertaintyInMeters = verbatimCoordinateUncertaintyInMeters
and where coordinates are generalised by ALA then:
> DwC:coordinateUncertaintyInMeters = verbatimCoordinateUncertaintyInMeters + additional uncertainty from rounding coordinates, DwC:coordinatePrecision would be altered to relect the adjusted number of decimals.

Where DwC:coordinateUncertaintyInMeters is NOT available then:

DwC:coordinateUncertaintyInMeters is calculated by adding four nominal terms to represent overall uncertainty.
The four nominal terms are (i) coordinate precision: the decimal representation of the precision of the coordinates, converted to metres (if not available label as ‘Unknown’ and substitute 150 metres); (ii) locationExtent: i.e. extent of the location (where location extent is not available label as ‘Unknown’ and substitute 1000 metres); (iii) potential datum shift: where the datum (DwC:geodeticDatum) is not available label as ‘Unknown’ and add an additional 200 metres. Do this also if the coordinates have not been projected to GDA 94 or WGS 84 coordinate system. (iv) geocode uncertainty : i.e. GPS accuracy or map scale uncertainty, an additional 150 metres

Therefore default DwC:coordinateUncertaintyInMetere = 150+1000+200+150 = 1500 metres

5. Presently where uncertainty is specified some ALA spatial tools plot an uncertainty circle, while for visual clarity no circle is drawn when that field has an ‘Unknown’ value. Where this occurs there should be an explicit visual and textual indication that the location is in fact quite general and does not represent a point location.

It may be preferable that when the circle is shown it should represent the overall coordinateUncertaintyInMeters, and also be plotted when terms are ‘Unknown’. It would be worth conducting trials to obtain an optimal solution, perhaps with different shading/outline symbology where the terms are ‘Unknown’, e.g. if unknown a pale translucent circle with dotted outline could be plotted, while for specified values a darker circle with solid outline could be plotted.

_Note:_ It may be possible to assign more appropriate substitute values for certain data sets, for example data from ALA ‘Share a Sighting’ tool could use a default coordinate precision of 0.00001 degrees or 2 metres, with the datum error as 0, and with the Coordinate uncertainty (extent) being defined by the user. Also, there is a trend to increased spatial precision through time, e.g. records in 1800's are generally much less precisely located than those geocoded today using GPS or Google maps.

---


_A detailed explanation of each of the terms follows:_

#### Overall Coordinate Uncertainty ####
Coordinate uncertainty (DwC:coordinateUncertaintyInMeters) represents the radius of a circle that covers the whole location, including the extent of the location and ALL errors and uncertainties associated with determining the coordinates. DwC:coordinateUncertaintyInMeters is exactly equivalent to Maximum Error Distance used in some georeferencing tools (J. Wieczorek _in litt_.). It is proposed that where altered the original values be displayed as verbatimCoordinateUncertiantyInMeters.

#### Uncertainty associated with geocoding method ####
These uncertainties generally relate to the method (DwC:georeferenceProtocol) used to determine the latitude and longitude. Generally coordinates determined from GPS are quite precise (5-10 metres), especially if the Horizontal Dilution of Precision (HDOP) is also recorded. Coordinates determined from modern satellite maps, for example, Google Maps/Earth are also quite precise (although beware of satellite image rectification issues). On the other hand coordinates determined from say 1:1,000,000 maps or from gazetteers presenting coordinates to one minute are much less precise. Where this values is unknown, generally substitute about 150 meters i.e. the approximate average error of reading geocode from a 1:100,000 to 1:250,000 map sheet.

#### Coordinate precision ####
The precision of the location is defined by DwC:coordinatePrecision ‘A decimal representation of the precision of the coordinates given in the decimalLatitude and decimalLongitude. Examples: "0.00001" (normal GPS limit for decimal degrees), "0.000278" (nearest second), "0.01667" (nearest minute), "1.0" (nearest degree)’.

Where coordinate precision is ‘Unknown’, generally substitute 0.001 degrees or about 150 metres.

Sometimes the coordinates are generalised to protect sensitive species locations. Common methods are to (i) round or truncate coordinates to fewer decimal places, (ii) grid the data or (iii) randomly move the location. Where altered the original values be displayed as verbatimCoordinatePrecsion. Any generalisations need to be factored into the overall coordinateUncertaintyInMeters.

It is important to note that the number of decimal places in the coordinates cannot be relied upon to explicitly indicate the precision of the coordinates as they are often (unknowingly) rounded, truncated and imprecisely transcribed.

Note that the conversion of coordinate precision to metres varies with latitude; see Guide to Best Practices for Georeferencing page 27.

#### Extent of the location: locationExtent ####
Where ‘Unknown’ generally substitute 1000 metres

The extent of the location is not presently defined in the Darwin Core standard, although is often used in the calculation of the overall spatial uncertainty, i.e. DwC:coordinateUncertaintyInMeters.

The extent of a location varies greatly, for example, it may be an actual point within a metre or two of the coordinate; it could be a general location such as Black Mountain Reserve which is about 3.2 km across (locationExtent of about 1600 metres); or it may be a standardised survey plot like the 2ha areas used by Birds Australia (locationExtent of 100 metres).

#### Geodetic datum and spatial reference system ####
Where ‘Unknown’ generally substitute 200 metres.

For a latitude/longitude coordinate to be precisely located you must also know the spatial reference system under which it was collected: DwC:geodeticDatum. The current global standard is WGS84 (used by GPS, Google Maps), with the Australian standard GDA94 being virtually identical. Coordinates collected under older Australian standards: AGD 1966 and 1984 are in a different physical location to those of the modern standards, and so may be mis-mapped by 200 metres if not accounted for (see http://www.icsm.gov.au/gda/mapsgda.pdf ). This potential inaccuracy is called datum shift. A fuller definition of the Spatial Reference System may be contained in DwC:verbatimSRS, but this is generally not needed if the datum is available.


#### References ####
Chapman, A.D and J. Wieczorek (eds). 2006. Guide to Best Practices for Georeferencing. Copenhagen: Global Biodiversity Information Facility. Available at http://manisnet.org/GeorefGuide.html

TDWG. 2009. Darwin Core Terms: A quick reference guide. Aaialable at http://rs.tdwg.org/dwc/terms/

Wieczorek, J.  2007 Georeferencing Calculator, Version 070228. Available at http://manisnet.org/gc.html, with guidelines at http://manisnet.org/GeorefGuide.html


---



Examples from Georeferencing Calculator, http://manisnet.org/gc.html for Charleville Qld (midway NS across Australia).
MED is Maximum Error Distance _aka_ coordinateUncertaintyInMeters (CUIM)

_Assuming the location is an exact point:_
|Scenario|Geocoding method|Uncertainty from geocoding|Latitude|Longitude|Datum|Datum Shift (metres)|Coordinate precision (degrees)|Coordinate precision (metres)|Extent of Location|MED(m)|CUIM presentation (m)|
|:-------|:---------------|:-------------------------|:-------|:--------|:----|:-------------------|:-----------------------------|:----------------------------|:-----------------|:-----|:--------------------|
|Google Earth (always WGS84)|Google Earth 10m accuracy|10|-26.40066|146.24122|WGS84|0 |0.00001|1.5|0 |11.5|10|
|Google Earth (always WGS84), and generalised to 2 decimal places|Google Earth 10m accuracy|10|-26.4|146.24|WGS84|0 |0.01|1500|0 |1510|1500|
|GPS, datum recorded|GPS 10m accuracy|10|-26.40066|146.24122|WGS84|0 |0.00001|1.5|0 |11.5|10|
|GPS, datum recorded, and generalised to 2 decimal places|GPS 10m accuracy|10|-26.4|146.24|WGS84|0 |0.01|1500|0 |1510|1500|
|GPS, datum unknown|GPS 10m accuracy|10|26.40066|146.24122|? |200|0.00001|1.5|0 |211.5|200|
|GPS, datum unknown, and generalised to 2 decimal places|GPS 10m accuracy|10|-26.4|146.24|? |200|0.01|1500|0 |1710|1500|
|Bare coordinates 5 decimals, assume geocoded from 1:1,000,000 map|1:1,000,000 map|1000|-26.40066|146.24122|? |200|0.00001|1.5|0 |1201.5|1200|
|Bare coordinates 4 decimals, assume geocoded from 1:1,000,000 map|1:1,000,000 map|1000|-26.4006|146.2412|? |200|0.0001|15|0 |1215|1200|
|Bare coordinates 3 decimals, assume geocoded from 1:1,000,000 map|1:1,000,000 map|1000|-26.4|146.241|? |200|0.001|150|0 |1350|1500|
|Bare coordinates 2 decimals, assume geocoded from 1:1,000,000 map|1:1,000,000 map|1000|-26.4|146.24|? |200|0.01|1500|0 |2700|3000|
|Bare coordinates 1 decimals, assume geocoded from 1:1,000,000 map|1:1,000,000 map|1000|-26.4|146.2|? |200|0.1|15000|0 |16200|15000|
|Bare coordinates 1 decimals, assume geocoded from 1:1,000,000 map|1:1,000,000 map|1000|-26|146|? |200|0 |150000|0 |151200|150000|

_Assuming the location has an extent of 1000 metres (radius):_
|Scenario|Geocoding method|Uncertainty from geocoding|Latitude|Longitude|Datum|Datum Shift (metres)|Coordinate precision (degrees)|Coordinate precision (metres)|Extent of Location|MED(m)|CUIM presentation (m)|
|:-------|:---------------|:-------------------------|:-------|:--------|:----|:-------------------|:-----------------------------|:----------------------------|:-----------------|:-----|:--------------------|
|Google Earth (always WGS84)|Google Earth 10m accuracy|10|-26.40066|146.24122|WGS84|0 |0.00001|1.5|1000|1011.5|1000|
|Google Earth (always WGS84), and generalised to 2 decimal places|Google Earth 10m accuracy|10|-26.4|146.24|WGS84|0 |0.01|1500|1000|2510|2500|
|GPS, datum recorded|GPS 10m accuracy|10|-26.40066|146.24122|WGS84|0 |0.00001|1.5|1000|1011.5|1000|
|GPS, datum recorded, and generalised to 2 decimal places|GPS 10m accuracy|10|-26.4|146.24|WGS84|0 |0.01|1500|1000|2510|2500|
|GPS, datum unknown|GPS 10m accuracy|10|26.40066|146.24122|? |200|0.00001|1.5|1000|1211.5|1200|
|GPS, datum unknown, and generalised to 2 decimal places|GPS 10m accuracy|10|-26.4|146.24|? |200|0.01|1500|1000|2710|3000|
|Bare coordinates 5 decimals, assume geocoded from 1:1,000,000 map|1:1,000,000 map|1000|-26.40066|146.24122|? |200|0.00001|1.5|1000|2201.5|2000|
|Bare coordinates 4 decimals, assume geocoded from 1:1,000,000 map|1:1,000,000 map|1000|-26.4006|146.2412|? |200|0.0001|15|1000|2215|2000|
|Bare coordinates 3 decimals, assume geocoded from 1:1,000,000 map|1:1,000,000 map|1000|-26.4|146.241|? |200|0.001|150|1000|2350|2500|
|Bare coordinates 2 decimals, assume geocoded from 1:1,000,000 map|1:1,000,000 map|1000|-26.4|146.24|? |200|0.01|1500|1000|3700|4000|
|Bare coordinates 1 decimals, assume geocoded from 1:1,000,000 map|1:1,000,000 map|1000|-26.4|146.2|? |200|0.1|15000|1000|17200|15000|
|Bare coordinates 1 decimals, assume geocoded from 1:1,000,000 map|1:1,000,000 map|1000|-26|146|? |200|0 |150000|1000|152200|150000|

_Note: CUD of earlier versions has been abandoned in favour of recording verbatimCoordinateUncertaintyInMeters and verbatimCoordinateArecision._