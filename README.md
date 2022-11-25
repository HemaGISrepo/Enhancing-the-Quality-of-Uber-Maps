# Enhancing-the-Quality-of-Uber-Maps-with-Metrics-Computation

On the surface, Uber’s ridesharing technology may seem simple: a user requests a ride from the app, and a driver arrives to take them to their destination. Behind the scenes, however, a giant infrastructure consisting of thousands of services and terabytes of data supports each and every trip on the platform.

Rather than the simple, two-dimensional representations people see when they look at the Uber app, a map is actually a complex data structure. In computational terms, we need to define the size of each geographical portion of a map, as well as decide which objects are included/displayed on a map.

How Uber defines a map region

Before we can compute and report map quality metrics, we first need to define our map regions. For example, we might be interested in the map quality of North America, or the state of California, or Santa Clara County, or even just the most urban (and trafficked) areas of the city of San Francisco.

Before Uber launches operations in a new area, we define and onboard a new region to our map technology stack. Inside this map region, we define subregions labeled with grades A, B, AB, and C, as follows:

Grade A: A subregion of Uber Territory covering urban centers and commute areas that make up approximately 90 percent of all expected Uber traffic. With that in mind, it is of critical importance to ensure the highest map quality of grade A map regions.

Grade B: A subregion of Uber Territory covering rural and suburban areas that might be less populated or less traveled by Uber customers.

Grade AB: A union of grade A and B subregions.

Grade C: A set of highway corridors connecting various Uber Territories


UBER MAP MODEL:

Maps are intuitively defined by their purpose. A map orients us in space, letting us see where we are in the world. With a map, we can also navigate from where we are to where we want to go.
From the perspective of determining map quality, we define a map as a collection of map features, from man-made places like road segments, junctions, and buildings to natural features such as mountains, lakes, and oceans. Further, for Uber-specific use cases, we include access points, which specify allowed or preferred pick-up and drop-off locations for a certain address point, as map features. For example, access points at the San Francisco International Airport include a set of terminals, gates, and airport-determined  gathering spots.

Finally, each map feature has a set of attributes that fully describe it. For example, a road segment’s attributes include geometry, length, name, road class (local road? highway?), and usage (road? bike path?).

Map features and attributes form a data structure which we call the Uber Map Model (UMM). We can visualize the UMM as layers of map features that collectively create a map.

![image](https://user-images.githubusercontent.com/118595650/204042607-76d2b959-98f8-4f70-9045-3a0e21ee9131.png)


DETERMINING MAP QUALITY:

Map quality means different things to different map users. For example, imaging tools such as Google Earth and Esri’s ArcGIS Earth might focus on the accuracy of map labels or the aesthetics of map cartography, i.e., how each map tiles looks. For Uber’s most basic use case, ridesharing, map quality metrics must answer questions such as:

Do we have enough roads? Are we classifying them correctly?
Are we picking up and dropping off our riders at the right locations?
Are we navigating drivers on optimal routes?
Do we have the addresses and locations that people are taking trips to?
Are our road names accurate, and do they reflect local usage?
The full set of metrics we use in our maps are too numerous to list, but we can divide them into simple and comparative coverage metrics. Simple metrics include roads, unique route counts, signpost counts, turn restrictions, and number of lanes per road. We compute these metrics by simply analyzing map data as a single input. A more complex set of metrics we take into account, comparative coverage, uses two inputs: map data being processed for quality and reference map data.

Both simple and comparative metrics are computed automatically by using powerful data processing frameworks. However, some metrics are more difficult or even impossible to automate: are the pitch and timing of voice prompts for navigation correct and user-friendly? Are the map tiles displayed in an aesthetically pleasing manner? Are the street labels clear and readable? To get such answers/metrics, we conduct map quality evaluation drives, for which we create evaluation surveys in the form of multiple choice questions. The results of these surveys are then processed and aggregated into metrics.

Regardless of their categorization, all metrics computation must be accurate, execute reasonably fast, reliably generate output, and scale with no issues. Scaling is especially important, as a fatal error of a certain region’s metrics computation must not affect metrics computation in other regions.


