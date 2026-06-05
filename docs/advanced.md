# Advanced
Guides for more complicated operations.

## Writting to an xml or kml File [8]

After performing any geographical point operations, you may want to write your output to an `xml` file to be used in other GIS applications. This can be done with one of

    Map.write(horizontal k, char *filename)
    Globe.write(geodetic k, char *filename)
    Area.write(char *filename)
    Volume.write(char *filename)

depending on the dimensionality and number of your results.  
Here is a short program to demonstrate this:

    #include "mocklib\area_volume.h"
    #include "mocklib\horizontal_geodetic.h"

    int main(){
        //... after performing some operations
       geodetic point_to_print.longitude = 0;
       point_to_print.laditude = 0;
       point_to_print.elevation = 0; 
       Map.write(point_to_print, new_file.kml);
    }

`new_file.kml` will be:

    <?xml version="1.0" encoding="UTF-8"?>
    <Document>
    <Placemark>
        <Point>
            <coordinates> 0.0, 0.0, 0 </coordinates>
        </Point>
    </Placement>
    </Document>



## Getting length of a path

It's possible to do quite a bit with the geographical information read from an xml file. If you wanted to know the length of a path taken on a morning walk, first call
    
    Area.get_info(char *filename)

to set a `horizontal *` array of the given coordinates. Then use

    Area.return_perim()

to return, in kilometers, the length of the path given by following each point.  
Here is another sample program deomstrating this:

    #include "mocklib\area_volume.h"
    #include "mocklib\horizontal_geodetic.h"

    int main(){
        Area sample();
        sample.get_info(walk_on_beach.xml);
        cout << sample.return_perim(); // will output int of length of the path
    }

## Distance to Mariana Trench, Null Island, and Land Mass Comparitors

Classes in **mocklib** have locally saved coordinate values for different GIS usages.  
If you wanted to know the distance from a given geographical point to the Mariana Trench or "Null Island", you can check using one of [5]:

    Map.dist_to_null_island(horizontal k)
    Globe.dist_to_mariana_trench(geodetic k)

You may also be interested in what Continent or Ocean a given point is on. Use one of

    Map.get_ocean_continent(horizontal k)
    Map.get_closest_ocean(horizontal k)

To return the Ocean or Continent a point is on, or the closest ocean to a point.  
Here is some sample code deomstrating these comparitors:

    #include "mocklib\Map_Globe.h"
    #include "mocklib\horizontal_geodetic.h"

    int main(){
        horizontal vanouver;
        Map map();
        int dist = map.dist_to_null_island; // output distance from vancouver to null island
        //... some time later        
        cout << map.get_ocean_continent(vancouver); 
        cout << map.get_closest_ocean(vancouver); 
    }

The sample output will be:

    North America
    Pacific
