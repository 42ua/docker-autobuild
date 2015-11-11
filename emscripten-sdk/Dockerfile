FROM ubuntu

RUN \
	apt-get update && apt-get install -y build-essential \
	cmake python2.7 nodejs-legacy default-jre git-core curl && \
	apt-get clean 

RUN \
	cd ~/ && \
	curl -sL https://s3.amazonaws.com/mozilla-games/emscripten/releases/emsdk-portable.tar.gz | tar xz && \
	cd emsdk_portable/ && \
	./emsdk update && \
	./emsdk install -j1 latest && \
	./emsdk activate latest && \
	find . -name "*.o" -exec rm {} \; && \
	find . -name "*.a" -exec rm {} \; && \
	find . -name "*.tmp" -exec rm {} \; && \
	find . -type d -name ".git" -exec rm -rf {} \;

RUN \
	apt-get -y --purge remove curl git-core cmake && \
	apt-get -y autoremove && apt-get clean

ENV PATH ~/emsdk_portable:$PATH
ENV PATH `ls -d ~/emsdk_portable/clang/fastcomp/build_master_*/bin`:$PATH
ENV PATH ~/emsdk_portable/emscripten/master:$PATH

# http://docs.docker.com/engine/reference/run/#workdir
WORKDIR /home/src