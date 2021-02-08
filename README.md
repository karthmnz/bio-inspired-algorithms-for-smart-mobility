# Graph-Search-Algorithms
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) [![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://GitHub.com/Naereen/StrapDown.js/graphs/commit-activity) [![GitHub contributors](https://img.shields.io/github/contributors/Naereen/StrapDown.js.svg)](https://github.com/singh264/smart-mobility/graphs/contributors) 
[![GitHub issues](https://img.shields.io/github/issues/Naereen/StrapDown.js.svg)](https://github.com/singh264/smart-mobility/issues) 
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](https://github.com/singh264/smart-mobility/pulls)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/singh264/smart-mobility/master)

---
# Getting Started
- To run the main code of our project checkout our repo's binder: https://mybinder.org/v2/gh/singh264/smart-mobility/master.
- To inspect all assets of our project visit our public repo: https://github.com/singh264/smart-mobility.


# Files and Directories 

### main.ipynb
- This is the main file for the project.

### kmeans.ipynb
- Includes k-means code for clustering lat, long from traffic data to identify key locations. The severity of traffic is treated as frequency. The nodes outputted from this file is used directly in the main.ipynb. This is a standalone file.  

### models
- Includes container classes to encapsulate useful details about coordinates, edges and traffic incidents.

### map
- Standalone tool to download and cache the coordinates of the edges of the North-York map.

### bing_traffic
- Module contains `bing_live_traffic_incidents_api.py` that retrieve live traffic incidents from the Bing Traffic API for a given bounding box on the map.
- Checkout this [Wiki](https://github.com/singh264/smart-mobility/wiki/Bing-Traffic) to learn more about the Bing Traffic API.

### Pictures 
- Includes demo pictures. 
- These pictures are used in the presentation. 
