# docker-autobuild

### Build:
    ~$ sudo docker build -no-cache -t mazko/emsdk -f emscripten-sdk/Dockerfile .
    #sudo docker run -i -t --rm mazko/emsdk /bin/bash
    #sudo docker ps -aq | sudo xargs docker stop
    #sudo docker ps -aq | sudo xargs docker rm
    #sudo docker rmi mazko/emsdk

### Usage:
    ~$ docker run --rm -v $(pwd):/home/src mazko/emsdk emcc hello_world.c
    ~$ docker run --rm -v $(pwd):/src mazko/emsdk emconfigure ./configure
    ~$ docker run --rm -v $(pwd):/src mazko/emsdk emmake make
