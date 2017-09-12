
### Visualization
<p> Use folium to display the map and to cluster users, use "POI1","POI3","POI4" as example</p>
<P> Deploy marketing stratge within the area that has higher user density</P>


```python
import folium
from IPython.display import display
from folium.plugins import MarkerCluster

SF_COORDINATES = (float(df[df.POI =='POI1'].head(1).plat),float(df[df.POI =='POI1'].head(1).plon))
SF_COORDINATES1 = (float(df[df.POI =='POI3'].head(1).plat),float(df[df.POI =='POI3'].head(1).plon))
SF_COORDINATES2 = (float(df[df.POI =='POI4'].head(1).plat),float(df[df.POI =='POI4'].head(1).plon))
# for speed purposes
MAX_RECORDS = 200
 
# create empty map zoomed in Canada
m = folium.Map(location=(52.662724, -94.948657), zoom_start=3.5)
marker_cluster = MarkerCluster().add_to(m)

# add a marker for every record in the filtered data, use a clustered view
for each in df[df.POI=='POI1'].head(MAX_RECORDS).iterrows():
    folium.Marker(
        location = [each[1]['lat'],each[1]['lon']],
        icon=folium.Icon(color='green'),
    ).add_to(marker_cluster) 
for each in df[df.POI=='POI3'].head(MAX_RECORDS).iterrows():
    folium.Marker(
        location = [each[1]['lat'],each[1]['lon']],
        icon=folium.Icon(color='yellow'),
    ).add_to(marker_cluster)
for each in df[df.POI=='POI4'].head(MAX_RECORDS).iterrows():
    folium.Marker(
        location = [each[1]['lat'],each[1]['lon']],
        icon=folium.Icon(color='blue'),
    ).add_to(marker_cluster) 
folium.Marker(location = SF_COORDINATES, icon=folium.Icon(color='red',icon='POI')).add_to(m)
folium.Marker(location = SF_COORDINATES1, icon=folium.Icon(color='red',icon='POI')).add_to(m)
folium.Marker(location = SF_COORDINATES2, icon=folium.Icon(color='red',icon='POI')).add_to(m)
display(m)
```
![alt text](https://raw.githubusercontent.com/vic614/geospatial/master/ezgif.com-optimize.gif "Demo")
