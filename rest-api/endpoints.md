---
description: How to query metrics using Metlo's REST API.
---

# Endpoints

{% swagger baseUrl="https://yourcompany.metlo.com" path="/api/query" method="post" summary="Start Query" %}
{% swagger-description %}
This endpoint starts a Metlo query. The body parameters should be in a JSON object. Look at the next section for example requests.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authentication" type="string" %}
Bearer <api_key>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="metrics" type="array" %}
The list of metrics you want to query
{% endswagger-parameter %}

{% swagger-parameter in="body" name="filters" type="array" %}
A list of filter objects
{% endswagger-parameter %}

{% swagger-parameter in="body" name="groups" type="array" %}
A list of dimensions you want to group by
{% endswagger-parameter %}

{% swagger-parameter in="body" name="time_dimensions" type="array" %}
A list of time dimensions
{% endswagger-parameter %}

{% swagger-response status="200" description="The request was successful and the query has started." %}
```javascript
{
    "id": "<query_id>",
    "status": "PENDING",
    "ok": true,
    "msg": "Query Started"
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Something about your query is invalid. The msg field should explain what went wrong." %}
```javascript
{
    "ok": false,
    "msg": "Invalid Filters."
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://yourcompany.metlo.com" path="/api/fetch/<query_id>" method="get" summary="Fetch Results" %}
{% swagger-description %}
This endpoint lets you poll for results from a started query.
{% endswagger-description %}

{% swagger-parameter in="path" name="query_id" type="string" %}
Your queries id (returned by the query endpoint)
{% endswagger-parameter %}

{% swagger-response status="200" description="The fetch request was successful. Keep on polling for the result using this endpoint while status is one of the following: 'PENDING', 'RECEIVED', 'STARTED', 'RETRY'. " %}
```javascript
{
    "id": "<query_id>",
    "ok": true,
    "status": "SUCCESS",
    "result": {
        "num_completed_trips": {
            "0": 6942, "1": 2351
        },
        "product": {
            "0": "SOLO", "1": "POOL"
        }
    }
}
```
{% endswagger-response %}
{% endswagger %}

