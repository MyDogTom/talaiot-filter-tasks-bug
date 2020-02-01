Example project for the https://github.com/cdsap/Talaiot/issues/140 bug.

When `./gradlew DummyTask` is executed, `InfluxDbPublisher` fails with

```
[InfluxDbPublisher]: ================
[InfluxDbPublisher]: InfluxDbPublisher
[InfluxDbPublisher]: publishBuildMetrics: true
[InfluxDbPublisher]: publishTaskMetrics: false
[InfluxDbPublisher]: ================
[InfluxDbPublisher]: Creating db tracking
[InfluxDbPublisher]: Sending points to InfluxDb server BatchPoints [database=null, retentionPolicy=rpTalaiot, consistency=ONE, tags={}, precision=NANOSECONDS, points=[Point [name=build, time=1580559475776, tags={cacheMode=local, cpuCount=8, gradleVersion=6.1.1, javaVmName=1.8.0_232-b09, osVersion=Mac OS X-10.14.6, requestedTasks=DummyTask, rootProject=talaiot-filter-tasks-bug, switch.cache=false, switch.configurationOnDemand=false, switch.daemon=false, switch.dryRun=false, switch.parallel=false, switch.refreshDependencies=false, switch.rerunTasks=false, switch.scan=false, username=svyatoslav.chatchenk}, precision=MILLISECONDS, fields={cacheRatio=NaN, configuration=880, cpuCount=8, duration=886, gitBranch=master, gitUser=undefined, gradleVersion=6.1.1, javaVmName=1.8.0_232-b09, javaXmxBytes=8589934592, locale=en, maxWorkers=4, osVersion=Mac OS X-10.14.6, requestedTasks=DummyTask, rootProject=talaiot-filter-tasks-bug, start=1.58055947489E12, success=true, totalRamAvailableBytes=5314068480, username=svyatoslav.chatchenk}]]]
[InfluxDbPublisher]: InfluxDbPublisher-Error-Executor Runnable: unable to parse 'build,cacheMode=local,cpuCount=8,gradleVersion=6.1.1,javaVmName=1.8.0_232-b09,osVersion=Mac\ OS\ X-10.14.6,requestedTasks=DummyTask,rootProject=talaiot-filter-tasks-bug,switch.cache=false,switch.configurationOnDemand=false,switch.daemon=false,switch.dryRun=false,switch.parallel=false,switch.refreshDependencies=false,switch.rerunTasks=false,switch.scan=false,username=svyatoslav.chatchenk cacheRatio=�,configuration=880i,cpuCount=8i,duration=886i,gitBranch="master",gitUser="undefined",gradleVersion="6.1.1",javaVmName="1.8.0_232-b09",javaXmxBytes=8589934592i,locale="en",maxWorkers=4i,osVersion="Mac OS X-10.14.6",requestedTasks="DummyTask",rootProject="talaiot-filter-tasks-bug",start=1580559474890.0,success=true,totalRamAvailableBytes=5314068480i,username="svyatoslav.chatchenk" 1580559475776000000': invalid boolean
```

Before running you have to run local Docker image with:
```
docker run -d \
  -p 3003:3003 \
  -p 3004:8083 \
  -p 8086:8086 \
  -p 22022:22 \
  -v /var/lib/influxdb \
  -v /var/lib/grafana \
  cdsap/talaiot:latest
```
