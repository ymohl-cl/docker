ARG GO_VERSION=latest

# Golang image to build crossplatform project with SDL2
FROM golang:$GO_VERSION

ARG CLANG_VERSION=12

# get sdl2 and tooling dependencies need to build go project
RUN apt-get update -qq && apt-get install -y libsdl2-dev \
			libsdl2-ttf-dev \
			libsdl2-gfx-dev \
			libsdl2-image-dev \
			libsdl2-mixer-dev \
			libsdl2-net-dev \
			libsdl2-ttf-dev \
			libgtk-3-dev \
			mingw-w64 \
			gnupg \
			gnupg1 \
			gnupg2 \
			software-properties-common

# get mandatories files
COPY --from=ymohlcl/gosdl2_windows:0.0.1 /usr/x86_64-w64-mingw32 /usr/x86_64-w64-mingw32
COPY --from=ymohlcl/gosdl2_windows:0.0.1 /usr/i686-w64-mingw32 /usr/i686-w64-mingw32
COPY --from=ymohlcl/osxcross:0.0.1 /usr/osxcross /usr/osxcross

# get clang / llvm
WORKDIR /usr/llvm
RUN wget https://apt.llvm.org/llvm.sh
RUN chmod +x llvm.sh
RUN ./llvm.sh ${CLANG_VERSION}

# set binaries in env path
ENV PATH=/usr/lib/llvm-${CLANG_VERSION}/bin:$PATH
ENV PATH=$PATH:/usr/osxcross/target/bin

WORKDIR $GOPATH
