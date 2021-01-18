# dokku InfluxDB (beta)

InfluxDB plugin for dokku.

## disclaimer

  - This plugin is not production ready yet.

## requirements

- dokku 0.4.0+

## installation

```shell
# on 0.4.x
dokku plugin:install https://github.com/IMcD23/dokku-influxdb.git influxdb
```

## commands

```shell
influxdb:create <name>         Create new InfluxDB container
influxdb:destroy <name>        Destroy InfluxDB container
influxdb:expose <name> [port]  Expose on a custom port if provided (random port otherwise)
influxdb:exists <name>         Check if service exists
influxdb:link <name> <app>     Link InfluxDB service to the app
influxdb:logs <name> [-t]      Print the most recent log(s) for this service
influxdb:restart <name>        Graceful shutdown and restart of the InfluxDB service container
influxdb:start <name>          Start a previously stopped InfluxDB service
influxdb:stop <name>           Stop a running InfluxDB service
influxdb:unexpose <name>       Unexpose a previously exposed InfluxDB service
influxdb:unlink <name> <app>   Unlink InfluxDB service from the app
```

## usage

```shell
# create an InfluxDB service named lolipop
dokku influxdb:create lolipop

# another service can be linked to your app
dokku influxdb:link lolipop playground

# you can tail logs for a particular service
dokku influxdb:logs lolipop
dokku influxdb:logs lolipop -t # to tail

# expose docker port to the host machine
dokku influxdb:expose lolipop 8086

# finally, you can destroy the container
dokku influxdb:destroy lolipop
```

## contributing

Feel free to contribute to this project if you want to fix/extend/improve it.

## TODO

  - Implement/test InfluxDB cluster
  - ...
