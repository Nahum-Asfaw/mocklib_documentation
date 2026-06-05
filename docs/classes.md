# Classes

List of all classes, methods, and elements in **mocklib**.

## Map

Class to manage horiziontal point information
for individual points, not creating an area or perimiter.

### Public Methods
    Map()

Empty constructor.  
Has no return value.

    Map.get_distance(horizontal k1, horizontal k2)
    
Returns `int` of geographical distance in kilometers between `k1` and `k2`, approximating arc distance using tunnel distance.  
Returns `-1` on error.

    Map.get_long_difference(horizontal k1, horizontal k2)

Returns `float` of comparison `|k1 - k2|` of longitude values for `k1`, `k2`.  
Returns `-1` on error.

    Map.get_lad_difference(horizontal k1, horizontal k2)

Returns `float` of comparison `|k1 - k2|` of laditude values for `k1`, `k2`.  
Returns `-1` on error.

    Map.get_closest_ocean(horizontal k)

Returns `char` string sating closest ocean given a reference point `k`. Ocean points are saved  
as the center of each ocean.  
Returns one of `Pacific`, `Atlantic`, `Indian`, `Artic`, `Antartic` on success.  
Returns `Error: example error msg` on error.

    Map.get_ocean_continent(horizontal k)

Returns `char` string of Ocean or Continent a reference point `k` is on.  
Returns one of `Pacific`, `Atlantic`, `Indian`, `Artic`, `Antartic`,  
`Africa`, `Asia`, `Europe`, `North America`, `Oceania`, `South America`, `Antartica` on success.  
Returns `Error: example error msg` on error.

    Map.dist_to_null_island(horizontal k)

Returns `int` of geographical distance in kilometers to "Null Island", the point where `longitude = 0` and  
`laditude = 0`. Off the coast of Ghana, "Null Island" is an in-joke in GIS applications, it's not an actuall island.  
Returns `-1` on error.

    Map.write(horizontal k, char *filename)

Append a single `horiziontal` point `k` to an xml file of `filename`. If that file doesn't exist, it will create it.  
Returns `Error: example error msg` on error.

### Private Methods
There are no private methods for `Map`.

## Globe
Class to manage geodetic point information
for individual points not creating a volume.

### Public Methods
    Globe()

Empty constructor.  
Has no return value.

    Globe.get_pythag_distance(geodetic k1, geodetic k2)

Returns `int` of pythagorean distance in kilometers between two geodetic points `k1`, `k2`.  
Returns `-1` on error.

    Globe.get_long_difference(geodetic k1, geodetic k2)

Returns `float` of comparison `|k1 - k2|` of longitude values for `k1`, `k2`.  
Returns `-1` on error.

    Globe.get_lad_difference(geodetic k1, geodetic k2)

Returns `float` of comparison `|k1 - k2|` of laditude values for `k1`, `k2`.  
Returns `-1` on error.

    Globe.get_elevation_difference(geodetic k1, geodetic k2)

Returns `int` of comparison `|k1 - k2|` of elevation values for `k1`, `k2`.  
Returns `-1` on error.

    Globe.get_ocean_continent(geodetic k)

Returns `char` string of Ocean or Continent a reference point `k` is on.  
Returns one of `Pacific`, `Atlantic`, `Indian`, `Artic`, `Antartic`,  
`Africa`, `Asia`, `Europe`, `North America`, `Oceania`, `South America`, `Antartica` on success.  
Returns `Error: example error msg` on error.

    Globe.dist_to_mariana_trench(geodetic k)

Returns `int` of distance in kilometers from geodetic point `k` to the bottom of the Mariana Trench.  
returns `-1` on error.

    Globe.write(geodetic k, char *filename)

Append a single `geodetic` point `k` to an xml file of `filename`. If that file doesn't exist, it will create it.  
Returns `Error: example error msg` on error.

### Private Methods
There are no private methods for `Globe`.

## gpx 
Class to manage input output operations with GPX (xml) files.

### Public Methods

    gpx()

Empty construcor.  
Has no return value.

    gpx.get_info(char *filename)

Read from a GPX (`xml`) file, return point info as either `horizontal` or `geodetic`.  
Returns `Error: example error msg` on error.

    gpx.write_horiz_to_xml(char *filename, horizontal *array)

