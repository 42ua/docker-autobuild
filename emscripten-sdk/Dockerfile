FROM ubuntu

RUN \
	apt-get update && apt-get install -y build-essential \
	cmake python2.7 python nodejs-legacy default-jre git-core curl && \
	apt-get clean && \
\
	cd ~/ && \
	curl -sL https://s3.amazonaws.com/mozilla-games/emscripten/releases/emsdk-portable.tar.gz | tar xz && \
	cd emsdk_portable/ && \
	./emsdk update && \
	./emsdk install -j1 latest && \
	./emsdk activate latest && \
\
	rm -rf ~/emsdk_portable/clang/tag-*/src && \
	find . -name "*.o" -exec rm {} \; && \
	find . -name "*.a" -exec rm {} \; && \
	find . -name "*.tmp" -exec rm {} \; && \
	find . -type d -name ".git" -prune -exec rm -rf {} \; && \
\
	apt-get -y --purge remove curl git-core cmake && \
	apt-get -y autoremove && apt-get clean

# source emsdk_env.sh
# Adding directories to PATH:
# PATH += /root/emsdk_portable
# PATH += /root/emsdk_portable/clang/tag-e1.35.8/build_tag-e1.35.8_64/bin
# PATH += /root/emsdk_portable/emscripten/tag-1.35.8

# Dynamic variables not supported stackoverflow.com/q/27711304/ 

# Setting environment variables:
# EMSCRIPTEN = /root/emsdk_portable/emscripten/tag-1.35.8

# ENV PATH ~/emsdk_portable:$PATH
# ENV PATH $(ls -d ~/emsdk_portable/clang/tag-*/build_tag-*)/bin:$PATH
# ENV PATH $(dirname $(ls -d ~/emsdk_portable/emscripten/tag-*/emcc)):$PATH

# ENV EMSCRIPTEN $(dirname $(ls -d ~/emsdk_portable/emscripten/tag-*/emcc))

# http://docs.docker.com/engine/reference/run/#workdir
WORKDIR /home/src