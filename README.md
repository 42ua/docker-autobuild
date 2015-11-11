# docker-autobuild

### Build:
    ~$ sudo docker build -no-cache -t 42ua/emsdk -f emscripten-sdk/Dockerfile .
    #sudo docker run -i -t --rm 42ua/emsdk /bin/bash
    #sudo docker ps -aq | sudo xargs docker stop
    #sudo docker ps -aq | sudo xargs docker rm
    #sudo docker rmi 42ua/emsdk

### Usage:

*hello_world.c*
```
#include<stdio.h>

int main() {
    printf("hello, world!\n");
    return 0;
}
```

    ~$ docker run --rm -v $(pwd):/home/src 42ua/emsdk emcc hello_world.c
    ~$ docker run --rm -v $(pwd):/home/src 42ua/emsdk emconfigure ./configure
    ~$ docker run --rm -v $(pwd):/home/src 42ua/emsdk emmake make