```
from rasterstats import zonal_stats
listofzones = zonal_stats(
    os.path.join("../repo/split_shapefile","河北_130300.shp"), 
    "../repo/tif_result/maskersHB.tif",
     stats="sum")
```
