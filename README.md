# Protocol Buffers + Docker

A lightweight `protoc` Docker image, published as `qarlm/protoc` to [Docker Hub](https://hub.docker.com/repository/docker/qarlm/protoc/tags), with all dependencies built-in, to generate code in multiple languages. Forked from https://github.com/jaegertracing/docker-protobuf.

## Purpose

`gogoproto` annotations in proto files help make internal domain model types more efficient in golang, but using these proto files to generate code in other languages requires to include these dependencies anyway. The `Dockerfile` in this repo compiles all dependencies into the image, for easy code generation in multiple languages.

## Contents

`Dockerfile` configured with dependencies specific to the ML projects. 

## What's included in the image
- https://github.com/ckaznocha/protoc-gen-lint
- https://github.com/gogo/protobuf
- https://github.com/golang/protobuf
- https://github.com/google/protobuf
- https://github.com/grpc-ecosystem/grpc-gateway
- https://github.com/grpc/grpc
- https://github.com/grpc/grpc-java

## Supported languages
- C#
- C++
- Go
- Java / JavaNano (Android)
- JavaScript
- Objective-C
- PHP
- Python
- Ruby

## Usage
```
$ docker run \
        --rm \
        -v$(PWD):/protos \
        qarlm/docker-protoc \
        --working-dir /protos
        --language <lang>
        --grpc
```

For help try:
```
$ docker run --rm qarlm/protoc --help
```

### To generate language specific code

1. Make sure you have the `model.proto` file present in `${PWD}`

2. Use any of the language specific options -
```
    --language python
    --language ruby
    --language java
    --langauge python,ruby,java
```

Example for Java:
```
docker run \
   --rm \
   -v${PWD}:/protos \
   qarlm/docker-protoc:latest \
       --working-dir /protos
       --language java
       --grpc
```
