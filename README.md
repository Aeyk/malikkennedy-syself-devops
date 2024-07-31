# Chart
A sample chart to deploy an application. It's using Wordpress as a
placeholder, and is missing a required MySQL compatible database, to
add it change the NetworkPolicy to allow them to connect, the values
to specify database information like hostname, replicas, external or
helm-managed, another config-map for any database configuration, and a
stateful set to actually run the database if it's helm-managed.
