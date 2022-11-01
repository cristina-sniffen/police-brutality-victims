# Police Killings
Source of the Data: https://github.com/fivethirtyeight/data/tree/master/police-killings.

To investigate disproportionality by race and socio-economic status in police brutality victims across US states, we used the Police Killings dataset by FiveThirtyEight.

The database links entries from the 2015 Guardian's database on police killings (http://www.theguardian.com/us-news/ng-interactive/2015/jun/01/the-counted-map-us-police-killings) to census data from the American Community Survey. The Guardian data was downloaded on June 2, 2015. 

Census data was calculated at the tract level from the 2015 5-year American Community Survey using the tables `S0601 (demographics)`, `S1901 (tract-level income and poverty)`, `S1701 (employment and education)` and `DP03 (county-level income)`. Census tracts were determined by geocoding addresses to latitude/longitude using the Bing Maps and Google Maps APIs and then overlaying points onto 2014 census tracts.

For state level analysis, we utilized the tidycensus package to get access to the 2015 1-year American Community Survey variables- `B02001_001 (estimate State Population)`, `B02001_002 (estimate White alone)`, `B02001_003 (estimate Black alone)`, `B02001_004 (estimate Native American or Alaska Native alone)`, `B02001_005 (estimate Asian alone)`, `B02001_006 (estimate Native Hawaiian and Other Pacific Islander alone)`, `B03002_012 (estimate Hispanic/Latino alone)` 
Note: tidycensus::get_acs() function call has been made within the rmd and hence these variables are not available in the csv file.

Field descriptions:

Header | Description | Source
---|-----------|----
`name` | Name of deceased | Guardian
`age` | Age of deceased | Guardian
`gender` | Gender of deceased | Guardian
`raceethnicity` | Race/ethnicity of deceased | Guardian
`month` | Month of killing | Guardian
`day` | Day of incident | Guardian
`year` | Year of incident | Guardian
`streetaddress` | Address/intersection where incident occurred | Guardian
`city` | City where incident occurred | Guardian
`state` | State where incident occurred | Guardian
`latitude` | Latitude, geocoded from address | 
`longitude` | Longitude, geocoded from address | 
`state_fp` | State FIPS code | Census
`county_fp` | County FIPS code | Census
`tract_ce` | Tract ID code | Census
`geo_id` | Combined tract ID code | 
`county_id` | Combined county ID code | 
`namelsad` | Tract description | Census
`lawenforcementagency` | Agency involved in incident | Guardian
`cause` | Cause of death | Guardian
`armed` | How/whether deceased was armed | Guardian
`pop` | Tract population | Census
`share_white` | Share of pop that is non-Hispanic white | Census
`share_bloack` | Share of pop that is black (alone, not in combination) | Census
`share_hispanic` | Share of pop that is Hispanic/Latino (any race) | Census
`p_income` | Tract-level median personal income | Census
`h_income` | Tract-level median household income | Census
`county_income` | County-level median household income | Census
`comp_income` | `h_income` / `county_income` | Calculated from Census 
`county_bucket` | Household income, quintile within county | Calculated from Census
`nat_bucket` | Household income, quintile nationally | Calculated from Census
`pov` | Tract-level poverty rate (official) | Census
`urate` | Tract-level unemployment rate | Calculated from Census
`college` | Share of 25+ pop with BA or higher | Calculated from Census
`population` | Population of each state | American Community Survey 2015
`white` | (state-level) Estimate white individuals alone | American Community Survey 2015
`black` | (state-level) Estimate black individuals alone | American Community Survey 2015
`hispanic` | (state-level) Estimate hispanic individuals alone | American Community Survey 2015
`native_amer` | (state-level) Estimate native american or alaskan native individuals alone | American Community Survey 2015
`asian` | (state-level) Estimate asian individuals alone | American Community Survey 2015
`nh.pi` | (state-level) Estimate native hawaiian/pacific islander individuals alone | American Community Survey 2015
`geometry` | Geometry of US States | Tidycensus


<b>Note regarding income calculations:</b>

All income fields are in inflation-adjusted 2013 dollars.

`comp_income` is simply tract-level median household income as a share of county-level median household income.

`county_bucket` provides where the tract's median household income falls in the distribution (by quintile) of all tracts in the county. (1 indicates a tract falls in the poorest 20% of tracts within the county.) Distribution is not weighted by population.

`nat_bucket` is the same but for all U.S. counties.
