# Structs

Basic data structures to hold longitude, laditude, and elevation values.

## horizontal 

Defines a `struct` for horizontal datums, where `longitude` is a `float` value from `-180` to `180` and `laditude` is a `float` from `-90` to `90`.

    struct horizontal{
        float longitude;
        float laditude;
    };

`horizontal` is used in `Map`, `Area`, and `GPX`.

## geodetic

Defines a `struct` for geodetic datums, where `longitude` is a float from `-180` to `180`, `laditude` is a float from `-90` to `90`, and elevation is an `int` above sea level.

    struct geodetic{
        float longitude;
        float laditude;
        int elevation;
    };

`geodetic` is used in `Globe`, `Volume`, and `GPX`.

