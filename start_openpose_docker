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
