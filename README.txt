More details on this repo can be found in my medium article
https://medium.com/@dhanushkasampath.mtr/setup-prometheus-and-grafana-locally-to-monitor-the-behaviour-of-a-spring-boot-application-de93c7c3a469




setup Prometheus and grafana locally and monitor its behaviour


prometheus is a time series data base that polls data and shows in timeseries format



docker compose up

main directory/data/prometheus/config/prometheus.yaml


====================
after running the application with prometheus and actuator dependencies we can call below endpoint
http://localhost:2020/actuator/prometheus

it will give labels and its attributes
(image app-row-data)



=====================



main_directory/docker-compose.yaml


prometheus url : http://localhost:9090
grafana url: http://localhost:3000

====================================

GRAFANA

1. default password admin/admin

2. after starting grafana first thing we need to do is configure the datasouce by giving prometheus url

configuration->data sources -> Add data source -> Prometheus
(image data-source-config)

3. create first dashboard

create -> Dashboard -> Add a new panel -> in the Metrics browser search for the label that we want



search for log_back_events. cz we are interested to various warning logs we are generating once we hit an endpoint

"logback_events_total{}"
======================================

we dont want the number of error logs or warn logs. what we want is the rate of them**********

metric browser
rate(logback_events_total{level="warn"}[1m])  <- this will show the number of warning logs that were generated over a perioud of 1 minute

after setting the correct label in metric browser, click on Apply. then that panel will be shown in the dashboard. we can set auto refresh to any time. 5s, 10s, 30s, etc...


(image dashboard-1 )


we can add more panel as like this. But we dont hava to create all by our own. There are community dashboards available for free.
we can import them as a json file.

+ -> import -> Upload JSON file 




usecase:
identify the slow service by prometheus and grafana




