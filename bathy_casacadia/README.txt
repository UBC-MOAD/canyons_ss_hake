

Digital elevation model (DEM) of Cascadia, latitude 39N-53N, longitude
116W-133W

compiled by
Ralph A. Haugerud (1)


Open-File Report 99-369

This report is preliminary and has not been reviewed for conformity with
U.S. Geological Survey editorial standards or with the North American
Stratigraphic Code. Any use of trade, product, or firm names is for
descriptive purposes only and does not imply endorsement by the U.S.
Government.

The data in this report are not suitable for navigation.




U.S. DEPARTMENT OF THE INTERIOR
U.S. GEOLOGICAL SURVEY
  ------------------------------------------------------------------------

(1) USGS@UW, Box 351310, Seattle WA 98195
email: rhaugerud@usgs.gov
  ------------------------------------------------------------------------

Introduction

This report contains a 250-meter digital elevation model (DEM) for Cascadia
(latitude 39N - 53N, longitude 116W - 133W), a region that encompasses the
Cascade volcanic arc, the Cascadia subduction zone, and the Juan de Fuca
Ridge system. The DEM is distributed as file cascdem.tar.gz  (39 MB; 78MB
uncompressed).

Cascdem.tar.gz includes the following files:

 index.htm     this document in html form

 README.txt    this document as ASCII text

 cascadia.bil  data file, about 77 megabytes in size

 cascadia.hdr  header file

 cascadia.stx

 cascadia.blw

 cascadia.prj  ARC/INFO projection file for Cascadia grid

 sources.e00   ARC/INFO export file of map of data sources

The DEM contains elevation values in integer meters, at regularly-spaced
points in a Lambert conformal conic projection with standard parallels at
latitudes 41.5N and 50.5N, and a central longitude of 124.5W (the
"Cascadia" projection.).

This report is on the World-Wide Web at
http://geopubs.wr.usgs.gov/open-file/of99-369. It may also be obtained by
anonymous ftp at:

         geopubs.wr.usgs.gov

cd to directory

         pub/open-file/of99-369

File cascdem.tar.gz may also be obtained by sending a 2.3 or 5.0 GB, 8mm
Exabyte tape with request and return address to

     Cascadia DEM
     c/o Database Coordinator
     U.S. Geological Survey
     345 Middlefield Road, MS 975
     Menlo Park, CA 94025

The compressed tar file will be returned on the tape.


A 1:2,000,000-scale color shaded-relief map prepared from this DEM, with an
interpretation of the physiography of Cascadia, is in press as U.S.
Geological Survey map I-2689.

To ease data transfer for the widest possible range of users, the DEM is
distributed as a BIL (Band Interleave by Line) file, produced with the ARC
GRIDIMAGE command. For grids (the ARC term for a DEM in the form of a
regular array of height values), such files are more compact than ARC
export (.e00) files and USGS DEM-format files, and are much faster to
create and import. They can also be read by many applications other than
ARC. cascadia.bil is such a file of binary integers. Elevations are stored
in cascadia.bil as unsigned positive 2-byte binary integers, in Motorola
byte-order (default for Sun hardware), with an offset of 10000. That is,
203 meters is stored as 10203 meters, and values less than 10000 represent
negative elevations. Values of 0 in cascadia.bil represent no data. Values
are given by row, west to east, starting at the north edge of the region.

To convert CASCADIA files to an ARC grid

Assemble the cascadia.* files (.bil, .blw, .hdr, prj; .stx is not
necessary) in one directory. Make this your workspace.

     Arc: imagegrid cascadia casc1
     Arc: grid
     Grid: casc2 = con(casc1 <> 0, casc1 - 10000)
     Grid: &sys cp cascadia.prj casc2/prj.adf

If you DESCRIBE casc2 in ARC, you should get

     Description of Grid CASC2

     Cell Size = 250.000 Data Type: Integer
     Number of Rows = 6435 Number of Values = 8555
     Number of Columns = 5951 Attribute Data (bytes) = 8

     BOUNDARY STATISTICS

     Xmin = -738044.062 Minimum Value = -4853.000
     Xmax = 749705.938 Maximum Value = 4378.000
     Ymin = 101590.289 Mean = -628.692
     Ymax = 1710340.289 Standard Deviation = 2076.818

                          COORDINATE SYSTEM DESCRIPTION

     Projection              LAMBERT
     Zunits                  UNKNOWN
     Units                    METERS             Spheroid
     CLARKE1866
     Parameters:
     1st standard parallel                                   41 30
     0.000
     2nd standard parallel                                   50 30
     0.000
     central meridian                                       -124 30
     0.00
     latitude of projection's origin                         38  0
     0.000
     false easting (meters)
     0.00000
     false northing (meters)
     0.00000

To use the SOURCES coverage

