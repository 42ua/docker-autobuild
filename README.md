# docker-emsdk-autobuild

### Usage:
    ~$ sudo docker pull 42ua/emsdk

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
~$ sudo docker run --rm -v $(pwd):/home/src 42ua/emsdk emcc hello_world.c
```

### Run Sample:

```
~$ node a.out.js
```

### Makefiles:

```
~$ sudo docker run --rm -v $(pwd):/home/src 42ua/emsdk emconfigure ./configure
~$ sudo docker run --rm -v $(pwd):/home/src 42ua/emsdk emmake make
```

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

### Build:
    ~$ sudo docker build --no-cache -t 42ua/emsdk -f emscripten-sdk/Dockerfile .
    ~$ sudo docker push 42ua/emsdk
    # sudo docker run -i -t --rm 42ua/emsdk /bin/bash
    # sudo docker ps -aq | sudo xargs docker stop
    # sudo docker ps -aq | sudo xargs docker rm
    # sudo docker rmi 42ua/emsdk