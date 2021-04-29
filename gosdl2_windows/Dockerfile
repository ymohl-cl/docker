## Windows context
FROM debian:latest as deps

WORKDIR /install/window

RUN apt update -qq && apt install -y wget

# download archive
RUN wget https://libsdl.org/release/SDL2-devel-2.0.14-mingw.tar.gz && \
	wget https://www.libsdl.org/projects/SDL_image/release/SDL2_image-devel-2.0.5-mingw.tar.gz && \
	wget https://www.libsdl.org/projects/SDL_mixer/release/SDL2_mixer-devel-2.0.4-mingw.tar.gz && \
	wget https://www.libsdl.org/projects/SDL_net/release/SDL2_net-devel-2.0.1-mingw.tar.gz && \
	wget https://www.libsdl.org/projects/SDL_ttf/release/SDL2_ttf-devel-2.0.15-mingw.tar.gz

# extract archive
RUN tar xf SDL2-devel-2.0.14-mingw.tar.gz && \
	tar xf SDL2_image-devel-2.0.5-mingw.tar.gz && \
	tar xf SDL2_mixer-devel-2.0.4-mingw.tar.gz && \
	tar xf SDL2_net-devel-2.0.1-mingw.tar.gz && \
	tar xf SDL2_ttf-devel-2.0.15-mingw.tar.gz

# add sdl2 libraries
RUN cp -r SDL2-2.0.14/x86_64-w64-mingw32 /usr && \
	cp -r SDL2-2.0.14/i686-w64-mingw32 /usr && \
	cp -r SDL2_mixer-2.0.4/x86_64-w64-mingw32 /usr && \
	cp -r SDL2_mixer-2.0.4/i686-w64-mingw32 /usr && \
	cp -r SDL2_image-2.0.5/x86_64-w64-mingw32 /usr && \
	cp -r SDL2_image-2.0.5/i686-w64-mingw32 /usr && \
	cp -r SDL2_ttf-2.0.15/x86_64-w64-mingw32 /usr && \
	cp -r SDL2_ttf-2.0.15/i686-w64-mingw32 /usr && \
	cp -r SDL2_net-2.0.1/x86_64-w64-mingw32 /usr && \
	cp -r SDL2_net-2.0.1/i686-w64-mingw32 /usr

FROM debian:latest as artifact

COPY --from=deps /usr/x86_64-w64-mingw32 /usr/x86_64-w64-mingw32
COPY --from=deps /usr/i686-w64-mingw32 /usr/i686-w64-mingw32