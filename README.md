# OpenTelemetry Tracer Bridge

> OpenTracing Bridge for OpenTelemetry Tracers

[![Build Status](https://travis-ci.org/opentracing-contrib/java-opentelemetry-bridge.svg?branch=master)](https://travis-ci.org/opentracing-contrib/java-opentelemetry-bridge)
[![Coverage Status](https://coveralls.io/repos/github/opentracing-contrib/java-opentelemetry-bridge/badge.svg?branch=master)](https://coveralls.io/github/opentracing-contrib/java-opentelemetry-bridge?branch=master)
[![Javadocs](https://www.javadoc.io/badge/io.opentracing.contrib/opentelemetry-bridge.svg)](https://www.javadoc.io/doc/io.opentracing.contrib/opentelemetry-bridge)
[![Released Version](https://img.shields.io/maven-central/v/io.opentracing.contrib/opentelemetry-bridge.svg)](https://mvnrepository.com/artifact/io.opentracing.contrib/opentelemetry-bridge)

The <ins>OpenTelemetry Tracer Bridge</ins> is a <ins>Trace Exporter</ins> that uses the [OpenTelemetry OpenTracing Shim](https://github.com/open-telemetry/opentelemetry-java) to provide a `TracerFactory` implementation (specified by the [OpenTracing TracerResolver](https://github.com/opentracing-contrib/java-tracerresolver)).

Tracer parameters can be configured via the system properties:

## Parameters

<ins>OpenTelemetry Tracer Bridge</ins> parameters use the prefix `ot.otel.`:

| Parameter                             | Use          | Description |
|---------------------------------------|--------------|-------------|
| `ot.otel.exporter`                    | Optional     | Name of the OpenTelemetry exporter:<br>`jaeger`, `inmemory`, or `logging`. |
| `ot.otel.exporter.reportOnlySampled`  | Optional     | Whether only sampled spans should be reported. |

If `ot.otel.exporter=jaeger`, the following parameters apply to the Jaeger exporter:

| Parameter                             | Use          | Description |
|---------------------------------------|--------------|-------------|
| `ot.otel.exporter.jaeger.serviceName` | **Required** | The service name. |
| `ot.otel.exporter.jaeger.address`     | **Required** | Target address (`<HOST:PORT>`) of the Jaeger gRPC endpoint. |
| `ot.otel.exporter.jaeger.deadline`    | Optional     | The max waiting time for the collector to process each span batch. |

## Usage with SpecialAgent

The <ins>[OpenTracing SpecialAgent](https://github.com/opentracing-contrib/java-specialagent)</ins> automatically instruments 3rd-party libraries in Java applications. Starting with <ins>SpecialAgent v1.5.2</ins> (usage updated to spec of <ins>SpecialAgent v1.7.0</ins>), the <ins>OpenTelemetry Tracer Bridge</ins> is included as a [<ins>Trace Exporter</ins>](https://github.com/opentracing-contrib/java-specialagent/#42-trace-exporters), which allows traces to be sent to OpenTelemetry tracers. The <ins>OpenTelemetry Tracer Bridge</ins> can be enabled with the `-Dsa.exporter=otel` property:

```bash
java -javaagent:opentracing-specialagent-1.7.0.jar \
     -Dsa.exporter=otel \
     -Dot.otel.exporter=jaeger \
     -Dot.otel.exporter.jaeger.serviceName=myService \
     -Dot.otel.exporter.jaeger.address=127.0.0.1:1234 \
     -jar MyService.jar
```

## License

This project is licensed under the Apache 2 License - see the [LICENSE.txt](LICENSE.txt) file for details.