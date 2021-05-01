# GOSDL2

Docker image base from golang to expose golang compiler with sdl2 library

[![Docker Cloud Automated build](https://img.shields.io/docker/cloud/automated/ymohlcl/gosdl2?style=flat-square)](https://hub.docker.com/repository/docker/ymohlcl/gosdl2/builds)
[![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/ymohlcl/gosdl2?style=flat-square)](https://hub.docker.com/repository/docker/ymohlcl/gosdl2/builds)
[![Docker hub](https://img.shields.io/badge/docker-hub-informational?style=flat-square)](https://hub.docker.com/repository/docker/ymohlcl/gosdl2)

## Dependencies

Includes sdl2 components (x86-64 && i686):

* image
* mixer
* net
* ttf

To compile you project, you can use this binaries depends on your context

``` bash
# Linux binary
CC=clang GOOS=linux GOARCH=amd64
```

``` bash
# Windows binary
CC=x86_64-w64-mingw32-gcc GOOS=windows GOARCH=amd64
```

``` bash
# OSX
CC=x86_64-apple-darwin20.2-clang GOOS=darwin GOARCH=amd64
```

## Example usage

``` Dockerfile
From ymohl/gosdl2:latest

# COPY go sources files here
COPY . .

# Compilation to windows
RUN CGO_ENABLED=1 CC=x86_64-w64-mingw32-gcc GOOS=windows GOARCH=amd64 go build -tags static -ldflags "-s -w" .

# Compilaton to osx
RUN CGO_ENABLED=1 CC=x86_64-apple-darwin20.2-clang GOOS=darwin GOARCH=amd64 go build -tags static -ldflags "-s -w" .

# Compilation to linux
RUN CC=clang GOOS=linux GOARCH=amd64 go build -tags static -ldflags "-s -w"
```
