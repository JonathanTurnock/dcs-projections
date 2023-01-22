# dcs-projections

List of DCS World Projections to be used to power various projection libraries, for now this should just be imported from github raw either at run or compile time.

https://raw.githubusercontent.com/JonathanTurnock/dcs-projections/main/projections.json

## Usage

Grab the data at some point, either build or runtime.

You will need a library to convert mercator projections then use the string to cast to and from coords.

Here are some test values to use for the caucasus projection

```javascript
const lat = 42.5172;
const lon = 41.8622;
const x = -252691.23432109784;
const y = 628703.2536546878;
```

### Javascript

https://www.npmjs.com/package/proj4

```javascript
const proj4 = require("proj4");

const projector = proj4(<<desired-projection-string>>);

const LOtoLL = ([x, y]) => {
    const [xa, ya] = projector.inverse([y, x]);
    return [ya, xa];
}

const LLtoLO = ([lon, lat]) => {
    const [y, x] = projector.forward([lon, lat]);
    return [x, y];
}
```

### Python

https://pyproj4.github.io/pyproj/stable/

```python
from pyproj import CRS, Proj

lat = 42.5172
lon = 41.8622
x = -252691.23432109784
y = 628703.2536546878

crs = CRS.from_proj4(
    "+proj=tmerc +lat_0=0 +lon_0=33 +k_0=0.9996 +x_0=-99516.9999999732 +y_0=-4998114.999999984 +towgs84=0,0,0,0,0,0,0 +units=m +vunits=m +ellps=WGS84 +no_defs +axis=neu")

projector = Proj(crs)


def LLtoLO(lat, lon):
    return projector(latitude=lat, longitude=lon)


def LOtoLL(x, y):
    return projector(latitude=x, longitude=y, inverse=True)


print(LLtoLO(lat, lon)) // (628703.2536546879, -252691.23432109412)
print(LOtoLL(x, y)) // (41.862199999999994, 42.51719999999997)
```

## Credits

Credits to the PyDCS team for the values from the strings

- https://github.com/pydcs/dcs
