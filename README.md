# Realtime-API-Monitoring

Realtime monitoring using Python (Django) & Golang as programming languages, Postgresql & Influxdb as databases, Grafana and Docker. 
This project is under development.

<p align="center">
  <img src="https://i.imgur.com/lHWP9YC.jpg">
</p>
1. End user <br>
2. On django admin pannel you can enter endpoint api details such as uri, headers, body, etc. <br>
3. Django dashboard project stores request details to postgresql.
4. Postgresql stores Endpoint API's and can be used to monitoring.
5. As a time series database, influxdb will store response logs.

## Docker Containers
First, run Postgresql container on port 5434 and credentails (DB Name, USER, Password) to store API request details. <br>
    
```bash
docker run --name postgresql -d \
    -p 5434:5432 \
    --env 'DB_NAME=YOUR_POSTGRES_NAME' \
    --env 'DB_USER=YOUR_POSTGRES_USER' --env 'DB_PASS=YOUR_POSTGRES_PASSWORD' \
    --env 'DB_EXTENSION=pg_trgm' \
    --volume /srv/docker/postgres/api:/var/lib/postgresql_api \
    postgres:latest
```
Then, run `InfluxDB` container to store golang api core request results.
```
docker run --name influxdb -d \
    -p 8086:8086 -p 8083:8083 \
    -v /srv/docker/influxdb:/var/lib/influxdb \
    -e INFLUXDB_ADMIN_ENABLED=true \
    influxdb
```
Run grafana to see Restfull API chart logs. 
```
docker run --name grafana -d \
  -p 3000:3000 \
  -e "GF_SERVER_ROOT_URL=http://127.0.0.1" \
  -e "GF_SECURITY_ADMIN_PASSWORD=GRAFANA_ADMIN_PASSWORD" \
  grafana/grafana

```
