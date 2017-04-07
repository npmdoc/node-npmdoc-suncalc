# api documentation for  [suncalc (v1.8.0)](https://github.com/mourner/suncalc)  [![npm package](https://img.shields.io/npm/v/npmdoc-suncalc.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-suncalc) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-suncalc.svg)](https://travis-ci.org/npmdoc/node-npmdoc-suncalc)
#### A tiny JavaScript library for calculating sun/moon positions and phases.

[![NPM](https://nodei.co/npm/suncalc.png?downloads=true)](https://www.npmjs.com/package/suncalc)

[![apidoc](https://npmdoc.github.io/node-npmdoc-suncalc/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-suncalc_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-suncalc/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-suncalc/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-suncalc/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Vladimir Agafonkin"
    },
    "bugs": {
        "url": "https://github.com/mourner/suncalc/issues"
    },
    "dependencies": {},
    "description": "A tiny JavaScript library for calculating sun/moon positions and phases.",
    "devDependencies": {
        "eslint": "^3.12.2",
        "eslint-config-mourner": "^2.0.1",
        "tap": "^8.0.1"
    },
    "directories": {},
    "dist": {
        "shasum": "1d9898109563078750f4994a959e654d876acbf5",
        "tarball": "https://registry.npmjs.org/suncalc/-/suncalc-1.8.0.tgz"
    },
    "eslintConfig": {
        "extends": "mourner",
        "rules": {
            "indent": 0,
            "array-bracket-spacing": 0,
            "strict": 0,
            "brace-style": 0
        },
        "env": {
            "amd": true
        }
    },
    "gitHead": "b08d1f6f8e56a3c0d85469d6cf0ff8675cba40a5",
    "homepage": "https://github.com/mourner/suncalc",
    "jshintConfig": {
        "quotmark": "single",
        "trailing": true,
        "unused": true
    },
    "keywords": [
        "sun",
        "astronomy",
        "math",
        "calculation",
        "sunrise",
        "sunset",
        "twilight",
        "moon",
        "illumination"
    ],
    "main": "suncalc.js",
    "maintainers": [
        {
            "name": "mourner",
            "email": "agafonkin@gmail.com"
        }
    ],
    "name": "suncalc",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/mourner/suncalc.git"
    },
    "scripts": {
        "cov": "tap test.js --cov",
        "pretest": "eslint suncalc.js test.js",
        "test": "tap test.js"
    },
    "version": "1.8.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module suncalc](#apidoc.module.suncalc)
1.  [function <span class="apidocSignatureSpan">suncalc.</span>addTime (angle, riseName, setName)](#apidoc.element.suncalc.addTime)
1.  [function <span class="apidocSignatureSpan">suncalc.</span>getMoonIllumination (date)](#apidoc.element.suncalc.getMoonIllumination)
1.  [function <span class="apidocSignatureSpan">suncalc.</span>getMoonPosition (date, lat, lng)](#apidoc.element.suncalc.getMoonPosition)
1.  [function <span class="apidocSignatureSpan">suncalc.</span>getMoonTimes (date, lat, lng, inUTC)](#apidoc.element.suncalc.getMoonTimes)
1.  [function <span class="apidocSignatureSpan">suncalc.</span>getPosition (date, lat, lng)](#apidoc.element.suncalc.getPosition)
1.  [function <span class="apidocSignatureSpan">suncalc.</span>getTimes (date, lat, lng)](#apidoc.element.suncalc.getTimes)
1.  object <span class="apidocSignatureSpan">suncalc.</span>times



# <a name="apidoc.module.suncalc"></a>[module suncalc](#apidoc.module.suncalc)

#### <a name="apidoc.element.suncalc.addTime"></a>[function <span class="apidocSignatureSpan">suncalc.</span>addTime (angle, riseName, setName)](#apidoc.element.suncalc.addTime)
- description and source-code
```javascript
addTime = function (angle, riseName, setName) {
    times.push([angle, riseName, setName]);
}
```
- example usage
```shell
...
| 'night'         | night starts (dark enough for astronomical observations)                 |
| 'nadir'         | nadir (darkest moment of the night, sun is in the lowest position)       |
| 'nightEnd'      | night ends (morning astronomical twilight starts)                        |
| 'nauticalDawn'  | nautical dawn (morning nautical twilight starts)                         |
| 'dawn'          | dawn (morning nautical twilight ends, morning civil twilight starts)     |

'''javascript
SunCalc.addTime(/*Number*/ angleInDegrees, /*String*/ morningName, /*String*/ eveningName)
'''

Adds a custom time when the sun reaches the given angle to results returned by 'SunCalc.getTimes'.

'SunCalc.times' property contains all currently defined times.
...
```

#### <a name="apidoc.element.suncalc.getMoonIllumination"></a>[function <span class="apidocSignatureSpan">suncalc.</span>getMoonIllumination (date)](#apidoc.element.suncalc.getMoonIllumination)
- description and source-code
```javascript
getMoonIllumination = function (date) {

    var d = toDays(date || new Date()),
        s = sunCoords(d),
        m = moonCoords(d),

        sdist = 149598000, // distance from Earth to Sun in km

        phi = acos(sin(s.dec) * sin(m.dec) + cos(s.dec) * cos(m.dec) * cos(s.ra - m.ra)),
        inc = atan(sdist * sin(phi), m.dist - sdist * cos(phi)),
        angle = atan(cos(s.dec) * sin(s.ra - m.ra), sin(s.dec) * cos(m.dec) -
                cos(s.dec) * sin(m.dec) * cos(s.ra - m.ra));

    return {
        fraction: (1 + cos(inc)) / 2,
        phase: 0.5 + 0.5 * inc * (angle < 0 ? -1 : 1) / Math.PI,
        angle: angle
    };
}
```
- example usage
```shell
...
* 'distance': distance to moon in kilometers
* 'parallacticAngle': parallactic angle of the moon in radians


### Moon illumination

'''javascript
SunCalc.getMoonIllumination(/*Date*/ timeAndDate)
'''

Returns an object with the following properties:

* 'fraction': illuminated fraction of the moon; varies from '0.0' (new moon) to '1.0' (full moon)
* 'phase': moon phase; varies from '0.0' to '1.0', described below
* 'angle': midpoint angle in radians of the illuminated limb of the moon reckoned eastward from the north point of the disk;
...
```

#### <a name="apidoc.element.suncalc.getMoonPosition"></a>[function <span class="apidocSignatureSpan">suncalc.</span>getMoonPosition (date, lat, lng)](#apidoc.element.suncalc.getMoonPosition)
- description and source-code
```javascript
getMoonPosition = function (date, lat, lng) {

    var lw  = rad * -lng,
        phi = rad * lat,
        d   = toDays(date),

        c = moonCoords(d),
        H = siderealTime(d, lw) - c.ra,
        h = altitude(H, phi, c.dec),
        // formula 14.1 of "Astronomical Algorithms" 2nd edition by Jean Meeus (Willmann-Bell, Richmond) 1998.
        pa = atan(sin(H), tan(phi) * cos(c.dec) - sin(c.dec) * cos(H));

    h = h + astroRefraction(h); // altitude correction for refraction

    return {
        azimuth: azimuth(H, phi, c.dec),
        altitude: h,
        distance: c.dist,
        parallacticAngle: pa
    };
}
```
- example usage
```shell
...
* 'azimuth': sun azimuth in radians (direction along the horizon, measured from south to west),
e.g. '0' is south and 'Math.PI * 3/4' is northwest


### Moon position

'''javascript
SunCalc.getMoonPosition(/*Date*/ timeAndDate, /*Number*/ latitude, /*Number*/ longitude)
'''

Returns an object with the following properties:

* 'altitude': moon altitude above the horizon in radians
* 'azimuth': moon azimuth in radians
* 'distance': distance to moon in kilometers
...
```

#### <a name="apidoc.element.suncalc.getMoonTimes"></a>[function <span class="apidocSignatureSpan">suncalc.</span>getMoonTimes (date, lat, lng, inUTC)](#apidoc.element.suncalc.getMoonTimes)
- description and source-code
```javascript
getMoonTimes = function (date, lat, lng, inUTC) {
    var t = new Date(date);
    if (inUTC) t.setUTCHours(0, 0, 0, 0);
    else t.setHours(0, 0, 0, 0);

    var hc = 0.133 * rad,
        h0 = SunCalc.getMoonPosition(t, lat, lng).altitude - hc,
        h1, h2, rise, set, a, b, xe, ye, d, roots, x1, x2, dx;

    // go in 2-hour chunks, each time seeing if a 3-point quadratic curve crosses zero (which means rise or set)
    for (var i = 1; i <= 24; i += 2) {
        h1 = SunCalc.getMoonPosition(hoursLater(t, i), lat, lng).altitude - hc;
        h2 = SunCalc.getMoonPosition(hoursLater(t, i + 1), lat, lng).altitude - hc;

        a = (h0 + h2) / 2 - h1;
        b = (h2 - h0) / 2;
        xe = -b / (2 * a);
        ye = (a * xe + b) * xe + h1;
        d = b * b - 4 * a * h1;
        roots = 0;

        if (d >= 0) {
            dx = Math.sqrt(d) / (Math.abs(a) * 2);
            x1 = xe - dx;
            x2 = xe + dx;
            if (Math.abs(x1) <= 1) roots++;
            if (Math.abs(x2) <= 1) roots++;
            if (x1 < -1) x1 = x2;
        }

        if (roots === 1) {
            if (h0 < 0) rise = i + x1;
            else set = i + x1;

        } else if (roots === 2) {
            rise = i + (ye < 0 ? x2 : x1);
            set = i + (ye < 0 ? x1 : x2);
        }

        if (rise && set) break;

        h0 = h2;
    }

    var result = {};

    if (rise) result.rise = hoursLater(t, rise);
    if (set) result.set = hoursLater(t, set);

    if (!rise && !set) result[ye > 0 ? 'alwaysUp' : 'alwaysDown'] = true;

    return result;
}
```
- example usage
```shell
...

By subtracting the 'parallacticAngle' from the 'angle' one can get the zenith angle of the moons bright limb (anticlockwise).
The zenith angle can be used do draw the moon shape from the observers perspective (e.g. moon lying on its back).

### Moon rise and set times

'''js
SunCalc.getMoonTimes(/*Date*/ date, /*Number*/ latitude, /*Number*/ longitude[, inUTC])
'''

Returns an object with the following properties:

* 'rise': moonrise time as 'Date'
* 'set': moonset time as 'Date'
* 'alwaysUp': 'true' if the moon never rises/sets and is always _above_ the horizon during the day
...
```

#### <a name="apidoc.element.suncalc.getPosition"></a>[function <span class="apidocSignatureSpan">suncalc.</span>getPosition (date, lat, lng)](#apidoc.element.suncalc.getPosition)
- description and source-code
```javascript
getPosition = function (date, lat, lng) {

    var lw  = rad * -lng,
        phi = rad * lat,
        d   = toDays(date),

        c  = sunCoords(d),
        H  = siderealTime(d, lw) - c.ra;

    return {
        azimuth: azimuth(H, phi, c.dec),
        altitude: altitude(H, phi, c.dec)
    };
}
```
- example usage
```shell
...
// get today's sunlight times for London
var times = SunCalc.getTimes(new Date(), 51.5, -0.1);

// format sunrise time from the Date object
var sunriseStr = times.sunrise.getHours() + ':' + times.sunrise.getMinutes();

// get position of the sun (azimuth and altitude) at today's sunrise
var sunrisePos = SunCalc.getPosition(times.sunrise, 51.5, -0.1);

// get sunrise azimuth in degrees
var sunriseAzimuth = sunrisePos.azimuth * 180 / Math.PI;
'''

SunCalc is also available as an NPM package:
...
```

#### <a name="apidoc.element.suncalc.getTimes"></a>[function <span class="apidocSignatureSpan">suncalc.</span>getTimes (date, lat, lng)](#apidoc.element.suncalc.getTimes)
- description and source-code
```javascript
getTimes = function (date, lat, lng) {

    var lw = rad * -lng,
        phi = rad * lat,

        d = toDays(date),
        n = julianCycle(d, lw),
        ds = approxTransit(0, lw, n),

        M = solarMeanAnomaly(ds),
        L = eclipticLongitude(M),
        dec = declination(L, 0),

        Jnoon = solarTransitJ(ds, M, L),

        i, len, time, Jset, Jrise;


    var result = {
        solarNoon: fromJulian(Jnoon),
        nadir: fromJulian(Jnoon - 0.5)
    };

    for (i = 0, len = times.length; i < len; i += 1) {
        time = times[i];

        Jset = getSetJ(time[0] * rad, lw, phi, dec, n, M, L);
        Jrise = Jnoon - (Jset - Jnoon);

        result[time[1]] = fromJulian(Jrise);
        result[time[2]] = fromJulian(Jset);
    }

    return result;
}
```
- example usage
```shell
...
in the [Twilight article on Wikipedia](http://en.wikipedia.org/wiki/Twilight).


## Usage example

'''javascript
// get today's sunlight times for London
var times = SunCalc.getTimes(new Date(), 51.5, -0.1);

// format sunrise time from the Date object
var sunriseStr = times.sunrise.getHours() + ':' + times.sunrise.getMinutes();

// get position of the sun (azimuth and altitude) at today's sunrise
var sunrisePos = SunCalc.getPosition(times.sunrise, 51.5, -0.1);
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
