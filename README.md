# FLiP-PulsarSummit

Materials for Pulsar Summit Europe 2021

This is the source and examples for the "Using the FLiPN Stack for Edge AI (Flink, NiFi, Pulsar)" 

## Creation

```

bin/pulsar-admin topics create persistent://public/default/nvidia-sensor

bin/pulsar-admin topics list public/default

bin/pulsar-client consume "persistent://public/default/nvidia-sensor-partition-0" -s "nano2gbgo" -n 0

```

## Build This in the Cloud

```
bash -c "$(curl -fsSL https://storage.googleapis.com/downloads.streamnative.cloud/snctl/install.sh)"

```

## Flink SQL Manual Table DDL

```
CREATE TABLE default_catalog.default_database.nvidiasensor
(
  `id` STRING, uuid STRING, ir STRING,
  `end` STRING, lux STRING, gputemp STRING, 
  cputemp STRING, `te` STRING, systemtime STRING, hum STRING,
 memory STRING, gas STRING, pressure STRING, 
 `host` STRING, diskusage STRING, ipaddress STRING, macaddress STRING, 
  gputempf STRING, host_name STRING,
    `runtime` STRING, cpu STRING,cputempf STRING,
  publishTime TIMESTAMP(3) METADATA,
  WATERMARK FOR publishTime AS publishTime - INTERVAL '5' SECOND
) WITH (
  'connector' = 'pulsar',
  'topic' = 'persistent://public/default/nvidia-sensor',
  'value.format' = 'json',
  'service-url' = 'pulsar://localhost:6650',
  'admin-url' = 'http://localhost:8080',
  'scan.startup.mode' = 'earliest'
);


```

## Resources

* https://github.com/tspannhw/FLiP-SQL
* https://github.com/tspannhw/Flip-iot
* https://github.com/tspannhw/FLiP-Energy
* https://github.com/tspannhw/FLiP-Jetson
* https://github.com/tspannhw/FLiP-EdgeAI
* https://pulsar-summit.org/en/event/europe-2021/sessions/Using-the-FLiPN-Stack-for-Edge-AI-Flink-NiFi-Pulsar
* https://www.datainmotion.dev/2019/09/powering-edge-ai-for-sensor-reading.html
* https://www.datainmotion.dev/2019/05/dataworks-summit-dc-2019-report.html
* https://www.datainmotion.dev/2019/03/using-raspberry-pi-3b-with-apache-nifi.html
* https://github.com/tspannhw/ApacheDeepLearning302
* https://github.com/tspannhw/minifi-xaviernx
* https://github.com/tspannhw/SpeakerProfile/tree/main/2021/talks
* https://console.streamnative.cloud/
* https://docs.streamnative.io/
