---
description: Example queries to Metlo's REST API.
---

# Examples

### Querying for a Metric

```javascript
{
    "metrics": ["num_trips"]
}
```

### Filtering on a Dimension

```javascript
{
    "metrics": ["num_trips"],
    "filters": [
        {
            "dimension": "city",
            "values": [1, 2],
            "op": "eq"
        }
    ]
}
```

### Grouping by Dimensions

```javascript
{
    "metrics": [ "num_trips" ],
    "filters": [
        {
            "dimension": "city",
            "values": [1, 2],
            "op": "eq"
        }
    ],
    "groups": [ "city", "product" ]
}
```

### Time Dimensions

```python
{
    "metrics": ["num_trips"],
    "time_dimensions": [
        {
            "dimension": "trip_time",
            "granularity": "month",
            "date_range": [
                "2019-05-01T19:00:00+00:00",
                "2019-08-30T19:00:00+00:00"
            ]
        }
    ]
    "filters": [
        {
            "dimension": "city",
            "values": [1],
            "op": "eq"
        },
        {
            "dimension": "product",
            "values": ["SOLO"],
            "op": "eq"
        }
    ],
}
```
