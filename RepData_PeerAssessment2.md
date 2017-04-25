# RepData_PeerAssessment2
by Fabio Bianchini  
XX/XX/2017  


The following timelines show the different time spans for each period of unique data collection and processing procedures. Select below for detailed decriptions of each data collection type. 
<https://www.ncdc.noaa.gov/stormevents/details.jsp>



Loading and Processing the Raw Data

```r
url <- "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2FStormData.csv.bz2"
download(url, "Storm_Data.bz2", mode = "wb") #Download dataset from specific URL
```


```r
bunzip2("Storm_Data.bz2", "Storm_data.csv", remove = FALSE, skip = TRUE) # unzip data file
```

```
## [1] "Storm_data.csv"
## attr(,"temporary")
## [1] FALSE
```

```r
Storm_Data <- read.csv("Storm_data.csv") #
Storm_Data <- as_tibble(Storm_Data)
str(Storm_Data)
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	902297 obs. of  37 variables:
##  $ STATE__   : num  1 1 1 1 1 1 1 1 1 1 ...
##  $ BGN_DATE  : Factor w/ 16335 levels "1/1/1966 0:00:00",..: 6523 6523 4242 11116 2224 2224 2260 383 3980 3980 ...
##  $ BGN_TIME  : Factor w/ 3608 levels "00:00:00 AM",..: 272 287 2705 1683 2584 3186 242 1683 3186 3186 ...
##  $ TIME_ZONE : Factor w/ 22 levels "ADT","AKS","AST",..: 7 7 7 7 7 7 7 7 7 7 ...
##  $ COUNTY    : num  97 3 57 89 43 77 9 123 125 57 ...
##  $ COUNTYNAME: Factor w/ 29601 levels "","5NM E OF MACKINAC BRIDGE TO PRESQUE ISLE LT MI",..: 13513 1873 4598 10592 4372 10094 1973 23873 24418 4598 ...
##  $ STATE     : Factor w/ 72 levels "AK","AL","AM",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ EVTYPE    : Factor w/ 985 levels "   HIGH SURF ADVISORY",..: 834 834 834 834 834 834 834 834 834 834 ...
##  $ BGN_RANGE : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ BGN_AZI   : Factor w/ 35 levels "","  N"," NW",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ BGN_LOCATI: Factor w/ 54429 levels ""," Christiansburg",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ END_DATE  : Factor w/ 6663 levels "","1/1/1993 0:00:00",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ END_TIME  : Factor w/ 3647 levels ""," 0900CST",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ COUNTY_END: num  0 0 0 0 0 0 0 0 0 0 ...
##  $ COUNTYENDN: logi  NA NA NA NA NA NA ...
##  $ END_RANGE : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ END_AZI   : Factor w/ 24 levels "","E","ENE","ESE",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ END_LOCATI: Factor w/ 34506 levels ""," CANTON"," TULIA",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ LENGTH    : num  14 2 0.1 0 0 1.5 1.5 0 3.3 2.3 ...
##  $ WIDTH     : num  100 150 123 100 150 177 33 33 100 100 ...
##  $ F         : int  3 2 2 2 2 2 2 1 3 3 ...
##  $ MAG       : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ FATALITIES: num  0 0 0 0 0 0 0 0 1 0 ...
##  $ INJURIES  : num  15 0 2 2 2 6 1 0 14 0 ...
##  $ PROPDMG   : num  25 2.5 25 2.5 2.5 2.5 2.5 2.5 25 25 ...
##  $ PROPDMGEXP: Factor w/ 19 levels "","-","?","+",..: 17 17 17 17 17 17 17 17 17 17 ...
##  $ CROPDMG   : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ CROPDMGEXP: Factor w/ 9 levels "","?","0","2",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ WFO       : Factor w/ 542 levels ""," CI","%SD",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ STATEOFFIC: Factor w/ 250 levels "","ALABAMA, Central",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ ZONENAMES : Factor w/ 25112 levels "","                                                                                                               "| __truncated__,..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ LATITUDE  : num  3040 3042 3340 3458 3412 ...
##  $ LONGITUDE : num  8812 8755 8742 8626 8642 ...
##  $ LATITUDE_E: num  3051 0 0 0 0 ...
##  $ LONGITUDE_: num  8806 0 0 0 0 ...
##  $ REMARKS   : Factor w/ 436781 levels "","\t","\t\t",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ REFNUM    : num  1 2 3 4 5 6 7 8 9 10 ...
```


