# docker-openpose-realsense
Dockerfile to build a containerized working openpose repository
## Description
Dockerfile for https://hub.docker.com/r/brwrld/openpose.
It makes it easy to run openpose in docker. With intel realsense driver support, even though you can only use the video streams as of now. The image is based on debian.
## Instructions
To run the image, save the following code to a .sh file, e.g. [ready shell script] (https://github.com/j3cc/docker-openpose-realsense/blob/master/start_openpose_docker):

```
XSOCK=/tmp/.X11-unix
XAUTH=/tmp/.docker.xauth
touch $XAUTH
xauth nlist $DISPLAY | sed -e 's/^..../ffff/' | xauth -f $XAUTH nmerge -

docker run -it \
	--volume=$XSOCK:$XSOCK:rw \
        --volume=$XAUTH:$XAUTH:rw \
        -v /media/br/WCDB/data/wc/vv_openpose/:/openpose/data/ \
        --device /dev/video0 \
        --env="XAUTHORITY=${XAUTH}" \
        --env="DISPLAY" \
        --user="openpose" \
        -p 9000:9000 -it --rm --runtime=nvidia -e NVIDIA_VISIBLE_DEVICES=0 \
        brwrld/openpose:latest /bin/bash 

 ```
Replace --device /dev/video0 with the device you want to be able to see in the container. In the container, start the demo with `sudo ./build/examples/openpose/openpose.bin` 
