# Streaming

Metlo currently uses [Materialize](https://materialize.com) to stream metric data. You can build metrics on top of any stream of data that Materialize Supports.

## Creating Sources

Follow Materializes [Documentation](https://materialize.com/docs/sql/create-source/) to create a new source. For this example we will connect a Kinesis Stream of trip data for a rideshare service by running the following SQL:

```sql
CREATE SOURCE rideshare_trips_kinesis_stream
FROM KINESIS ARN 'arn:aws:kinesis:us-east-2:************:stream/metlo-demo-ridesharetrips-v2' WITH (
    access_key_id = '********************',
    secret_access_key = '****************************************'
)
FORMAT BYTES;
```

This Kinesis stream has trip data in the following JSON format:

```javascript
{
    "SequenceNumber": "49622401206323627989047709162250321742275053250653716498",
    "ApproximateArrivalTimestamp": "2021-09-27T13:09:50.044000",
    "data": {
        "date": "2021-09-27T20:09:49.696382",
        "uuid": "22ec9e1c-a6ab-4d30-bc93-a776ef1e4fae",
        "driver": "338119e7-8c69-4b38-b4f3-487513f69523",
        "rider": "1118e709-4edb-4ee3-b05d-fc5f4d92af96",
        "product": "SOLO",
        "city": 3,
        "final_status": "completed",
        "price": 23.55,
        "distance": 36.68,
        "trip_time": 538,
        "wait_time": 47
    },
    "PartitionKey": "202.8476711632773389.6969364"
}
```

## Adding a Stream to a Metric Definition

After you add a source you can add a stream built on top of this source in your definition file. You should use SQL (Most Postgres functions will work) to transform the source data to match the batch table you already have defined. 

In this case we will use Postgres's JSON functions to extract all the fields we want and then cast them to the correct type:

```yaml
name: rideshare_trips
owner: akshay
datasource: metlo_bigquery
description: A collection of trip metrics for Metlo's new rideshare service.
table: metricflow.test_data.rideshare_trips

stream: >
  SELECT
    CAST(data ->> 'date' as timestamp) as date,
    data ->> 'uuid' as uuid,
    data ->> 'driver' as driver,
    data ->> 'rider' as rider,
    data ->> 'product' as product,
    CAST(data -> 'city' as integer) as city,
    data ->> 'final_status' as final_status,
    CAST(data -> 'price' as float) as price,
    CAST(data -> 'distance' as float) as distance,
    CAST(data -> 'trip_time' as integer) as trip_time,
    CAST(data -> 'wait_time' as integer) as wait_time
  FROM (
    SELECT CAST(convert_from(data, 'utf8') AS jsonb) AS data
    FROM rideshare_trips_kinesis_stream
  )
```

After you add a stream to your definition file, all your metrics will support realtime queries automatically!
