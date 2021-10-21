---
description: A guide on how to make Metric Health Checks in the UI.
---

# Creating Metric Health Checks

Metric health checks are created per definition. You can view health checks on the definition page by clicking on health check button on the top right:

![](<../.gitbook/assets/Screen Shot 2021-10-21 at 11.24.27 AM.png>)

This page then shows a list of all the health checks that have already been created. The new health check button is on the top right:

![](<../.gitbook/assets/Screen Shot 2021-10-21 at 11.44.30 AM.png>)

## Info

The first step is to enter some basic metadata for your health check:

* **Name -** The name of the health check
* **Metric Name -** The metric you want to define this health check on
* **Enabled -** Should this health check run or not

![](<../.gitbook/assets/Screen Shot 2021-10-21 at 11.49.45 AM.png>)

## Granularity

The next step is to define the granularity you want your health check to run on. For example, if you wanted to define constraints on the metric `total_eth_transactions` per `block_number` per `day` you would set the time granularity to day and add the dimension `block_number` to groups.

![](<../.gitbook/assets/Screen Shot 2021-10-21 at 12.22.24 PM.png>)

You can also add filters on dimensions to only run your health check on a subset of your data. If we wanted to define this health check for a certain `sender`, we could add the following filter:

![](<../.gitbook/assets/Screen Shot 2021-10-21 at 12.32.45 PM.png>)

## Constraints

After you define the granularity you can define rules for a metric in constraints. If we want this metric (at the granularity we defined earlier) to always be `NOT NULL` and greater than `10`, we would define the following constraints:

![](<../.gitbook/assets/Screen Shot 2021-10-21 at 12.34.21 PM.png>)

## Schedule

You can define the cadence you want your health check to run on at a hourly, daily or weekly granularity. All times are in UTC.

![](<../.gitbook/assets/Screen Shot 2021-10-21 at 12.57.19 PM.png>)
