# RepData_PeerAssessment2
by Fabio Bianchini  
18/04/2017  



## Including Code 


1) - Loading and Processing the Raw Data



```r
bunzip2("Storm_Data.bz2", "Storm_data.csv", remove = FALSE, skip = TRUE)
```

```
## [1] "Storm_data.csv"
## attr(,"temporary")
## [1] FALSE
```

```r
Storm_Data <- read.csv("Storm_data.csv")
```


```r
names(Storm_Data)
```

```
##  [1] "STATE__"    "BGN_DATE"   "BGN_TIME"   "TIME_ZONE"  "COUNTY"    
##  [6] "COUNTYNAME" "STATE"      "EVTYPE"     "BGN_RANGE"  "BGN_AZI"   
## [11] "BGN_LOCATI" "END_DATE"   "END_TIME"   "COUNTY_END" "COUNTYENDN"
## [16] "END_RANGE"  "END_AZI"    "END_LOCATI" "LENGTH"     "WIDTH"     
## [21] "F"          "MAG"        "FATALITIES" "INJURIES"   "PROPDMG"   
## [26] "PROPDMGEXP" "CROPDMG"    "CROPDMGEXP" "WFO"        "STATEOFFIC"
## [31] "ZONENAMES"  "LATITUDE"   "LONGITUDE"  "LATITUDE_E" "LONGITUDE_"
## [36] "REMARKS"    "REFNUM"
```

```r
head(Storm_Data)
```

```
##   STATE__           BGN_DATE BGN_TIME TIME_ZONE COUNTY COUNTYNAME STATE
## 1       1  4/18/1950 0:00:00     0130       CST     97     MOBILE    AL
## 2       1  4/18/1950 0:00:00     0145       CST      3    BALDWIN    AL
## 3       1  2/20/1951 0:00:00     1600       CST     57    FAYETTE    AL
## 4       1   6/8/1951 0:00:00     0900       CST     89    MADISON    AL
## 5       1 11/15/1951 0:00:00     1500       CST     43    CULLMAN    AL
## 6       1 11/15/1951 0:00:00     2000       CST     77 LAUDERDALE    AL
##    EVTYPE BGN_RANGE BGN_AZI BGN_LOCATI END_DATE END_TIME COUNTY_END
## 1 TORNADO         0                                               0
## 2 TORNADO         0                                               0
## 3 TORNADO         0                                               0
## 4 TORNADO         0                                               0
## 5 TORNADO         0                                               0
## 6 TORNADO         0                                               0
##   COUNTYENDN END_RANGE END_AZI END_LOCATI LENGTH WIDTH F MAG FATALITIES
## 1         NA         0                      14.0   100 3   0          0
## 2         NA         0                       2.0   150 2   0          0
## 3         NA         0                       0.1   123 2   0          0
## 4         NA         0                       0.0   100 2   0          0
## 5         NA         0                       0.0   150 2   0          0
## 6         NA         0                       1.5   177 2   0          0
##   INJURIES PROPDMG PROPDMGEXP CROPDMG CROPDMGEXP WFO STATEOFFIC ZONENAMES
## 1       15    25.0          K       0                                    
## 2        0     2.5          K       0                                    
## 3        2    25.0          K       0                                    
## 4        2     2.5          K       0                                    
## 5        2     2.5          K       0                                    
## 6        6     2.5          K       0                                    
##   LATITUDE LONGITUDE LATITUDE_E LONGITUDE_ REMARKS REFNUM
## 1     3040      8812       3051       8806              1
## 2     3042      8755          0          0              2
## 3     3340      8742          0          0              3
## 4     3458      8626          0          0              4
## 5     3412      8642          0          0              5
## 6     3450      8748          0          0              6
```

```r
tail(Storm_Data)
```

