# Welcome to mocklib!

**mockib** is a fake C++ library for CMPT376W Technical Assignment. It manages geographic points in landitude, longitude, and elevation, using the WGS 84 standard. 

This library offers distance comparison, elevation comparison, GPX reading and writing, area calculations and much more.

This documentation website is build using `MKDocs` with the theme `Cinder`, and the favicon sourced from Wikimedia Commons [2-4].

## Installation

### Prerequisites
Before using **mocklib**, ensure you have the following installed:

* [Git](https://git-scm.com/install/)
* [Clang](https://releases.llvm.org/download.html), 
[g++](https://code.visualstudio.com/docs/cpp/config-mingw) or another apropriate C++ compiler
* [Visual Studio Code](https://code.visualstudio.com/) (Windows)

**mocklib** requires [gxplib](https://github.com/irdvo/gpxlib.git) for GPX file methods [1]. Clone the project:

    git clone https://github.com/irdvo/gpxlib.git

and move `gpx` to your working directory.

To download **mocklib**, clone the public repository to your working directory:

    git clone https://github.com/Nahum-Asfaw/mocklib.git

Now you're all set!

## Introduction
### Distance Comparison

**mocklib** provides basic classes and methods for geographical point operations [6]. If, for example,  
you had a collection of geographic points and wanted to know which two were the farthest apart, you can use 

    Map.get_distance(horizontal k1, horizontal k2)

As a comparator. Here's an example in a short program:

    #include "mocklib\Map_Globe.h"
    #include "mocklib\horizontal_geodetic.h"

    int main(){
        horizontal *points; // given collection of horizontal geographic points                  
        Map map();
        int largest = 0;
        horizontal a; b;
        for (int i = 0; i < sizeof(points); i++){
            int temp = map.get_distance(points[i], points[i+1]);
            if (temp >= largest){
                largest = temp;
                a = points[i]; b = points[i+1];
            }
        }
        cout << a << "\n" << b;
    }

### Inclusion/Exclusion
You can also perform 'inside-out' testing with a collection of points that define a region or area. If, for example,  
you had a collection of points that outlined a country, you can use one of

    Area.is_point_inside(horiziontal k)
    Volume.is_point_inside(geodetic k)

To check if a given point `k` was inside that area.  
Here's an example for the wikipedia question in the assignment description:

    #include "mocklib\area_volume.h"
    #include "mocklib\horizontal_geodetic.h"

    int main(){
        horizontal *outline; // collection of points that outline Canada
        horiziontal *wikipedia_points; // a collection of points on wikipedia
        Area canada(outline);
        Area wikipedia_canada();
        for (int i = 0; i < sizeof(wikipedia_points); i++){
            if (canada.is_point_inside(wikipedia_points[i])){
                wikipedia_canada.add_horiz_point(wikipedia_points[i]);
                cout << wikipedia_points[i] << endl;
            }
        }
    }

The same is possible with 3D wikipedia points, using `Volume`.

### GPX read/write
Use `gpx` to manage read/write operation with GPX (`xml`) files. To take a collection of geographic points from an `xml` file of `filename`, use

    gpx.get_info(char *filename)

to return either a `horizontal *` or `geodetic *` array of the location information in this file.
Here is an example involving an `xml` file that describes a path some Fitbit user has taken:

    #include "mocklib\gpx.h"
    #include "mocklib\horizontal_geodetic.h"

    int main(){
        gpx gpx();
        geodetic *array = gpx.get_info("data.xml");
        for(int i = 0; i < sizeof(array); i++){
            cout << array[i] << endl;
        }
    }

This is a small selection of what can be done with **mocklib**. For more topical guides, visit [Advanced](advanced.md).