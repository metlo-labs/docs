# Connecting with JDBC

You can connect to Metlo using the Presto [JDBC Driver](https://prestodb.io/docs/current/installation/jdbc.html).

1. Download the JDBC Driver
2. Generate an api key at `https://<company>-api.metlo.com/settings`

The JDBC connection string is:

`jdbc:presto://<company>-api.metlo.com:443/hive?SSL=true&accessToken=<API_KEY>`
