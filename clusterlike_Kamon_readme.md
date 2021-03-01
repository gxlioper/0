# Kamon
 
[![Build Status](https://travis-ci.org/kamon-io/Kamon.svg?branch=master)](https://travis-ci.org/kamon-io/Kamon)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/kamon-io/Kamon?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.kamon/kamon-core_2.12/badge.svg)](https://maven-badges.herokuapp.com/maven-central/io.kamon/kamon-core_2.12)

Kamon is a set of tools for monitoring applications running on the JVM.

### Getting Started

Kamon is currently available for Scala 2.10, 2.11 and 2.12.

Supported releases and dependencies are shown below.

| kamon  | status | jdk  | scala            | akka   |
|:------:|:------:|:----:|------------------|:------:|
|  0.6.5 | stable | 1.7+, 1.8+ | 2.10, 2.11, 2.12  | 2.3.x, 2.4.x |

To get started with SBT, simply add the following to your `build.sbt`
file:

```scala
libraryDependencies += "kamon.io" %% "kamon-core" % "0.6.5"
```

### Documentation

Kamon information and documentation is available on the
[website](http://kamon.io).

### Modules ###

* [Play Framework]
* [Spray]  
* [Akka]
* [Akka Remote]
* [Akka Http]  
* [Scala]  
* [Annotation]
* [System Metrics]
* [JDBC]  
* [Elasticsearch]

### Backends ###

* [Log Reporter]
* [StatsD]
* [Datadog]
* [SPM]
* [InfluxDB]
* [New Relic]  
* [FluentD]
* [JMX]
* [Riemann]  
* [Khronus]  


### Projects using Kamon ###

If you have a project you'd like to include in this list, either open a PR or let us know in [the gitter channel](https://gitter.im/kamon-io/Kamon) and we'll add a link to it here.

* [kamon-prometheus](https://github.com/MonsantoCo/kamon-prometheus): A Kamon backend to support Prometheus
* [spray-kamon-metrics](https://github.com/MonsantoCo/spray-kamon-metrics): Better Kamon metrics for Spray services
* [camel-kamon](https://github.com/osinka/camel-kamon): Kamon metrics and traces for Apache Camel routes, processors
* [kamon-play-extensions](https://github.com/agiledigital/kamon-play-extensions): Kamon extensions for use in Play2 applications.
* [kamon-logstash](https://github.com/darienmt/kamon-logstash): Kamon-logstash backend module.

## License

This software is licensed under the Apache 2 license, quoted below.

Copyright © 2013-2016 the kamon project  

Licensed under the Apache License, Version 2.0 (the "License"); you may not
use this file except in compliance with the License. You may obtain a copy of
the License at

    [http://www.apache.org/licenses/LICENSE-2.0]

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
License for the specific language governing permissions and limitations under
the License.


[Play Framework]: https://github.com/kamon-io/kamon-play
[Spray]: https://github.com/kamon-io/kamon-spray
[Akka]:https://github.com/kamon-io/kamon-akka                                          
[Akka Remote]: https://github.com/kamon-io/kamon-akka-remote
[Akka Http]: https://github.com/kamon-io/kamon-akka-http
[Scala]: https://github.com/kamon-io/kamon-scala
[Annotation]: https://github.com/kamon-io/kamon-annotation
[System Metrics]: https://github.com/kamon-io/kamon-system-metrics
[JDBC]: https://github.com/kamon-io/kamon-jdbc
[Elasticsearch]: https://github.com/kamon-io/kamon-elasticsearch

[Log Reporter]: https://github.com/kamon-io/kamon-log-reporter
[SPM]: https://github.com/kamon-io/kamon-spm
[Datadog]: https://github.com/kamon-io/kamon-datadog
[FluentD]: https://github.com/kamon-io/kamon-fluentd
[JMX]: https://github.com/kamon-io/kamon-jmx
[StatsD]: https://github.com/kamon-io/kamon-statsd
[Riemann]: https://github.com/kamon-io/kamon-riemann
[Khronus]: https://github.com/kamon-io/kamon-khronus
[New Relic]: https://github.com/kamon-io/kamon-newrelic
[InfluxDB]: https://github.com/kamon-io/kamon-influxdb


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)