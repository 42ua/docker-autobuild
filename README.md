# docker-emsdk-autobuild

### Build:
    ~$ sudo docker build -no-cache -t 42ua/emsdk -f emscripten-sdk/Dockerfile .
    ~$ docker push 42ua/emsdk
    #sudo docker run -i -t --rm 42ua/emsdk /bin/bash
    #sudo docker ps -aq | sudo xargs docker stop
    #sudo docker ps -aq | sudo xargs docker rm
    #sudo docker rmi 42ua/emsdk

## Usage:
    ~$ docker pull 42ua/emsdk

### Sample:

*hello_world.c*
```
#include<stdio.h>

int main() {
    printf("hello, world!\n");
    return 0;
}
```

### Compile Sample:

```
~$ docker run --rm -v $(pwd):/home/src 42ua/emsdk emcc hello_world.c
```

### Run Sample:

```
~$ node a.out.js
```

### Makefiles:

```
~$ docker run --rm -v $(pwd):/home/src 42ua/emsdk emconfigure ./configure
~$ docker run --rm -v $(pwd):/home/src 42ua/emsdk emmake make
```