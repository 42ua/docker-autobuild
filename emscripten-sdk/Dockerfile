FROM ubuntu:14.04
MAINTAINER mazko (http://mazko.github.io/)

WORKDIR ~/

RUN apt-get update && apt-get install -y build-essential \
	cmake python2.7 nodejs-legacy default-jre git-core wget && \
	apt-get clean && \
	wget https://s3.amazonaws.com/mozilla-games/emscripten/releases/emsdk-portable.tar.gz && \
	tar -xvf emsdk-portable.tar.gz && cd emsdk_portable/ && \
	./emsdk update && \
	./emsdk install latest && \
	./emsdk activate latest && \
	find emsdk_portable -name "*.o" -exec rm {} \; && \
	find emsdk_portable -name "*.a" -exec rm {} \; && \
	rm -rf emsdk_portable/emscripten/master/.git && \
	apt-get -y --purge remove wget git-core cmake && \
	apt-get -y autoremove && apt-get clean

ENTRYPOINT source ~/emsdk_portable/emsdk_env.sh ; emcc -v

WORKDIR /home/src