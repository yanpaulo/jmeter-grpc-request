# JMeter GRPC Request

<p align="center"><img src="./dist/asset/jmeter-and-grpc.png" width="600px" alt="Apache JMeter and gRPC logo" /></p>

<h4 align="center">This sampler JMeter lets you send an gRPC request to a server. </br> It's as simple as an HTTP Request.</h4>
<br>

[![Javadocs](https://www.javadoc.io/badge/org.apache.jmeter/ApacheJMeter_core.svg)](https://www.javadoc.io/doc/org.apache.jmeter/ApacheJMeter_core)
[![Stack Overflow](https://img.shields.io/:stack%20overflow-jmeter-brightgreen.svg)](https://stackoverflow.com/questions/tagged/jmeter)

## What is it

This is a simpler of JMeter used to test for any gRPC server, it is not necessary to generate gRPC classes or to compile the protos binary for the service. Just a very simple for input:

- Host and port of gRPC service.
- Method of service needs testing.
- Folder path of proto files.
- Data request in JSON format.

Same as JMeter HTTP Request but for gRPC. Copy only once file jar to lib/ext of JMeter, select your protobuf folder and start making requests! No extra steps.

*The JMeter gRPC Request is available at JMeter Plugins Manager, we can find here https://jmeter-plugins.org/?search=jmeter-grpc-request*

## Features

- Supports Blocking Unary Calls.
- Parses proto files at runtime.
- Supports plain text and TLS connections.
- Supports authentication via metadata (JWT/Token).
- Request data with JSON format.
- Runs on Mac, Linux and build project by Maven.

*Todo:*

- [x] *Supports TLS connections.*
- [x] *Supports authentication via metadata.*
- [x] *Auto list full methods.*
- [x] *Count the failed request in the report.*
- [ ] *Supports grpc-web protocol (HTTP1.1).*
- [ ] *Auto generate request data base on proto file.*

## Usage

<p align="center"><img src="./dist/asset/jmeter-grpc-create-testscript.gif" width="820px" alt="jmeter-create-testscript-grpc" /></p>

### Requirements

All you need copy *jmeter-grpc-request* file jar to directory `lib/ext` of JMeter and restart JMeter GUI (copy once, use forever). Binary are available from the [dist/bin](./dist/bin/) directory.

### Making a gRPC request with JMeter

Create test script:

- Add Thread Group: right-click on the Sample Test (our Test Plan) → Add → Threads (Users) → Thread Group.
- Add GRPC Request: right-click on the newly created Thread Group  → Add → Sampler → GRPC Request.
- Fill info request: host, port, method, data request, proto folder.
- Save test script.

Run test:

- Via JMeter GUI: in top bar click Run → Start.
- Via command line: `bin/jmeter -n -t <test JMX file>.jmx -l <test JMX result>.csv -j <test log file>.log -e -o <Path to output folder>`.

### Configurations

| No. 	| Fields                             	| Description                                                         	|
|-----	|-----------------------------------	|---------------------------------------------------------------------	|
| 1   	| Server Name or IP                 	| Domain/IP for gRPC server                                         	|
| 2   	| Port Number                       	| Port for gRPC server (80/ 443)                                      	|
| 3   	| SSL/TLS                           	| SSL/TLS to authenticate the server                                  	|
| 4   	| Proto Root Directory              	| Root directory contains proto files                                 	|
| 5   	| Library Directory (Optional)      	| Using a different underlying library (googleapis)                   	|
| 6   	| Full Method                       	| Full Method to test                                                 	|
| 7   	| Metadata                          	| Store token, authentication method, format: key1:value1,key2:value2                                  	|
| 8   	| Deadline                          	| How long gRPC clients are willing to wait for an RPC to complete  	|
| 9   	| Send JSON Format With the Request 	| Data request with JSON format                                       	|

## Running the examples

Example invocations can be found in the [example](./dist/example) directory.

## Benchmark

Purpose verify that *jmeter-grpc-request* is really stable when performing load testing for the gRPC system. Read more [Benchmark: jmter-grpc-request](./dist/benchmark)

- CCU: 120 user
- Duration: 30 min

<img src= "./dist/asset/report-120-1800s.jpg" />

## Build instructions

### Build requirements

In order to build JMeter GRPC Request from source, you will need:

- [Java 8](https://www.oracle.com/downloads/index.html)
- [Apache Maven 3](https://maven.apache.org/)

### Build from source

Build a (fat) jar output in target directory, run:

```
mvn clean install package
```

## Inspiration...

- Thanks: [grpc-ecosystem/polyglot](https://github.com/grpc-ecosystem/polyglot)
- More: https://stackoverflow.com/q/61133529/9488752
- If you like working with the request message builder at here [zalopay-oss/jmeter-grpc-plugin](https://github.com/zalopay-oss/jmeter-grpc-plugin)

## Fork by yanpaulo

This fork was created to add some features which were not available on the original plugin by zalopay-oss as listed below:
- Support for TLS NPN fallback when ALPN isn't supported. 
- Support for relative paths in the "Proto Root" and "Library Directory" fields.

Please note that both ALPN and NPN require at least OpenJDK 8u252 as of https://github.com/jetty-project/jetty-alpn-agent, https://mail.openjdk.java.net/pipermail/jdk8u-dev/2020-April/011566.html, https://mail.openjdk.java.net/pipermail/jdk8u-dev/2019-November/010573.html