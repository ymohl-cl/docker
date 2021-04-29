# GOSDL2_WINDOWS

Docker image base from debian to expose gcc compiler with SDL2 library to build project to windows

[![Docker Cloud Automated build](https://img.shields.io/docker/cloud/automated/ymohlcl/gosdl2_windows?style=flat-square)](https://hub.docker.com/repository/docker/ymohlcl/gosdl2_windows/builds)
[![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/ymohlcl/gosdl2_windows?style=flat-square)](https://hub.docker.com/repository/docker/ymohlcl/gosdl2_windows/builds)
[![Docker hub](https://img.shields.io/badge/docker-hub-informational?style=flat-square)](https://hub.docker.com/repository/docker/ymohlcl/gosdl2_windows)

## Dependencies

The lib SDL2 was composed from the [official sources](https://libsdl.org/)

Includes components (x86-64 && i686):

* [image](https://www.libsdl.org/projects/SDL_image/)
* [mixer](https://www.libsdl.org/projects/SDL_mixer/)
* [net](https://www.libsdl.org/projects/SDL_net/)
* [ttf](https://www.libsdl.org/projects/SDL_ttf/)

Use the gcc support compiler to windows [mingw-w64](http://mingw-w64.org/doku.php)

## Example usage

``` Dockerfile
# Golang context
From golang:latest

COPY --from=ymohlcl/gosdl2_windows /usr/x86_64-w64-mingw32 /usr/x86_64-w64-mingw32
COPY --from=ymohlcl/gosdl2_windows /usr/i686-w64-mingw32 /usr/i686-w64-mingw32

# COPY go sources files here
COPY . .

# Compilation
RUN CGO_ENABLED=1 CC=x86_64-w64-mingw32-gcc GOOS=windows GOARCH=amd64 go build -tags static -ldflags "-s -w" .
```
