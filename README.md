## Dockerfile setup for using mozilla Deepspeech

Commands to run

1. Build docker image

```
$ cd  docker
$ docker build -t deepspeech_docker .
$ cd ..
```

2. Download deepspeech model to the data directory
```
$ cd data
$ wget https://github.com/mozilla/DeepSpeech/releases/download/v0.4.1/deepspeech-0.4.1-models.tar.gz 
$ tar xzf deepspeech-0.4.1-models.tar.gz
$ cd ..
```

3. If you would like include any audio samples, copy them to data directory


4. Start docker container. Map ./data folder as $HOME/deepspeech in container
```
$ docker run -it -v $(pwd)/data:/home/mapr/deepspeech --name deepspeech_container  deepspeech_docker 
```
It will open a bash shell in the container.

6. To run deepspeech within the container, the commands are
```
$ cd deepspeech
$ ./infer.sh ./surely_a.wav
```

7. To attach a new shell to the container
```
$ docker exec -it deepspeech_container /bin/bash
```






