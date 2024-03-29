# ns-api

Access public transit data from [Nederlandse Spoorwegen API](https://www.ns.nl/reisinformatie/ns-api) with node.js

[![Changelog](https://img.shields.io/npm/v/ns-api.svg?maxAge=3600)](https://github.com/fvdm/nodejs-ns-api/blob/master/CHANGELOG.md)
[![Build Status](https://travis-ci.org/fvdm/nodejs-ns-api.svg?branch=master)](https://travis-ci.org/fvdm/nodejs-ns-api)
[![Coverage Status](https://coveralls.io/repos/github/fvdm/nodejs-ns-api/badge.svg?branch=master)](https://coveralls.io/github/fvdm/nodejs-ns-api?branch=master)
[![Greenkeeper badge](https://badges.greenkeeper.io/fvdm/nodejs-ns-api.svg)](https://greenkeeper.io/)


To use this module you need API access credentials,
which you can request at [Here](https://apiportal.ns.nl) (Dutch).

* [Node.js](https://nodejs.org)
* [package](https://www.npmjs.com/package/ns-api)
* [API documentation](https://apiportal.ns.nl)


## Example

```js
const NSAPI = require ('ns-api');
const ns = new NSAPI ({
  key: 'abc123',
});

// console.log does not log >3 levels
function output (data) {
  console.dir (data, {
    depth: null,
    colors: true,
  });
}

// Get travel advise
ns.getTrips ({
  fromStation: 'Amersfoort',
  toStation: 'Den Haag',
})
  .then (output)
  .catch (console.error)
;
```


## Installation

`npm i ns-api`


## Configuration

param   | type   | required | default | description
:-------|:-------|:---------|:--------|:-----------
key     | string | yes      |         | One of your API keys
timeout | number | no       | 5000    | Request time out in ms


```js
const NSAPI = require ('ns-api');
const ns = new NSAPI ({
  key: 'abc123',
});
```


## Methods

Each method returns a Promise, so make sure to catch the errors properly.
I'm not going to outline to full posibilities of each method here,
only to parts that adjust the API response or make the request easier.
Read the API documention links to find all available parameters that each
method can take.


### getAllStations

List of all stations

```js
ns.getAllStations()
  .then (console.log)
  .catch (console.error)
;
```

[API documentation](https://apiportal.ns.nl/docs/services/public-reisinformatie-api/operations/ApiV2StationsGet)


### getArrivals

List of arrivals at a station

argument   | type           | description
:----------|:---------------|:-----------
[dateTime] | Date or string | Value will be converted to the right format

```js
ns.getArrivals ({ dateTime: '2019-05-10' })
  .then (console.log)
  .catch (console.error)
;
```

[API documentation](https://apiportal.ns.nl/docs/services/public-reisinformatie-api/operations/ApiV2ArrivalsGet)


### getBigDepartures

Large list of departures at a station

argument   | type           | description
:----------|:---------------|:-----------
[dateTime] | Date or string | Value will be converted to the right format

```js
ns.getBigDepartures ({ dateTime: '2019-05-10' })
  .then (console.log)
  .catch (console.error)
;
```

[API documentation](https://apiportal.ns.nl/docs/services/public-reisinformatie-api/operations/ApiV2DeparturesBigGet)


### getDepartures

List all departures

argument | type   | description
:--------|:-------|:-----------
id       | string | Departure object ID

```js
ns.getDepartures ({ id: 'abc123' })
  .then (console.log)
  .catch (console.error)
;
```

[API documentation](https://apiportal.ns.nl/docs/services/public-reisinformatie-api/operations/ApiV2DeparturesGet)


### getDisruptions

List all disruptions

argument | type    | description
:--------|:--------|:-----------
[actual] | boolean | Only return disruptions within 2 hours

```js
ns.getDisruptions()
  .then (console.log)
  .catch (console.error)
;
```

[API documentation](https://apiportal.ns.nl/docs/services/public-reisinformatie-api/operations/ApiV2DisruptionsGet)


### getStationDisruption

List of disruptions at a station

argument   | type           | description
:----------|:---------------|:-----------
[dateTime] | Date or string | Value will be converted to the right format

```js
ns.getStationDisruption ({ dateTime: '2019-05-10' })
  .then (console.log)
  .catch (console.error)
;
```

[API documentation](https://apiportal.ns.nl/docs/services/public-reisinformatie-api/operations/ApiV2DisruptionsStationByCodeGet)


### getDisruption

Get details about one disruption

argument | type   | description
:--------|:-------|:-----------
id       | string | Disruption object ID

```js
ns.getDisruption ({ id: 'abc123' })
  .then (console.log)
  .catch (console.error)
;
```

[API documentation](https://apiportal.ns.nl/docs/services/public-reisinformatie-api/operations/ApiV2DisruptionsByIdGet)


### getTrips

Get a list of travel advises

argument   | type           | description
:----------|:---------------|:-----------
[dateTime] | Date or string | Value will be converted to the right format

```js
ns.getTrips ({
  dateTime: '2019-05-10 17:40',
  fromStation: 'Amersfoort',
  toStation: 'Den Haag',
})
  .then (console.log)
  .catch (console.error)
;
```

[API documentation](https://apiportal.ns.nl/docs/services/public-reisinformatie-api/operations/ApiV3TripsGet)


### getTrip

Get a specific travel advise

argument | type   | description
:--------|:-------|:-----------
ctxRecon | string | Trip `ctxRecon` from [getTrips()](#getTrips)

```js
ns.getTrip ({ ctxRecon: 'abc123' })
  .then (console.log)
  .catch (console.error)
;
```

[API documentation](https://apiportal.ns.nl/docs/services/public-reisinformatie-api/operations/ApiV3TripsTripGet)


### getPrices

Get pricing for travel between two stations.

argument    | type           | description
:-----------|:---------------|:-----------
fromStation | string         | Station name or ID
toStation   | string         | Station name or ID

```js
ns.getPrices ({
  fromStation: 'AMF',
  toStation: 'Den Haag',
})
  .then (console.log)
  .catch (console.error)
;

```

[API documentation](https://apiportal.ns.nl/docs/services/public-prijsinformatie-api/operations/getPrices_2)


## Unlicense

This is free and unencumbered software released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or
distribute this software, either in source code form or as a compiled
binary, for any purpose, commercial or non-commercial, and by any
means.

In jurisdictions that recognize copyright laws, the author or authors
of this software dedicate any and all copyright interest in the
software to the public domain. We make this dedication for the benefit
of the public at large and to the detriment of our heirs and
successors. We intend this dedication to be an overt act of
relinquishment in perpetuity of all present and future rights to this
software under copyright law.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR
OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.

For more information, please refer to <https://unlicense.org/>


Author
------

[Franklin van de Meent](https://fvdm.com)
