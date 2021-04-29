# OSXCROSS_CLANG

Docker image based from debian to expose clang compiler to build project to OSX

[![Docker Cloud Automated build](https://img.shields.io/docker/cloud/automated/ymohlcl/osxcross_clang?style=flat-square)](https://hub.docker.com/repository/docker/ymohlcl/osxcross_clang/builds)
[![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/ymohlcl/osxcross_clang?style=flat-square)](https://hub.docker.com/repository/docker/ymohlcl/osxcross_clang/builds)
[![Docker hub](https://img.shields.io/badge/docker-hub-informational?style=flat-square)](https://hub.docker.com/repository/docker/ymohlcl/osxcross_clang)

## Dependencies

The osx builds make it with [osxcross](https://github.com/tpoechtrager/osxcross) and loads by default the sdk MacOSX11.1 provided by [Joseluisq](https://github.com/joseluisq/macosx-sdks). Thanks to him &nbsp;:wink:&nbsp;

If you want to use an other SDK or an other link to get it, you could to do with update the `OSX_VERSION` and `OSX_SDL_LINK` build ARG values.

## Example usage

``` Dockerfile
# Golang context
From golang:latest

COPY --from=ymohlcl/osxcross_clang:latest /usr/osxcross /usr/osxcross
COPY --from=ymohlcl/osxcross_clang:latest /opt/clang /opt/clang
ENV PATH=/opt/clang/bin/:$PATH

# COPY go sources files here
COPY . .

# Compilation
RUN CGO_ENABLED=1 CC=x86_64-apple-darwin20.2-clang GOOS=darwin GOARCH=amd64 go build -tags static -ldflags "-s -w" .
```
