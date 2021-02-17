## Usage
1. Move .env.example to .env
2. Run `docker-compose up -d`
3. Configure datasource:
    1. Go to `<grafanaurl>/datasources` (in this case it will be http://localhost:3001)
    2. Add Influx DB
    3. Configure Influx HTTP endpoint (http://influxdb:8086)
    4. Set Database name `telegraf_metrics`
    5. Credentials as set in `.env`
4. Setup dashboards
   1. System metrics:
      a. Go to http://localhost:3001/dashboard/import
      b. Upload json file from `dashboards/system.json`
   1. Process metrics:
      a. Go to http://localhost:3001/dashboard/import
      b. Upload json file from `dashboards/procstat.json`
