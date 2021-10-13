---
description: A guide on how to make Metlo Metric definitions.
---

# Defining Metrics

The core data structure in Metlo is a definition. A definition is an entity that contains a set of metrics and dimensions built on top of the same table (or view) inside your data warehouse.

_Note: We are showing a YAML interface here but you can also use the Web UI to build metric definitions. The UI has additional features that make writing a metric definition easy like autocomplete and live validation while creating definitions._

## Metadata

To make a definition you first have to supply some metadata:

* **Name - **The name of the definition. This name is unique and will be used as a namespace for every metric you build inside of it.
* **Owner - **The user (or group) that owns this definition
* **Datasource - **The id of the database connection this definition will use
* **Description - **A friendly description that describes what type of metrics and dimensions this definition will contain.
* **Table - **The table metrics and dimensions inside this definition will be built on top of

```yaml
name: ethereum_stats
owner: akshay
datasource: metlo_bigquery
description: A set of stats from the public bigquery Ethereum dataset.
table: bigquery-public-data.crypto_ethereum.transactions
```

## Dimensions

After you define the metadata for a definition, the next step is defining the dimensions you can slice and dice a metric by. This should be a mapping between the name of a dimension and the following fields:

* **Description - **A friendly description for the dimension
* **SQL - **The sql for the column you want this dimension to reference

```yaml
dimensions:
  sender:
    description: The address of the sender of a transaction
    sql: from_address

  receiver:
    description: The address of the receiver of a transaction
    sql: to_address

  timestamp:
    description: The timestamp of the block this transaction was in
    sql: block_timestamp
```

*Note: You need to specify at least one time dimension in each definition*

## Metrics

Metrics are the actual aggregations on top of the table that you care about. Each metric has the following fields:

* **Name - **The name of the metric
* **Description - **A friendly description for the metric
* **Type -** The type of metric, This can be an aggregation (sum, count, count_distinct, etc…)
* **SQL - **The sql for the column you want the metric to reference

```yaml
metrics:
  - name: total_wei_transferred
    description: The total value transferred in wei
    type: sum
    sql: value

  - name: num_eth_transactions
    description: The total number of eth transactions
    type: count

  - name: total_eth_transferred
    description: The total number of eth transferred
    type: sum
    sql: 'value / 1000000000000000000'
```

These are the supported aggregations:

```python
class MetricType(str, Enum):
    SQL = 'sql'
    SUM = 'sum'
    AVG = 'avg'
    MIN = 'min'
    MAX = 'max'
    COUNT = 'count'
    COUNT_DISTINCT = 'count_distinct'
```

You can use the SQL metric type to specify any aggregation in SQL. For example:

```yaml
metrics:
  - name: num_zero_value_transactions
    description: The total amount of transactions that transferred zero wei
    type: sql
    sql: SUM(CASE WHEN (value = 0) THEN 1 ELSE 0 END)
```

## Complex Metrics

If you have more complex requirements for metrics, instead of a table you can write any SQL query to build metrics on top of. This removes any limitations and enables you to build arbitrarily complex metrics in Metlo.

```yaml
name: covid_metrics
owner: akshay
datasource: metlo_bigquery
description: ...
derived_table: true
table: >
    SELECT *
    FROM bigquery-public-data.covid19_open_data.covid19_open_data
    WHERE aggregation_level = 0
```
