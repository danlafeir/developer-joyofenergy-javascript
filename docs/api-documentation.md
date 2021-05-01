# API

Below is a list of API endpoints with their respective input and output. Please note that the application needs to be running for the following endpoints to work. For more information about how to run the application, please refer to **run the application** from the README.md

### Store readings

Endpoint

```text
POST /readings/store
```

Example of body

```json
{
  "smartMeterId": <smartMeterId>,
  "electricityReadings": [
    {
      "time": <time>,
      "reading": <reading>
    }
  ]
}
```

Parameters

| Parameter      | Description                                          |
| -------------- | ---------------------------------------------------- |
| `smartMeterId` | One of the smart meters' id listed above             |
| `time`         | The date/time (as epoch) when the _reading_ is taken |
| `reading`      | The consumption in `kW` at the _time_ of the reading |

Example readings

| Date (`GMT`)      | Epoch timestamp | Reading (`kW`) |
| ----------------- | --------------: | -------------: |
| `2020-11-29 8:00` |      1606636800 |         0.0503 |
| `2020-11-29 8:01` |      1606636860 |         0.0621 |
| `2020-11-29 8:02` |      1606636920 |         0.0222 |
| `2020-11-29 8:03` |      1606636980 |         0.0423 |
| `2020-11-29 8:04` |      1606637040 |         0.0191 |

In the above example, the smart meter sampled readings, in `kW`, every minute. Note that the reading is in `kW` and
not `kWH`, which means that each reading represents the consumption at the reading time. If no power is being consumed
at the time of reading, then the reading value will be `0`. Given that `0` may introduce new challenges, we can assume
that there is always some consumption, and we will never have a `0` reading value. These readings are then sent by the
smart meter to the application using REST. There is a service in the application that calculates the `kWH` from these
readings.

The following POST request, is an example request using CURL, sends the readings shown in the table above.

```console
$ curl \
  -X POST \
  -H "Content-Type: application/json" \
  "http://localhost:8080/readings/store" \
  -d '{"smartMeterId":"smart-meter-0","electricityReadings":[{"time":1606636800,"reading":0.0503},{"time":1606636860,"reading":0.0621},{"time":1606636920,"reading":0.0222},{"time":1606636980,"reading":0.0423},{"time":1606637040,"reading":0.0191}]}'
```

The above command will return an array with all readings for the given smart meter id.

Example output

```json
[
  {
    "time": 1607686125,
    "reading": 0.9258396634545867
  },
  {
    "time": 1607682525,
    "reading": 1.4237064184605117
  },
  {
    "time": 1607678925,
    "reading": 0.9974238262070414
  },
  {
    "time": 1607675325,
    "reading": 0.7347072120638889
  },
  {
    "time": 1607671725,
    "reading": 0.27168077193505225
  },
  {
    "time": 1607668125,
    "reading": 0.1981733770158689
  },
  {
    "time": 1606636800,
    "reading": 0.0503
  },
  {
    "time": 1606636860,
    "reading": 0.0621
  },
  {
    "time": 1606636920,
    "reading": 0.0222
  },
  {
    "time": 1606636980,
    "reading": 0.0423
  },
  {
    "time": 1606637040,
    "reading": 0.0191
  }
]
```

### Get Stored Readings

Endpoint

```
GET /readings/read/<smartMeterId>
```

Parameters

| Parameter      | Description                              |
| -------------- | ---------------------------------------- |
| `smartMeterId` | One of the smart meters' id listed above |

Retrieving readings using CURL

```console
$ curl "http://localhost:8080/readings/read/smart-meter-0"
```

Example output

```json
[
  {
    "time": 1607686125,
    "reading": 0.9258396634545867
  },
  {
    "time": 1607682525,
    "reading": 1.4237064184605117
  },
  {
    "time": 1607678925,
    "reading": 0.9974238262070414
  },
  {
    "time": 1607675325,
    "reading": 0.7347072120638889
  },
  {
    "time": 1607671725,
    "reading": 0.27168077193505225
  },
  {
    "time": 1607668125,
    "reading": 0.1981733770158689
  },
  {
    "time": 1606636800,
    "reading": 0.0503
  },
  {
    "time": 1606636860,
    "reading": 0.0621
  },
  {
    "time": 1606636920,
    "reading": 0.0222
  },
  {
    "time": 1606636980,
    "reading": 0.0423
  },
  {
    "time": 1606637040,
    "reading": 0.0191
  }
]
```

### View Current Price Plan and Compare Usage Cost Against all Price Plans

Endpoint

```text
GET /price-plans/compare-all/<smartMeterId>
```

Parameters

| Parameter      | Description                              |
| -------------- | ---------------------------------------- |
| `smartMeterId` | One of the smart meters' id listed above |

Retrieving readings using CURL

```console
$ curl "http://localhost:8080/price-plans/compare-all/smart-meter-0"
```

Example output

```json
{
  "smartMeterId": "smart-meter-0",
  "pricePlanComparisons": [
    {
      "price-plan-0": 0.0148314004034269
    },
    {
      "price-plan-1": 0.0029662800806853793
    },
    {
      "price-plan-2": 0.0014831400403426897
    }
  ]
}
```

### View Recommended Price Plans for Usage

Endpoint

```text
GET /price-plans/recommend/<smartMeterId>[?limit=<limit>]
```

Parameters

| Parameter      | Description                                          |
| -------------- | ---------------------------------------------------- |
| `smartMeterId` | One of the smart meters' id listed above             |
| `limit`        | (Optional) limit the number of plans to be displayed |

Retrieving readings using CURL

```console
$ curl "http://localhost:8080/price-plans/recommend/smart-meter-0?limit=2"
```

Example output

```json
[
  {
    "price-plan-2": 0.0014831400403426897
  },
  {
    "price-plan-1": 0.0029662800806853793
  }
]
```
