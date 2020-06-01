# Maputo-Population

Describe population estimate method

> CIESIN used proportional allocation to distribute population data from subnational census data to the settlement extents.
(CIESIN - https://ciesin.columbia.edu/data/hrsl/)

Image with the result. For our work the detail of those data very useful considering HRSL (pixel 30m per 30m), but absolutely inconsistence for the population estimated. Columbia university applied census data to hrsl.
So we developed something very similar, but considering updated CENSUS data and weighting the result in order to give more detail.

HRSL identify wether or not there is a building. It not consider if there is just one building or many buildings inside. For sure, for one HRSL pixel exist at least one building

Consider buildings from OSM and Google maps. OSM very precise just in small areas, where they are mapped. Google low precision, but wider areas. Much more precision in periphery (exactly the opposite of OSM).

Consider the division into morphological areas.

DENSITY: Count the number of HRSL pixel for each area. Count the number of buildings for each areas, both for OSM and Google maps sources. Manually for each area, we decided the reliability about buildings data. In some area OSM much more precise, in other Google maps, in still other none.

DENSITY 2: Buildings/HRSL (must be >= 1). To calculate this density we used OSM buildings or Google buildings where they are reliable - correct.
In the case where both are wrong or absents - the number of buildings is estimated as the minumum value buildings per HRSL of the same morphological class (at least 1).

RESIDENTIAL BUILDINGS. Excluding of industrial buildings.

Population per district from INE (2017 Census data)

Buildings per district (estimated - sum of buildings from morphological area in the same district)

I can easily estimate Pop / buildings.
I can easily estimate the Pop for each area.

NO, following has no sense: Can I refine the data considering average people/buildings in the district? By now has been considered homogeneous. No sense!

## References
Bonafilia, D., Kirsanov, D., Gill, J., & Sundram, J. (2019, April 09). Mapping the world to help aid workers, with weakly, semi-supervised learning. Retrieved from Facebook Artificial Intelligence: https://ai.facebook.com/blog/mapping-the-world-to-help-aid-workers-with-weakly-semi-supervised-learning

Tiecke, T. (2016, Novembar 15). Open population datasets and open challenges. Retrieved from Facebook Engineering: https://engineering.fb.com/connectivity/open-population-datasets-and-open-challenges/
