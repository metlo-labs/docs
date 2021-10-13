---
description: How to query metrics using the Python SDK.
---

# Usage

## Querying

To query a metric you can use the query function. For example, the `num_trips` metric can be queried as follows:

```python
import metlo

metlo.query('num_trips')
# =>
#    num_trips
# 0      50000
```

## Multiple Metrics

You can also query multiple metrics at the same time using the same function by passing in a list of metrics:

```python
import metlo

metlo.query(['num_trips', 'avg_trip_time'])
# =>
#    avg_trip_time  num_trips
# 0       599.9443      50000
```

## Filtering

The results can be filtered on any dimension using the `filters` keyword argument. For example, if you wanted to filter for only the metrics in the cities 1 and 2:

```python
from metlo import query, Filter, FilterOp

query(
    'num_trips',
    filters=[
        Filter(
            dimension='city',
            op=FilterOp.EQ,
            values=[1, 2],
        ),
    ],
)
# =>
#    num_trips
# 0       9950
```

Here are the different filters currently available:

```python
class FilterOp(str, Enum):
    EQ = 'eq'
    LT = 'lt'
    GT = 'gt'
    LTE = 'lte'
    GTE = 'gte'
    IN = 'IN'
    LIKE = 'LIKE'
    NOT_NULL = 'not_null'
    IS_NULL = 'is_null'
```

## Grouping

You can group by different dimensions using the `groups` keyword argument:

```python
from metlo import query, Filter

query(
    'num_trips',
    groups=['city', 'product'],
    filters=[
        Filter(dimension='city', values=[1, 2]),
    ],
)
# =>
#    city  num_trips product
# 0     1       3706    SOLO
# 1     1       1280    POOL
# 2     2       3711    SOLO
# 3     2       1253    POOL
```

## Time Dimensions

You can filter and group by time dimensions using the `time_dimensions` keyword argument. `granularity` is the time granularity you want to aggregate by (hour, day, month, etc..). `date_range` is a list with two date strings that specify an **inclusive** filter.

```python
from metlo import query, Filter, TimeDimension, TimeGranularity

query(
   'num_trips',
   time_dimensions=[
      TimeDimension(
         dimension='trip_time',
         granularity=TimeGranularity.MONTH,
         date_range=[
            "2019-05-01T19:00:00.000Z",
            "2019-08-30T19:00:00.000Z",
         ]
      )
   ],
   filters=[
      Filter(dimension='city', values=[1]),
      Filter(dimension='product', values=['SOLO']),
   ],
)
# =>
#                       month  num_trips
# 0  2019-05-01T00:00:00.000Z       1325
# 1  2019-06-01T00:00:00.000Z       1215
# 2  2019-07-01T00:00:00.000Z       1123
```

