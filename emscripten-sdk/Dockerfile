FROM ubuntu

RUN \
	apt-get update && apt-get install -y build-essential \
	cmake python2.7 python nodejs-legacy default-jre git-core curl && \
	apt-get clean && \
\
	cd ~/ && \
	curl -sL https://s3.amazonaws.com/mozilla-games/emscripten/releases/emsdk-portable.tar.gz | tar xz && \
	cd emsdk-portable/ && \
	./emsdk update && \
	./emsdk install -j1 latest && \
	./emsdk activate latest && \
\
	rm -rf ~/emsdk-portable/clang/tag-*/src && \
	find . -name "*.o" -exec rm {} \; && \
	find . -name "*.a" -exec rm {} \; && \
	find . -name "*.tmp" -exec rm {} \; && \
	find . -type d -name ".git" -prune -exec rm -rf {} \; && \
\
	apt-get -y --purge remove curl git-core cmake && \
	apt-get -y autoremove && apt-get clean

# http://docs.docker.com/engine/reference/run/#workdir
WORKDIR /home/src