### SETUP


JUPYTER WORKBOOKS

* coordinates_grid.ipynb - Creates grid of GPS coordinates covering the Bay Area, then stores in grid_coordinates2.csv

* calls_by_coord.ipynb - Makes API calls using coordinates in grid_coordinates2.csv and stores results in Resources folder as restaurant_data.csv. Note: multiple coordinates over 1k results cap, warranting additional queries on the pair to ensure valid results were not missed (see below)

* calls_for_2_coords_rating_ver2.ipynb - Makes additional queries on the multiple coordinates identified above, with ratings sort adjustment and stores in restaurant_data_ratings.csv. Provides extra assurance that top restaurants in those busy areas are represented in final dataset.


RESOURCES

* grid_coordinates.csv - Coordinates for a grid covering Bay Area with 3 mi intervals. Broken up over 5 csv files due to encuntering issues with Yelp API when searching the entire 1300+ set of geocoordinates

* restaurant_data.csv - Raw dataset from Yelp API that contains all restaurants in Bay Area, except limited results from multiple coordinates. Broken up over 5 csv files corresponding to the 5 grid_coordinates csv files

* restaurant_data_ratings.csv - Raw dataset of the top-1k restaurants for each of the 2 coordinates with limited results in restaurants_data_coords3.csv



### METHODOLOGY


1. Run coordinates_grid.ipynb to create grid of coordinates. Bay Area boundaries are hard-coded  and can be replaced as desired. The interval between coordinates is also hard-coded and set to 3 miles (4.82803 km).

2. Run calls_by_coords_ver2.ipynb, which takes in coordinates_grid2.csv created in step 1, and makes Yelp API calls using hard-coded search radius of 2.12 miles. For each result in a query, the following information is extracted:

- restaurant name
- address/city/zipcode
- coordinates
- rating
- review count
- price level
- category array
- yelp id

3. calls_by_coords_ver2.ipynb in step 2 also tracks total restaurants count for each query. The dataframe is sorted at bottom of workbook for quick identification of any queries exceeding 1k results. If a significant % of queries exceeds the 1k max, a tighter search radius AND/OR set of coordinates may be required before restarting the API calls.

4. Given that only a fraction of 1% of coordinates in this example exceeded 1k, no amount of adjusting of parameters in original code will extract 100% of results in reasonable time. In this case, running call_by_coords_rating_ver2.ipynb will suffice in supplementing initial API calls. Other supplemental methods may be required for different situations.

5. Merging of both csv from steps 2 and 3 is detailed in data cleaning section
