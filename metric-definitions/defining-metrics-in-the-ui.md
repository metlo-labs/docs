---
description: Making Metlo Metric Definitions in the UI.
---

# Defining Metrics in the UI

## Creating a New Definition

A new metric definition can be created by clicking the `+ Definition` button on the definitions page.

![](<../.gitbook/assets/Screen Shot 2021-10-13 at 10.06.27 AM.png>)

## Metadata

To make a definition you first have to supply some metadata:

* **Name -** The name of the definition. This name is unique and will be used as a namespace for every metric you build inside of it.
* **Owner -** The user that owns this definition
* **Datasource -** The id of the database connection this definition will use
* **Description -** A friendly description that describes what type of metrics and dimensions this definition will contain.
* **Table -** The table metrics and dimensions inside this definition will be built on top of

![](<../.gitbook/assets/Screen Shot 2021-10-21 at 4.11.07 PM.png>)

If you want to build more complicated metrics you can enable SQL and use a `SELECT` query instead of a table name. Here is  an example using BigQuery's public covid dataset.

![](<../.gitbook/assets/Screen Shot 2021-10-21 at 4.13.27 PM.png>)

_Note: Be sure to select all the columns you want to build metrics and dimensions with in this query_

## Dimensions

After you define the metadata for a definition, the next step is defining the dimensions you can slice and dice a metric by. Each dimension takes the following info

* **Name - **A unique name for the dimension
* **Description -** A friendly description for the dimension
* **Column -** The column you want the dimension to reference (This can also be a SQL Expression)

![](<../.gitbook/assets/Screen Shot 2021-10-21 at 4.19.13 PM.png>)

_Note: You need to specify at least one time dimension in each definition_

## Metrics

Metrics are the actual aggregations on top of the table that you care about. Each metric has the following fields:

* **Name -** The name of the metric
* **Description -** A friendly description for the metric
* **Type -** The type of metric. This can be an aggregation (sum, count, count\_distinct, etc…)
* **Column -** The column you want the metric to reference
* **\[Optionals] Filters - **Any filters you want to apply when computing the metric

![](<../.gitbook/assets/Screen Shot 2021-10-21 at 4.35.04 PM.png>)

The column can also be a SQL Expression. For example, if you wanted to find the percent of rows where `final_status` is equal to `'completed'`, you could take the average of the column `CASE WHEN final_status = 'completed' THEN 1 ELSE 0 END`.

![](<../.gitbook/assets/Screen Shot 2021-10-21 at 4.45.20 PM.png>)

A custom SQL aggregation can be written by using the `SQL` metric type:

![](<../.gitbook/assets/Screen Shot 2021-10-21 at 4.55.02 PM.png>)
