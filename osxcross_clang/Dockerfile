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
			xz-utils


# clone osxcross repo
WORKDIR /usr
RUN git clone ${OSXCROSS_GIT}

# get osx's sdk and put it on tarball forlder
WORKDIR /usr/osxcross/tarballs
RUN wget ${OSX_SDK_LINK}

# osxcross dependencies building
WORKDIR /usr/osxcross
RUN ./tools/get_dependencies.sh
RUN UNATTENDED=yes INSTALLPREFIX=/opt/clang ./build_clang.sh \
	&& cd /usr/osxcross/build/llvm-10.0.1.src/build_stage2 \
	&& make install \
	&& cd -
RUN UNATTENDED=yes ./build.sh

FROM debian:latest as artifact

COPY --from=deps /usr/osxcross /usr/osxcross
COPY --from=deps /opt/clang /opt/clang
# export PATH=/opt/clang/bin/:$PATH to use binary clang