Appends to an `xml` file (or creates one with the given filename if one doesn't exist)  
the horizontal point information `array` and time of day.  
Returns `Error: example error msg` on error.

    gpx.write_geodetic_to_xml(char *filename, horizontal *array)

Appends to an `xml` file (or creates one with the given filename if one doesn't exist)  
the geodetic point information `array` and time of day.  
Returns `Error: example error msg` on error.

### Private Methods
There are no private methods for `GPX`.

## Area
Class to manage array of horizontal point values that create an area.

### Public Methods

    Area(horizontal *new_array)

Constructor. Takes type `horizontal *` for `new array`, setting `array` and calculating `area` and `perim`.  
Has no return value.

    Area.add_horiz_point(horizontal k)

Appends horizontal point `k` to the `array`. Updates `area` and `perim` according to the new `array`.  
Returns `Error: example error msg` on error.

    Area.return_perim()

Returns `int` value `perim` representing the perimiter (path) in kilometers bounded by the points in `array`.  
Returns `-1` on error.

    Area.return_area()

Returns `int` value `area` representing the area in kilometers squared bounded by the points in `array`.  
Returns `-1` on error.

    Area.return_array()

Returns array of `horizontal *` type.  
Returns `Error: example error msg` on error.

    Area.is_point_inside(horizontal k)

Returns `bool`, checks whether a given `horizontal` point `k` is bounded within the points  
in `array`. Returns `true` if `k` is inside the area, `false` if not.  
Returns `false` on error.

    Area.write(char *filename)

Appends array (list) of horizontal point information to `xml` file of a given `filename`. Will create an `xml` file of `filename` if that file is not found.  
Returns `Error: example error msg` on error.

    Area.new_array(horizontal *new_array)

Takes new `horizontal *` type array given as `new_array` and recalculates `area`, `perim`.  
Returns `Error: example error msg` on error.

### Private Methods
    horizontal *array;
    int area;
    int perim;

Makes `array` to hold an array of horizontal point values, `area` to hold area in kilometers squared of the space bounded by `array`, and `perim` to hold the length in kilometers of the path of connected points in `array`.

## Volume

Class to manage array of geodetic point values that create a volume.

### Public Methods
    Volume(geodetic *new_array)
Constructor. Takes type `geodetic *` for `new_array`, setting `array` and calculating `area`, `perim`, and `volume`.  
Has no return value.

    Volume.add_geodetic_point(geodetic k)

Appends horizontal point `k` to the `array`. Updates `area`, `perim` and `volume` according to the new `array`.  
Returns `Error: example error msg` on error.

    Volume.return_perim()

Returns `int` value `perim` representing the perimiter (path) in kilometers bounded by the points.  
Returns `-1` on error.

    Volume.return_area()

Returns `int` value `area` representing the area in kilometers squared bounded by the points in `geodetic *` array, ignoring elevation values.  
Returns `-1` on error.

    Volume.return_volume()

Returns `int` value representing in kilometers squared the volume bounded by the points in `geodetic *` array.  
Returns `-1` on error.

    Volume.return_array()

Returns array of type `geodetic *`.  
Returns `Error: example error msg` on error.

    Volume.is_point_inside(geodetic k)

Returns `bool`, checks if geodetic point `k` is inside the volume bounded by the points in `array`. Returns `true` if `k` is inside the volume, `false` if not.  
Returns `false` on error.

    Volume.return_avg_elevation()

Returns `int` representing in kilometers the average elevation of the volume bounded in the `geodetic *` array.  
Returns `-1` on error.

    Volume.write(char *filename)

Appends array (list) of geodetic point information to `xml` file of a given `filename`. Will create an `xml` file of `filename` if that file is not found.  
Returns `Error: example error msg` on error.

    Globe.new_array(geodetic *new_array)

Takes new `geodetic *` type array given as `new_array` and recalculates `area`, `perim`, and `volume`.  
Returns `Error: example error msg` on error.

### Private Methods
    geodetic *array;
    int area;
    int perim;
    int volume;

Makes `array` to hold an array of geodetic point values, `area` to hold area in kilometers squared of the space bounded by `array`, `perim` to hold the length in kilometers of the path of connected points in `array`, and `volume` to hold the volume in kilometers cubed. 

