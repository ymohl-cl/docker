FROM debian:latest as deps

ARG OSX_VERSION=11.0
ARG OSX_SDK_LINK=https://github.com/joseluisq/macosx-sdks/releases/download/11.1/MacOSX11.1.sdk.tar.xz
ARG OSXCROSS_GIT=https://github.com/tpoechtrager/osxcross.git
ENV MACOSX_DEPLOYMENT_TARGET=${OSX_VERSION}
ENV OSX_VERSION_MIN=${OSX_VERSION}

# update linux dependencies to osxcross build
RUN apt-get update -qq && apt-get install -y cmake \
			git \
			wget \
			patch \
			bzip2 \
			libxml2-dev \
			libssl-dev \
			zlib1g-dev \
			xz-utils \
			clang

# clone osxcross repo
RUN git clone ${OSXCROSS_GIT} /usr/osxcross
RUN wget -P /usr/osxcross/tarballs ${OSX_SDK_LINK}

# osxcross dependencies building
WORKDIR /usr/osxcross
RUN ./tools/get_dependencies.sh
RUN UNATTENDED=yes ./build.sh

FROM debian:latest as artifact

COPY --from=deps /usr/osxcross /usr/osxcross

ENTRYPOINT [ "/bin/bash" ]