# docker-emsdk-autobuild

### Install:
    ~$ docker pull 42ua/emsdk

### Sample:

*hello_world.c*
```
#include <stdio.h>

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

### Useful Env(BASH):

    for alias in 'emcc' 'emconfigure' 'emmake'; do
      alias $alias="docker run -i -t --rm -v \$(pwd):/home/src 42ua/emsdk $alias"
    done
    unset alias

    PS1="(emsdk)$PS1"

Env usage: ```emcc -v```

### Optional increase memory before build docker image:
```
    ~$ free
                 total       used       free     shared    buffers     cached
    Память:    3937028    2191548    1745480     235688      71004     897288
    -/+ буферы/кэш:    1223256    2713772
    Подкачка:    1998844          0    1998844
```

```
    # https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-ubuntu-14-04
    ~$ sudo fallocate -l 8G /media/DATA/swapfile-$$
    ~$ sudo chmod 600 /media/DATA/swapfile-$$
    ~$ sudo mkswap /media/DATA/swapfile-$$
    ~$ sudo swapon /media/DATA/swapfile-$$
    # cat /proc/sys/vm/vfs_cache_pressure
    # cat /proc/sys/vm/swappiness
    ~$ sudo sysctl vm.swappiness=10 && sudo sysctl vm.vfs_cache_pressure=50
```

```
    ~$ free
                 total       used       free     shared    buffers     cached
    Память:    3937028    2196772    1740256     179024      72788     864476
    -/+ буферы/кэш:    1259508    2677520
    Подкачка:   10387448          0   10387448
```

### Build docker image:
    ~$ git clone https://github.com/42ua/docker-autobuild.git && cd docker-autobuild
    ~$ docker build --no-cache -t emsdk -f emscripten-sdk/Dockerfile .
    ~$ CLEAN_PATH=`docker run --rm emsdk bash -c 'echo $PATH'`
    ~$ EMSDK_PATH=`docker run --rm emsdk bash -c \
        '. ~/emsdk-portable/emsdk_env.sh > /dev/null ; echo $PATH'`
    ~$ EMSDK_EMSCRIPTEN=`docker run --rm emsdk bash -c \
        '. ~/emsdk-portable/emsdk_env.sh > /dev/null ; echo $EMSCRIPTEN'`
    ~$ EM_CONFIG=`docker run --rm emsdk bash -c \
        '. ~/emsdk-portable/emsdk_env.sh > /dev/null ; echo $EM_CONFIG'`
    ~$ EMSDK_PATH=${EMSDK_PATH%":$CLEAN_PATH"} # suffix
    ~$ EMSDK_PATH=${EMSDK_PATH#"$CLEAN_PATH:"} # prefix
    ~$ {
         echo "FROM emsdk"
         echo "ENV PATH ${EMSDK_PATH}:\$PATH"
         echo "ENV EM_CONFIG ${EM_CONFIG}"
         echo "ENV EMSCRIPTEN ${EMSDK_EMSCRIPTEN}"
       } | docker build --no-cache -t 42ua/emsdk -
    ~$ docker run -it --rm 42ua/emsdk emcc -v
    # 1.36.0
    ~$ docker rmi emsdk
    ~$ docker push 42ua/emsdk
    # docker ps -aq | xargs docker stop
    # docker ps -aq | xargs docker rm
    # docker rmi 42ua/emsdk
    # docker images -qa | xargs docker rmi