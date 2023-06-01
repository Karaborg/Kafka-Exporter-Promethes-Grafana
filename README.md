# JMX EXPORTER
### ADD JAVA PATH
`export PATH=$PATH:/tmp/furkan/jdk-11/bin`

### ADD TO ZOOKEEPER START SH INSIDE EXTRA_ARGS PARAMETER
`-javaagent:/tmp/furkan/jmx_prometheus.jar=7070:/tmp/furkan/zookeeper.yml`

### ADD TO KAFKA START SH INSIDE EXTRA_ARGS PARAMETER
`-javaagent:/tmp/furkan/jmx_prometheus.jar=7071:/tmp/furkan/kafka.yml`

> RESTART KAFKA AND ZOOKEEPER

### CHECK IF 7070 PORT IS LISTENING
`netstat -tlnp | grep 7070`

### CHECK IF 7071 PORT IS LISTENING
`netstat -tlnp | grep 7071`

### CHECK METRICS
`curl -s <KAFKA_IP>:7071 | grep -i kafka`

> OPEN FIREWALL FOR 7071

> ADD IP AND PORT AS TARGET IN PROMETHEUS YML FILE

### START GRAFANA
`./tmp/furkan/grafana/bin/grafana-server --config /tmp/furkan/grafana/conf/defaults.ini --homepath /tmp/furkan/grafana/ --tracing &`

> CHOOSE LOCALHOST:9090 AS DATASOURCE

# KAFKA EXPORTER
`./kafka_exporter  --kafka.server=<KAFKA_IP>:<KAFKA_PORT>  --sasl.enabled --sasl.username=<KAFKA_SASL_USERNAME> --sasl.password="<KAFKA_SASL_PASSWORD>" --sasl.mechanism="plain" --kafka.version=3.3.1 --log.enable-sarama`

> OPEN FIREWALL FOR 9308

> ADD IP AND PORT AS TARGET IN PROMETHEUS YML FILE
> YOUR TARGET WILL BE <IP>:<PORT>/metrics

### START GRAFANA
`./tmp/furkan/grafana/bin/grafana-server --config /tmp/furkan/grafana/conf/defaults.ini --homepath /tmp/furkan/grafana/ --tracing &`

> CHOOSE LOCALHOST:9090 AS DATASOURCE

# GRAFANA ALARM
### ALERTING > NOTIFICATION CHANNELS > NEW CHANNEL

### OPEN ANY DASHBOARD > EDIT PANEL > ALERT

