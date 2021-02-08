# Problem Dataset 
The following document contains key map locations and APIs utilized for the project. All of the following data is publically available and it has been configured to fit our narative.  

**Chosen Location**: North York, Ontario, Canada

**Brief Summary** 

We use the osmnx API to get information about the nodes and edges contained in the map of North York. Locations of fire stations and hospitals are identified using the Overpass scripts. We are also collecting live and historical accident and construction locations to identify the optimal path for an emergency vehicle to meet a crucial response time. We have utilized the Bing Traffic API to capture all the accident and construction zones that have occurred within the time frame of 3 weeks. This is the historical data for the project. We have used the weighted-KNN algorithm on this data to help us capture the zones of busy areas on the map. In addition, we acquire live accident data using the Bing Traffic API and then use it to identify the busy streets. We plan to design an algorithm that integrates all these data to fine-tune the routing of emergency vehicles. The objectives considered include minimizing the total travel time to a dispatch location while eliminating busy areas, which is what the public is concerned with the most.     

Outlined below is a detailed summary of the data we have utlizied and captured for this project. 

## Geospatial Datasets

### Amenities - Using `Overpass turbo`'s Wizard 

For our problem, we need Fire Stations and Hospitals. Hence, the following is utilized. 

The following `Overpass turbo`'s wizard synatx and script:
* Firestations in North York 
  * **`amenity= fire_station in "North York, Ontario, Canada"`** to find all Firestations in North York. 
  * [Script](./Dataset/scripts/firestations_northyork.oql) 
* Hospitals in North York 
  * **`amenity= hospital in "North York, Ontario, Canada"`** to find all Firestations in North York. 
  * [Script](./Dataset/scripts/hospitals_northyork.oql)


### Traffic data - Using `Bing Traffic API`

* Live traffic incident data in North York
  * Using our **custom** `BingTrafficIncidentsApi`
  * Source code: [`bing_traffic/bing_traffic_incidents_api.py:get_live_traffic_incidents(..)`](https://github.com/singh264/smart-mobility/blob/master/bing_traffic/bing_traffic_incidents_api.py) 
  * We take a snapshot and return a list of the current live incidents in North York. These incidents are used to assign a risk score for each edge on the North York map that is near the traffic incident. Finally, this data is used again to send out emergency dispatch to locations where the most severe accidents occured.

* Historical traffic incident data in North York
  * Using our **custom** `BingTrafficIncidentsApi`
  * Source code: [`bing_traffic/bing_traffic_incidents_api.py:download_traffic_incidents(..)`](https://github.com/singh264/smart-mobility/blob/master/bing_traffic/bing_traffic_incidents_api.py)
  * All historical traffic incident data can be found on our [Drive](https://drive.google.com/drive/folders/1ObGRrqJbvuVqW3wQDg16Wnjh-9BA0K04)
    * The above data contains the timestamp, origin latitude, origin longitude, destination latitude, destination longitude and the severity of each traffic incident. The traffic data is extracted and saved to a seperate json file every hour. Then, all of the traffic incident data is merged into one csv file per region (or bounding box) that is configured in the BingTrafficIncidentsApi configuration. For each region, the json files are merged into a csv file so that our weighted knn algorithm can consume the data easily. The clustering is weighted based on the severity of each traffic incident. 


### Map edges coordinates data - Using `Osmapi`

* Edges coordinates in North York
  * Using our **custom** `MapEdgesCoordinatesDowloader`
  * Source code: [`map/map_edges_coordinates_downloader.py:download_edges_coordinates(..)`](https://github.com/singh264/smart-mobility/blob/master/map/map_edges_coordinates_downloader.py) 
  * All edges coordinates data can be found on our [Drive](https://drive.google.com/drive/folders/1ObGRrqJbvuVqW3wQDg16Wnjh-9BA0K04)
    * The above data is created to reduce the run-time of the application. Rather than mapping each osmid to its latitude and longitude during runtime, we do this ahead of time to save call to OsmApi each time. This improves the overhead performance significantly, and it will be useful for demo purposes.
  
  
