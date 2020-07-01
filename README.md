# Greater Maputo population estimate

This guide describe the methodology adopted to estimate the population in the Greater Maputo area.

### Data
- HRSL
- OSM buildings
- Google buildings
- INE Census data
- Morphological areas

### Existing population data
There are two main existing sources for population data in the Greater Maputo area.
The first one is the official census dataset provided by the *INE - Instituto Nacional de Estatistica* for the IV General Census of Population and Housing in 2017. The main problem of this dataset is the low resolution, infact the data are aggregated by province or by district.
The second source is *HRSL - High Resolution Settlement Layer*. This layer is developed by Facebook using AI and 2016 satellite images. It identifies populated areas with a resolution of 1 arcsec, around 30x30 meters, detecting whether there are buildings. 
CIENIS process HRSL data and INE census data applying growth rate to estimate population per HRSL pixel.

> CIESIN used proportional allocation to distribute population data from subnational census data to the settlement extents.
(CIESIN - https://ciesin.columbia.edu/data/hrsl/)

> Adjustments to match the census population with the UN estimates are applied at the national level. The UN estimate for a given country (or state/territory) is divided by the total census estimate of population for the given country. The resulting adjustment factor is multiplied by each administrative unit census value for the target year. This preserves the relative population totals across administrative units while matching the UN total.
So the population is considered equally distributed within the HRSL pixel of the same district or province. 

Issues that affect the neighbourhood scale: 
- data aggregated at the district or province level 
<img src="img/HRSL1-tot.PNG" width=300 />
- wrong overlapping with administrative boundaries
<img src="img/HRSL1-dist1.PNG" width=300 />

### Estimate population method

The existing population dataset are not very effective considering the scale we are dealing with. However, the resolution of HRSL pixel is high and provide a proper measure of density, identifying weather the people lives and are concentrated. Columbia university applied census data to HRSL homogeneously. In this methodology we considered updated CENSUS data, HRSL and the actual presence of buildings.
HRSL identify weather or not there are buildings, but it does not consider the actual number of buildings within each pixel. Surely for each HRSL pixel exist at least one building.

For Maputo does not exist any comprehensive buildings dataset, so we used buildings from OSM and Google maps. OSM buildings are very precise, but buildings are mapped just in the inner city. Google buildings have low precision in high density areas, where the buildings are smaller and close (as in the inner city), but they covered all the metropolitan areas with higher precision in the periphery.
We decided to estimate the population in the morphological areas, using INE census data, HRSL pixel - to have a comprehensive view of the entire metropolitan areas - and the buildings data in order to get more detail. 

The following items have been calculated first: 
-	*Hi* Count the number of HRSL pixel for the morphological area *i*.
-	*Bi* Count the number of buildings for the morphological area *i*. 

We checked the reliability of the second item in order to understand the most precise sources between OSM and Google maps, or if none of them are reliable.
The assumption is that two areas of the same morphological class have approximately the same number of buildings per HRSL pixel. Therefore, in areas where both sources are not reliable, has been applied the lowest value of buildings per HRSL pixel, measured within the same morphological classes’ areas (in which OSM or Google are reliable).
There is no data about use of buildings, so no way to exclude industrial or tertiary buildings. This information is controversial in Mozambique, because often the uses are not well defined and separated. In any case the areas identifiable as industrial have been excluded (no resident).

The number of buildings per each morphological areas in Greater Maputo (*Bi*) have been calculated. The population have been estimated counting the number of buildings within the census administrative areas (*Bj*) and therefore estimating the average people per buildings (*Pb*). Finally, this value has been multiplied for the total number of buildings in the morphological area to obtain the population living in that area.

*Pi = Pb* * *Bj*

*Pb = Pj* / *Bj*

*P* = population; *B* = buildings

*i* = morphological area; *j* = district/province


## References
Bonafilia, D., Kirsanov, D., Gill, J., & Sundram, J. (2019, April 09). Mapping the world to help aid workers, with weakly, semi-supervised learning. Retrieved from Facebook Artificial Intelligence: https://ai.facebook.com/blog/mapping-the-world-to-help-aid-workers-with-weakly-semi-supervised-learning

Tiecke, T. (2016, Novembar 15). Open population datasets and open challenges. Retrieved from Facebook Engineering: https://engineering.fb.com/connectivity/open-population-datasets-and-open-challenges/

Facebook Connectivity Lab and Center for International Earth Science Information Network - CIESIN - Columbia University. 2016. High Resolution Settlement Layer (HRSL). Source imagery for HRSL © 2016 DigitalGlobe. Accessed 03 June 2020.