Sources.e00 is only accessible with ARC/INFO. Copy sources.e00 to an
appropriate directory, start ARC/INFO, make this directory your workspace,
and type

     Arc: import cover sources sources

to convert the export file into a usable coverage named sources.

Coverage sources was created with the ARC GRIDPOLY command from a 250-m
grid. It does not provide a usable shoreline!

How the DEM was compiled

To make the DEM, data from many sources were resampled at a 250-m interval
in the Cascadia map projection and composited. The software used for
projecting the data (ARC/INFO GRID, version 7.0.3) does not allow for
explicit registration of the output grid, and as a result there are lateral
shifts of potentially as much as one grid cell (250 meters) between blocks
of data. These shifts appear to be insignificant at this resolution. Data
sets 14, 15, and 16 (see below) were combined, interpolated, and gridded
together to produce a surface that is smooth at the data-set boundaries.

One-cell-wide gaps between data blocks that resulted from lateral shifts
were filled with the focal mean of surrounding values. Wider gaps were
locally present at some shoreline locations, where marine and terrestrial
data were truncated at different shorelines. These were filled with value Z
= 0.

Marine and terrestrial data were merged with the naive assumption that they
are measured in relation to the same vertical datum. This is not so: marine
depths are relative to Mean Lower Low Water, whereas terrestrial elevations
were measured from datums which are approximately equivalent to Mean Sea
Level. The difference is most acute in the southern end of Puget Sound
(Washington State), where the vertical datums differ by about 2 meters.

Artifacts

Lack of data makes most of the floor of the northeastern Pacific Ocean
appear smooth. Some of the smoothness is real, reflecting a blanket of
sediment that smothers the oceanic-ridge topography beneath it. But most of
the smoothness simply reflects insufficient data--compare the areas from
sources 14, 15, and 16 with adjacent areas of high-resolution multibeam
sonar surveys (sources 2 and 3). Similarly, apparent differences in the
physiography of the Washington continental slope, relative to adjoining
parts of the slope, at least partly reflect differences in data quality.
Additional artifacts result from mismatches between sets of source data.
Perhaps the most obvious mismatch is at longitude 132°W, extending south
from 52°N, where an abrupt change in apparent depth occurs at a source-data
boundary. Abrupt northward termination at 46°N of longitudinal ridges in
the Juan de Fuca Slope also reflects juxtaposition of differing data
sources.

Sources

(Numbers correspond to polygon-IDs in the sources coverage.)

     1) WASH_30M2: Thirty-meter (UTM) 7.5-minute quad-format DEMs,
     most produced by scanning/vectorizing/gridding 1:24000-scale
     topographic maps. Obtainable from USGS or WDNR. Some produced by
     stereoprofiling (poor quality), a few produced via Gestalt
     Photo-Mapper (semi-automated image correlation procedure, which
     makes mostly-excellent grids of the tops of the trees.) DEMs were
     merged into larger blocks, then projected/subsampled, and merged
     to a state-wide grid. Minor holes between data blocks were filled
     with the focal mean of surrrounding cells

     2) SEABEAM: Multi-beam swath bathymetry. Projected/subsampled
     from 100-m (UTM) grids (National Geophysical Data Center, 1993)

     3) PMELTRIM2: Trimmed version of 250-m (Cascadia projection) grid
     supplied by Andra Bobbitt, Pacific Marine Environmental
     Laboratories, Newport, Oregon. Data is composite of SEABEAM data
     collected on research cruises to the Juan de Fuca spreading
     center. Same data (as 100-m grid) is available from
     Lamont-Doherty RIDGE Web server

     4) NOS_N, NOS_S: Raw digital hydrographic survey data (National
     Geophysical Data Center, 1998). Used, with USGS 1:100K DLG
     shorelines (EDCFTP) to construct triangulated irregular networks
     in UTM coordinates. TINs were gridded, smoothed,
     projected/subsampled to Cascadia projection, and merged

     5) DMA_3AS: Three-arc-second DEMs (geographic grid) from EDCFTP,
     merged into larger blocks, projected/subsampled to Cascadia
     projection, and merged into final block. Single-cell-width holes
     filled with focal mean of surrounding cells. Trimmed to Z > 0
     prior to merging onto marine data. After merging with marine
     data, holes in low-elevation coastal areas patched with Z = 0

     6 DTED_3AS: Three-arc-second DEMs (geographic grid) produced by
     U.S. Defense Mapping Agency. May be purchased from Geomatics
     Canada. Merged into larger blocks, projected/subsampled, and
     merged to single block. Areas of bad data along some 1°x1° block
     boundaries deleted. Trimmed to Z > 0 prior to merging with other
     data

     7) GOLDFINGER: Incomplete 100-meter grid of Oregon continental
     shelf and slope, provided by Chris Goldfinger, Oregon State
     University (personal communication, 1994)

     8) GFPATCH: Patches to Goldfinger's 100-m grid, produced by
     interpolating across gaps with TOPOGRID (ARC/INFO 7.0.3, drainage
     enforcement off)

     9) CA_SHELF, OR_SHELF3, WA_SHELF: 1:100,000-scale digital line
     graphs (DLGs) of bathymetry (EDCFTP), supplemented with
     1:100K-scale shoreline DLGs (also EDCFTP) and gridded with
     TOPOGRID (ARC/INFO 7.0.3, drainage enforcement off.) Gridded at
     30 to 100 meter resolution, in UTM coordinates, then
     projected/subsampled.

     10) CA_SHELF_N: Digitized by Haugerud from U.S. Coast and
     Geodetic Survey (1969). Projected to Cascadia projection, and
     then gridded with TOPOGRID (ARC/INFO 7.0.3, drainage enforcement
     off)

     11) PUGETSOUND_J:  Projected/subsampled from 300-meter grid of
     Puget Sound basin (Myrtle Jones, USGS, Tacoma, WA, personal
     communication, 1994; Jones derived this grid from published point
     and contour bathymetry)

     12) GSC_1KM: One-km grid supplied by Dave Seeman and Tark
     Hamilton, Geological Survey of Canada-Victoria (personal
     communication, 1994). Projected, converted to a TIN, gridded, and
     smoothed. See http://gdcinfo.agg.nrcan.gc.ca/cat/cateng.html for
     information on purchase of this data

     13) MILBANKEPATCH: Defect in GSC_1KM repaired with data from
     Canadian Hydrographic Service (1993). Point depths digitized,
     projected, and gridded with TOPOGRID.

     14) Digital 1:1,000,000 contours, 100-m contour interval, of NE
     Pacific (prepared by Florence Wong, USGS, from data of Grim and
     others, 1992 and Chase and others, 1992) supplemented in areas
     with no contour control by point data from 1500-meter grid (RIDGE
     Web server) and, outside extent of 1500 m RIDGE grid, ETOPO5
     (National Geophysical Data Center, 1993)

     15) RIDGE 1500-m grid

     16) ETOPO5 (National Geophysical Data Center, 1993)

     Data from 14, 15, and 16 were projected, masked/merged, and then
     gridded using ANUDEM version 4.4 (Hutchison, 1989; drainage
     enforcement off):

     17) NOYO_PATCH: Small area at head of Noyo Canyon, at edge of
     northern California continental shelf. Filled by interpolation
     from surrounding areas with TOPOGRID (ARC/INFO 7.0.3, drainage
     enforcement off)

