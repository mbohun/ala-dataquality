
---

|Name|DETECTED\_OUTLIER\_GEOGRAPHIC|
|:---|:----------------------------|
|Code|x |
|Description|The location is an outlier detected in geographic space|
|Severity/Verification/Metric|Error|
|Failure implication|Optionally exclude from mapping and other reports|
|Darwin Core Class|Location|
|Darwin Core Fields|decimalLongitude, decimalLatitude|
|New/Currently Supported|New|


---

### References ###

Burgman. M.A. & J.C. Fox. 2003. Bias in species range estimates from minimum convex hulls: implications for conservation and options for improved planning. Animal Conservation 6, 19-18.

IUCN. 2009. Definitions of terms used in the IUCN Categories and Criteria: Extent of Occurrence. PowerPoint presentation downloaded from www.iucnredlist.org/documents/Extent\_Of\_Occurrence\_Aug09.pps

Fu, L. 2009 Implementation of Three-dimensional Scagnostics. Master thesis available at http://www.math.uwaterloo.ca/navigation/CompMath/graduatestudies/Fu_copy.pdf

Pateiro-Lopez, B. & A. Rodriguez-Casal.2011. 2011-10-23, R package: alphahull: Generalization of the convex hull of a sample of points in the plane.  Version 0.2-1, 2011-10-23. Available at http://cran.r-project.org/web/packages/alphahull/index.html

Wikepedia 2011. Home range at http://en.wikipedia.org/wiki/Home_range

---


### Implementation notes (algorithms) ###

Burgman and Fox (2003) advocated the use of alpha-hulls as a means of excluding discontinuities when determining a species extent of occurrence (distribution range). Along with the convex hulls, alpha-hulls have been included in the range of tools advocated for determining extent of occurrence of a species (IUCN 2009). Alpha-hulls can also be used to estimate animal home ranges (http://en.wikipedia.org/wiki/Home_range). Birds Australia are presently
using the method to flag outlier records.

The alpha-hull method is based on Delaunay triangulation and works by joining lines between all species occurrence points to form triangles, then measuring the length of each edge and excluding those triangles that are more than a multiple (alpha) of the average edge length. While IUCN (2009) advocated an alpha value of two as a good starting point, Burgman and Fox found that a value of three was consistently the most robust to sampling artefacts introduced by differing sampling intensities, spatial accuracies and spatial uniformities.

Burgman and Fox also found that _another advantage of the alpha-hull is that outliers are also excluded from the hull when their distance from other records exceeds the alpha value_. Note that three adjacent (< alpha length) isolated points will form a separate ‘island’ hull, while single isolates are always excluded, the R implementation treats two adjacent isolated points as inliers if they are within alpha distance hull.

Note that it is important to remove repeated records of the same occurrence which may have slightly different coordinates created through rounding errors and other artefacts. This sometimes occurs where data are aggregated from different sources.

Implementation example
R package: alphahull: Generalization of the convex hull of a sample of points in the plane.

'This package computes the alpha-shape and alpha-convex hull of a given sample of points in the plane. The concepts of alpha-shape and alpha-convex hull generalize the definition of the convex hull of a finite set of points. The programming is based on the duality between the Voronoi diagram and Delaunay triangulation. The package also includes a function that returns the Delaunay mesh of a given sample of points and its dual Voronoi diagram in one single object.'

The package has two arguments x,y for the coordinates of a set of points, and alpha value.
Exact duplicate coordinates must be removed otherwise an error occurs: ‘Error in tri.mesh(X) : duplicate data points’.

Note that the R implementation uses arcs during triangulation, whereas some other implementations form straight line triangles.

See Fu (2009) for example of java implementation.

---

#### Preliminary Evaluation ####
A useful and readily implemented method of outlier check suited to characterising occurrence records in geographic space (latitude and longitude) and indicate spatial outliers. It is not suited to analysis of occurrence records in univariate or bivariate environmental space.
As the method relies on an arbitrary geographic distance rather than environmental distance then errors of omission may occur where (i) there are steep environmental gradients over relatively short geographic space; and (ii) three or more adjacent spurious occurrences occur as isolates. Errors of omission may occur where there are one or two isolated genuine occurrences.

---

#### Example Plots ####

_Figure 1_

![http://ala-dataquality.googlecode.com/svn/trunk/images/acanthiza-katherina-alphahull-3.png](http://ala-dataquality.googlecode.com/svn/trunk/images/acanthiza-katherina-alphahull-3.png)

Figure 1 shows the alphahull R implementation (alpha=3) applied to occurrences of the _Acanthiza katherina_ Mountain Thornbill, an inhabitant of upland rainforest in north-eastern Queensland. Detected outlier values are the solid back dots outside the bounding hull.


---


_Figure 2_

![http://ala-dataquality.googlecode.com/svn/trunk/images/macropus-rufus-alphahull-3.png](http://ala-dataquality.googlecode.com/svn/trunk/images/macropus-rufus-alphahull-3.png)

Figure 2 shows the alphahull R implementation (alpha=3) applied to occurrences of the _Macropus rufus_ Red Kangaroo, an inhabitant of arid inland Australia. Detected outlier values are the solid back dots outside the bounding hull. Note the isolated hull in the northwest formed by two adjacent records are not considered outliers.  Note that single records greater than alpha distance from a hull are always considered outliers.



---



_Figure 3_


![http://ala-dataquality.googlecode.com/svn/trunk/images/macropus-rufus-alphahull-2.png](http://ala-dataquality.googlecode.com/svn/trunk/images/macropus-rufus-alphahull-2.png)


Figure 3 shows the Red Kangaroo occurrences with alpha set to 2. Note how fewer peripheral records are included in the hull and are considered  outliers. An alpha setting of 2 may be preferred for outlier detection where this method is used in conjunction with additional environmental surface outlier detection methods.


---

### Logic ###

  1. Obtain all occurrence records for a species.
  1. Discard duplicate and repeated records from the sample.
  1. Run algorithm and flag outliers.


---

### Contributors ###
Simon Bennett


---
