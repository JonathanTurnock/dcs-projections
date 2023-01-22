# dcs-projections

List of DCS World Projections to be used to power various projection libraries

## Usage

### Javascript

```javascript
const projector = proj4(<<desired-projection-string>>)

function LOtoLL(projector, [x, y]) {
    const [xa, ya] = projector.inverse([y, x]);
    return [ya, xa];
}

function LLtoLO([lon, lat], projector) {
    const [y, x] = this.projector.forward([lon, lat]);
    return [x, y];
}
```

## Credits

Credits to the PyDCS team for the values from the strings

- https://github.com/pydcs/dcs