```
##        STATE__           BGN_DATE    BGN_TIME TIME_ZONE COUNTY
## 902292      47 11/28/2011 0:00:00 03:00:00 PM       CST     21
## 902293      56 11/30/2011 0:00:00 10:30:00 PM       MST      7
## 902294      30 11/10/2011 0:00:00 02:48:00 PM       MST      9
## 902295       2  11/8/2011 0:00:00 02:58:00 PM       AKS    213
## 902296       2  11/9/2011 0:00:00 10:21:00 AM       AKS    202
## 902297       1 11/28/2011 0:00:00 08:00:00 PM       CST      6
##                                  COUNTYNAME STATE         EVTYPE BGN_RANGE
## 902292 TNZ001>004 - 019>021 - 048>055 - 088    TN WINTER WEATHER         0
## 902293                         WYZ007 - 017    WY      HIGH WIND         0
## 902294                         MTZ009 - 010    MT      HIGH WIND         0
## 902295                               AKZ213    AK      HIGH WIND         0
## 902296                               AKZ202    AK       BLIZZARD         0
## 902297                               ALZ006    AL     HEAVY SNOW         0
##        BGN_AZI BGN_LOCATI           END_DATE    END_TIME COUNTY_END
## 902292                    11/29/2011 0:00:00 12:00:00 PM          0
## 902293                    11/30/2011 0:00:00 10:30:00 PM          0
## 902294                    11/10/2011 0:00:00 02:48:00 PM          0
## 902295                     11/9/2011 0:00:00 01:15:00 PM          0
## 902296                     11/9/2011 0:00:00 05:00:00 PM          0
## 902297                    11/29/2011 0:00:00 04:00:00 AM          0
##        COUNTYENDN END_RANGE END_AZI END_LOCATI LENGTH WIDTH  F MAG
## 902292         NA         0                         0     0 NA   0
## 902293         NA         0                         0     0 NA  66
## 902294         NA         0                         0     0 NA  52
## 902295         NA         0                         0     0 NA  81
## 902296         NA         0                         0     0 NA   0
## 902297         NA         0                         0     0 NA   0
##        FATALITIES INJURIES PROPDMG PROPDMGEXP CROPDMG CROPDMGEXP WFO
## 902292          0        0       0          K       0          K MEG
## 902293          0        0       0          K       0          K RIW
## 902294          0        0       0          K       0          K TFX
## 902295          0        0       0          K       0          K AFG
## 902296          0        0       0          K       0          K AFG
## 902297          0        0       0          K       0          K HUN
##                       STATEOFFIC
## 902292           TENNESSEE, West
## 902293 WYOMING, Central and West
## 902294          MONTANA, Central
## 902295          ALASKA, Northern
## 902296          ALASKA, Northern
## 902297            ALABAMA, North
##                                                                                                                                                            ZONENAMES
## 902292 LAKE - LAKE - OBION - WEAKLEY - HENRY - DYER - GIBSON - CARROLL - LAUDERDALE - TIPTON - HAYWOOD - CROCKETT - MADISON - CHESTER - HENDERSON - DECATUR - SHELBY
## 902293                                                                              OWL CREEK & BRIDGER MOUNTAINS - OWL CREEK & BRIDGER MOUNTAINS - WIND RIVER BASIN
## 902294                                                                                     NORTH ROCKY MOUNTAIN FRONT - NORTH ROCKY MOUNTAIN FRONT - EASTERN GLACIER
## 902295                                                                                                 ST LAWRENCE IS. BERING STRAIT - ST LAWRENCE IS. BERING STRAIT
## 902296                                                                                                                 NORTHERN ARCTIC COAST - NORTHERN ARCTIC COAST
## 902297                                                                                                                                             MADISON - MADISON
##        LATITUDE LONGITUDE LATITUDE_E LONGITUDE_
## 902292        0         0          0          0
## 902293        0         0          0          0
## 902294        0         0          0          0
## 902295        0         0          0          0
## 902296        0         0          0          0
## 902297        0         0          0          0
##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        REMARKS
## 902292                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    EPISODE NARRATIVE: A powerful upper level low pressure system brought snow to portions of Northeast Arkansas, the Missouri Bootheel, West Tennessee and extreme north Mississippi. Most areas picked up between 1 and 3 inches of with areas of Northeast Arkansas and the Missouri Bootheel receiving between 4 and 6 inches of snow.EVENT NARRATIVE: Around 1 inch of snow fell in Carroll County.
## 902293                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           EPISODE NARRATIVE: A strong cold front moved south through north central Wyoming bringing high wind to the Meeteetse area and along the south slopes of the western Owl Creek Range. Wind gusts to 76 mph were recorded at Madden Reservoir.EVENT NARRATIVE: 
## 902294                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      EPISODE NARRATIVE: A strong westerly flow aloft produced gusty winds at the surface along the Rocky Mountain front and over the plains of Central Montana. Wind gusts in excess of 60 mph were reported.EVENT NARRATIVE: A wind gust to 60 mph was reported at East Glacier Park 1ENE (the Two Medicine DOT site).
## 902295 EPISODE NARRATIVE: A 960 mb low over the southern Aleutians at 0300AKST on the 8th intensified to 945 mb near the Gulf of Anadyr by 2100AKST on the 8th. The low crossed the Chukotsk Peninsula as a 956 mb low at 0900AKST on the 9th, and moved into the southern Chukchi Sea as a 958 mb low by 2100AKST on the 9th. The low then tracked to the northwest and weakened to 975 mb about 150 miles north of Wrangel Island by 1500AKST on the 10th. The storm was one of the strongest storms to impact the west coast of Alaska since November 1974. \n\nZone 201: Blizzard conditions were observed at Wainwright from approximately 1153AKST through 1611AKST on the 9th. The visibility was frequently reduced to one quarter mile in snow and blowing snow. There was a peak wind gust to 43kt (50 mph) at the Wainwright ASOS. During this event, there was also a peak wind gust to \n68 kt (78 mph) at the Cape Lisburne AWOS. \n\nZone 202: Blizzard conditions were observed at Barrow from approximately 1021AKST through 1700AKST on the 9th. The visibility was frequently reduced to one quarter mile or less in blowing snow. There was a peak wind gust to 46 kt (53 mph) at the Barrow ASOS. \n\nZone 207: Blizzard conditions were observed at Kivalina from approximately 0400AKST through 1230AKST on the 9th. The visibility was frequently reduced to one quarter of a mile in snow and blowing snow. There was a peak wind gust to 61 kt (70 mph) at the Kivalina ASOS.  The doors to the village transportation shed were blown out to sea.  Many homes lost portions of their tin roofing, and satellite dishes were ripped off of roofs. One home had its door blown off.  At Point Hope, severe blizzard conditions were observed. There was a peak wind gust of 68 kt (78 mph) at the Point Hope AWOS before power was lost to the AWOS. It was estimated that the wind gusted as high as 85 mph in the village during the height of the storm during the morning and early afternoon hours on the 9th. Five power poles were knocked down in the storm EVENT NARRATIVE: 
## 902296 EPISODE NARRATIVE: A 960 mb low over the southern Aleutians at 0300AKST on the 8th intensified to 945 mb near the Gulf of Anadyr by 2100AKST on the 8th. The low crossed the Chukotsk Peninsula as a 956 mb low at 0900AKST on the 9th, and moved into the southern Chukchi Sea as a 958 mb low by 2100AKST on the 9th. The low then tracked to the northwest and weakened to 975 mb about 150 miles north of Wrangel Island by 1500AKST on the 10th. The storm was one of the strongest storms to impact the west coast of Alaska since November 1974. \n\nZone 201: Blizzard conditions were observed at Wainwright from approximately 1153AKST through 1611AKST on the 9th. The visibility was frequently reduced to one quarter mile in snow and blowing snow. There was a peak wind gust to 43kt (50 mph) at the Wainwright ASOS. During this event, there was also a peak wind gust to \n68 kt (78 mph) at the Cape Lisburne AWOS. \n\nZone 202: Blizzard conditions were observed at Barrow from approximately 1021AKST through 1700AKST on the 9th. The visibility was frequently reduced to one quarter mile or less in blowing snow. There was a peak wind gust to 46 kt (53 mph) at the Barrow ASOS. \n\nZone 207: Blizzard conditions were observed at Kivalina from approximately 0400AKST through 1230AKST on the 9th. The visibility was frequently reduced to one quarter of a mile in snow and blowing snow. There was a peak wind gust to 61 kt (70 mph) at the Kivalina ASOS.  The doors to the village transportation shed were blown out to sea.  Many homes lost portions of their tin roofing, and satellite dishes were ripped off of roofs. One home had its door blown off.  At Point Hope, severe blizzard conditions were observed. There was a peak wind gust of 68 kt (78 mph) at the Point Hope AWOS before power was lost to the AWOS. It was estimated that the wind gusted as high as 85 mph in the village during the height of the storm during the morning and early afternoon hours on the 9th. Five power poles were knocked down in the storm EVENT NARRATIVE: 
## 902297                           EPISODE NARRATIVE: An intense upper level low developed on the 28th at the base of a highly amplified upper trough across the Great Lakes and Mississippi Valley.  The upper low closed off over the mid South and tracked northeast across the Tennessee Valley during the morning of the 29th.   A warm conveyor belt of heavy rainfall developed in advance of the low which dumped from around 2 to over 5 inches of rain across the eastern two thirds of north Alabama and middle Tennessee.  The highest rain amounts were recorded in Jackson and DeKalb Counties with 3 to 5 inches.  The rain fell over 24 to 36 hour period, with rainfall remaining light to moderate during most its duration.  The rainfall resulted in minor river flooding along the Little River, Big Wills Creek and Paint Rock.   A landslide occurred on Highway 35 just north of Section in Jackson County.  A driver was trapped in his vehicle, but was rescued unharmed.  Trees, boulders and debris blocked 100 to 250 yards of Highway 35.\n\nThe rain mixed with and changed to snow across north Alabama during the afternoon and  evening hours of the 28th, and lasted into the 29th.  The heaviest bursts of snow occurred in northwest Alabama during the afternoon and evening hours, and in north central and northeast Alabama during the overnight and morning hours.  Since ground temperatures were in the 50s, and air temperatures in valley areas only dropped into the mid 30s, most of the snowfall melted on impact with mostly trace amounts reported in valley locations.  However, above 1500 foot elevation, snow accumulations of 1 to 2 inches were reported.  The heaviest amount was 2.3 inches on Monte Sano Mountain, about 5 miles northeast of Huntsville.EVENT NARRATIVE: Snowfall accumulations of up to 2.3 inches were reported on the higher elevations of eastern Madison County.  A snow accumulation of 1.5 inches was reported 2.7 miles south of Gurley, while 2.3 inches was reported 3 miles east of Huntsville atop Monte Sano Mountain.
##        REFNUM
## 902292 902292
## 902293 902293
## 902294 902294
## 902295 902295
## 902296 902296
## 902297 902297
```

You can include R code in the document as follows:

2) - Process/transform the data (if necessary) into a format suitable for your analysis


## Including Plots

You can also embed plots, for example:


Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
