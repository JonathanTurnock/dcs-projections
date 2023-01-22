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
import proj4 from "proj4"

const lat = 42.5172;
const lon = 41.8622;
const x = -252691.23432109784;
const y = 628703.2536546878;

const projector = proj4("+proj=tmerc +lat_0=0 +lon_0=33 +k_0=0.9996 +x_0=-99516.9999999732 +y_0=-4998114.999999984 +towgs84=0,0,0,0,0,0,0 +units=m +vunits=m +ellps=WGS84 +no_defs +axis=neu");


const LOtoLL = (x, y) => {
    const [lon, lat] = projector.inverse([y, x]);
    return [lat, lon];
}

const LLtoLO = (lon, lat) => {
    const [y, x] = projector.forward([lon, lat]);
    return [x, y];
}

console.log(LLtoLO(lon, lat));      // [-252691.23432109784, 628703.2536546...]
console.log(LOtoLL(x, y));          // [42.5172, 41.86220000000001]
```

### Python

https://pyproj4.github.io/pyproj/stable/

```python
from pyproj import CRS, Proj

lon = 41.8622
lat = 42.5172
x = -252691.23432109784
y = 628703.2536546878

crs = CRS.from_proj4(
    "+proj=tmerc +lat_0=0 +lon_0=33 +k_0=0.9996 +x_0=-99516.9999999732 +y_0=-4998114.999999984 +towgs84=0,0,0,0,0,0,0 +units=m +vunits=m +ellps=WGS84 +no_defs +axis=neu")

projector = Proj(crs)

def LOtoLL(x, y):
    (lat, lon) = projector(latitude=x, longitude=y, inverse=True)
    return [lon, lat]

def LLtoLO(lon, lat):
    (x, y) = projector(latitude=lat, longitude=lon)
    return [x, y]


print(LOtoLL(x, y))         # [42.51719999999997, 41.862199999999994]
print(LLtoLO(lon, lat))     # [628703.2536546879, -252691.23432109412]
```

## Credits

Credits to the PyDCS team for the values from the strings

- https://github.com/pydcs/dcs
