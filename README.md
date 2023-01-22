# dcs-projections

List of DCS World Projections to be used to power various projection libraries

## Usage

First you will need a library to convert mercator projections then use the string to cast to and from coords.

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

> TODO: Add Projection Example

## Credits

Credits to the PyDCS team for the values from the strings

- https://github.com/pydcs/dcs
