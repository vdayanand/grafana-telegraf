## Usage

The following assumes you're running the grafana dashboard and database on the
computer which is being monitored with telegraf.

1. Move .env.example to .env and set password to something random.
2. Run `docker-compose up -d`
3. Ensure you can access TCP port 3001 on your host.
    * If running in AWS, SSH port forwarding is is a good option. It's secure,
      avoids the need to modify AWS security group rules for your instance, and
      protects http traffic when interacting with grafana:
      ```
      ssh -N -i $aws_key -L 127.0.0.1:3001:localhost:3001 $your_aws_host
      ```
      (Here, `localhost` is from the point of view of `$your_aws_host`, and
       `127.0.0.1` refers to your laptop, allowing only local connections to
       itself.)
4. Configure datasource:
    1. Go to `<grafanaurl>/datasources` (in this case it will be http://localhost:3001/datasources)
    2. Add Influx DB
    3. Configure Influx HTTP endpoint (http://influxdb:8086 - the grafana
       backend can find this server name via the internal docker network.)
    4. Set Database name `telegraf_metrics`
    5. Credentials and your host name as set in `.env`
5. Setup dashboards
   1. System metrics:
      a. Go to http://localhost:3001/dashboard/import
      b. Upload json file from `dashboards/system.json`
   1. Process metrics:
      a. Go to http://localhost:3001/dashboard/import
      b. Upload json file from `dashboards/procstat.json`
