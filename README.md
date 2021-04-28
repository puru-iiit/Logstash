# Logstash and Osquery
Logstash and osquery configuration steps


## Command to run the osqueryd
```
./usr/local/bin/osqueryd --D --config_path=$(pwd)/osquery.example.conf --database_path=/home/app/logs/osquery/ --pidfile=$(pwd)/pidfile --logger_path=/home/app/logs/osquery --socket=/home/appusr/.osquery/shell.em &

```

## Check the osqueryd log
```
tail -10f /home/app/logs/osquery/osqueryd.snapshots.log
```

## logstash conf file placing and way to configure the logstash to create one pipeline for each conf file

1. Make folder app_name at location ***./config*** and place the ***.conf*** files at this location.

2. Make below entries in ***pipelines.yml***(it will be available at location :***./config/pipelines.yml***)

```
- pipeline.id: app_gc
  pipeline.workers: 1
  path.config: "./config/app_name/app_gc.conf"

- pipeline.id: application
  pipeline.workers: 1
  path.config: "./config/app_name/application.conf"
  
```

## Command to run the logstash
```
nohup ./bin/logstash &
```