```r
dim(Storm_Data) # Dataset dimension
```

```
## [1] 902297     37
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

Process/transform the data into a format suitable for your analysis


```r
ds1 <- Storm_Data
# variable must have a unique name in the dataset
names(ds1)[names(ds1)=="STATE__"] <- "STATE_NUM"
names(ds1)[names(ds1)=="LONGITUDE_"] <- "LONGITUDE_E"
names(ds1) <- str_to_lower(names(ds1)) # Force lowercase dataset columb names
names(ds1) <-str_replace(names(ds1), "_+$","") # Remove final underscore from columb names
names(ds1) <- str_replace(names(ds1), "_",".") #
names(ds1)
```

```
##  [1] "state.num"   "bgn.date"    "bgn.time"    "time.zone"   "county"     
##  [6] "countyname"  "state"       "evtype"      "bgn.range"   "bgn.azi"    
## [11] "bgn.locati"  "end.date"    "end.time"    "county.end"  "countyendn" 
## [16] "end.range"   "end.azi"     "end.locati"  "length"      "width"      
## [21] "f"           "mag"         "fatalities"  "injuries"    "propdmg"    
## [26] "propdmgexp"  "cropdmg"     "cropdmgexp"  "wfo"         "stateoffic" 
## [31] "zonenames"   "latitude"    "longitude"   "latitude.e"  "longitude.e"
## [36] "remarks"     "refnum"
```



```r
# Remove the observation with no interest for answer the question fo this analysis
#ds2 <- ds1[ds1$fatalities > 0 | ds1$injuries > 0 | ds1$cropdmg > 0 | ds1$propdmg > 0,] 
ds2 <- ds1[ds1$fatalities > 0 | ds1$injuries > 0,] 
dim(ds2)
```

```
## [1] 21929    37
```
#####1. Across the United States, which types of events (as indicated in the 𝙴𝚅𝚃𝚈𝙿𝙴 variable) are most harmful with respect to population health?

We assume that the variable of interest, for analazing the impact on population healt, present in the dataset are:
- fatalites 
- injuries 
so we create a subset from the original dataset with only the variable of interest.


```r
# Create a dataset with only the columb/variable of interest to answer the question
ds3 <- select(ds2, fatalities, injuries, evtype)
# Force all `evtypes` to uppercase 
ds3$evtype <- str_to_upper(ds3$evtype)
# replace multiple spaces with single space
ds3$evtype <- gsub(" +", " ", ds3$evtype)
dim(table(ds3$evtype))
```

```
## [1] 204
```

```r
ds4 <- ds3 %>% group_by(evtype) %>% summarise(tot.fatalities = sum(fatalities), tot.injuries = sum(injuries))
dim(ds4) # 
```

```
## [1] 204   3
```


```r
fatalities <- arrange(ds4, desc(tot.fatalities))
mean(fatalities$tot.fatalities) # Mean value for fatalities
```

```
## [1] 74.2402
```


```r
plot_fatalities <- fatalities[fatalities$tot.fatalities > mean(fatalities$tot.fatalities), ]
nrow(plot_fatalities) # Events with n. of fatalities greater that the mean
```

```
## [1] 25
```

```r
ggplot(plot_fatalities, aes(tot.fatalities, fct_reorder(evtype, tot.fatalities))) + geom_point() + labs(title="Total fatalities by storm type", x="N. fatalities", y="", caption = "") 
```

![](RepData_PeerAssessment2_files/figure-html/plot total fatalities by Storm-1.png)<!-- -->


```r
injuries <- arrange(ds4, desc(tot.injuries))
mean(injuries$tot.injuries) # Mean value for injuries
```

```
## [1] 688.8627
```


```r
plot_injuries <- injuries[injuries$tot.injuries > mean(injuries$tot.injuries), ]
nrow(plot_injuries) # Events with n. of injuries > mean(injuries)
```

```
## [1] 18
```

```r
ggplot(plot_injuries, aes(tot.injuries, fct_reorder(evtype, tot.injuries))) + geom_point() + labs(title="Total injuries by Storm Type", x="N.injuries", y="") 
```

![](RepData_PeerAssessment2_files/figure-html/plot total injuries by Storm-1.png)<!-- -->



```r
# Create a vector for all the possible Event Types (48 from Directive 10-1605)
evtype.group <- c("Astronomical Low Tide", "Avalanche","Blizzard", "Coastal Flood", "Cold Wind Chill", "Debris Flow", "Dense Fog","Dense Smoke", "Drought", "Dust Devil", "Dust Storm", "Excessive Heat", "Extreme Cold Wind Chill", "Flash Flood ", "Flood", "Frost Freeze", "Freezing Fog","Funnel Cloud", "Hail", "Heat", "Heavy Rain","Heavy Snow", "High Surf", "High Wind", "Hurricane Typhoon", "Ice Storm", "Lakeshore Flood", "Lake Effect Snow", "Lightning", "Marine Hail", "Marine High Wind", "Marine Strong Wind","Marine Thunderstorm Wind","Rip Current", "Seiche", "Sleet","Storm Surge Tide", "Strong Wind", "Thunderstorm Wind", "Tornado", "Tropical Depression", "Tropical Storm", "Tsunami", "Volcanic Ash", "Waterspout", "Wildfire", "Winter Storm", "Winter Weather")
evtype.group <- str_to_upper(evtype.group)
evtype.group <- gsub(" ", "|", evtype.group)
evtype.group
```

```
##  [1] "ASTRONOMICAL|LOW|TIDE"    "AVALANCHE"               
##  [3] "BLIZZARD"                 "COASTAL|FLOOD"           
##  [5] "COLD|WIND|CHILL"          "DEBRIS|FLOW"             
##  [7] "DENSE|FOG"                "DENSE|SMOKE"             
##  [9] "DROUGHT"                  "DUST|DEVIL"              
## [11] "DUST|STORM"               "EXCESSIVE|HEAT"          
## [13] "EXTREME|COLD|WIND|CHILL"  "FLASH|FLOOD|"            
## [15] "FLOOD"                    "FROST|FREEZE"            
## [17] "FREEZING|FOG"             "FUNNEL|CLOUD"            
## [19] "HAIL"                     "HEAT"                    
## [21] "HEAVY|RAIN"               "HEAVY|SNOW"              
## [23] "HIGH|SURF"                "HIGH|WIND"               
## [25] "HURRICANE|TYPHOON"        "ICE|STORM"               
## [27] "LAKESHORE|FLOOD"          "LAKE|EFFECT|SNOW"        
## [29] "LIGHTNING"                "MARINE|HAIL"             
## [31] "MARINE|HIGH|WIND"         "MARINE|STRONG|WIND"      
## [33] "MARINE|THUNDERSTORM|WIND" "RIP|CURRENT"             
## [35] "SEICHE"                   "SLEET"                   
## [37] "STORM|SURGE|TIDE"         "STRONG|WIND"             
## [39] "THUNDERSTORM|WIND"        "TORNADO"                 
## [41] "TROPICAL|DEPRESSION"      "TROPICAL|STORM"          
## [43] "TSUNAMI"                  "VOLCANIC|ASH"            
## [45] "WATERSPOUT"               "WILDFIRE"                
## [47] "WINTER|STORM"             "WINTER|WEATHER"
```

ggplot(data = diamonds) +
          geom_bar(
            mapping = aes(x = cut, fill = clarity),
            position = "dodge"
          )
          
Now we assign a precise even type at each observation in the Dataset 

#####2. Across the United States, which types of events have the greatest economic consequences?

We assume that the variable of interest, for greatest economic consequences, present in the dataset are:
- propdmg (Property damage)
- cropdmg (Crop damage)