References Cited

Canadian Hydrographic Service, 1993, Milbanke Sound: Map 3728, scale
1:76,557.

Chase, T.E., Wilde, P., Normark, W.R., Evenden, G.I., Miller, C.P.,
Seekins,
B.A., Young, J.D., Grim, M.S., and Lief, C.J., 1992, Map showing bottom
topography of the Pacific continental margin, Cape Mendocino to Point
Conception: U.S. Geological Survey Map I-2090-C, scale 1:1,000,000.

Grim, M.S., Chase, T.E., Evenden, G.I., Holmes, M.L., Normark, W.R., Wilde,

P., Fox, C.J., Lief, C.J., and Seekins, B.A., 1992, Map showing bottom
topography of the Pacific continental margin, Strait of Juan de Fuca to
Cape
Mendocino: U.S. Geological Survey Map I-2091-C, scale 1:1,000,000.

Hutchinson, M.F., 1989, A new method for gridding elevation and stream line

data with automatic removal of pits: Journal of Hydrology, v. 106, p.
211-232.
See also http://cres.anu.edu.au/software/anudem.html

National Geophysical Data Center, 1993, Global Relief Data on CD-ROM: See
http://www.ngdc.noaa.gov/mgg/fliers/93mgg01.html

National Geophysical Data Center, 1998, NOS hydrographic survey data, US
Coastal Waters: see http://www.ngdc.noaa.gov/mgg/fliers/98mgg03.html

U.S. Coast and Geodetic Survey, 1969, 1:250,000-scale bathymetric chart
1308N-12, Point St. George to Point Delgada, 10-meter contour interval.

Addresses of Data Sources

EDCFTP: anonymous ftp from edcftp.cr.usgs.gov, see directories pub/data/DLG

and pub/data/DEM (ftp://edcftp.cr.usgs.gov/pub/data/DLG/100K,
ftp://edcftp.cr.usgs.gov/pub/data/DEM/250)

Geomatics Canada: See http://www.geocan.NRCan.gc.ca/

RIDGE Web Server: See
http://imager.ldeo.columbia.edu/ridgembs/ne_pac/html/home.html

USGS: phone 1-800-USA-MAPS, or http://edcwww.cr.usgs.gov/dsprod/prod.html

WDNR: Washington Department of Natural Resources, Olympia, WA 98504, phone
360-902-1000

