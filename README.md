# docker-autobuild

###Build:
	sudo docker build -no-cache -t emscripten -f emscripten-sdk/Dockerfile .
	#sudo docker run -i -t --rm emscripten /bin/bash
	#sudo docker ps -aq | sudo xargs docker stop
	#sudo docker ps -aq | sudo xargs docker rm
	#sudo docker rmi emscripten

###Usage:
    ~$ docker run --rm -v $(pwd):/home/src -t mazko/emscripten-sdk emcc hello_world.c
