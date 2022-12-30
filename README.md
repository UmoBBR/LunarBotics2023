# LunarBotics2023
Repository to store all code for LunarBotics20203 competition

# ROS Dockerfile
[docker run documentation](https://docs.docker.com/language/nodejs/run-containers/)

I (Nathan), am aware that running containers with `--privileged` is insecure. I'll make a tutorial on how to find a device and pass it through to the container later.

clone this repo

    git clone https://github.com/UmoBBR/LunarBotics2023.git

Move into the directory and build the dockerfile

    cd LunarBotics2023/ROSdockerfile/ 
    docker build -t umaineros2 .

Run the container detached

    docker run -itd --privileged --name umorosworkspace umaineros2 /bin/bash 

Check if the container is up with `docker ps -a`

You can connect to the container's shell at any time via 

    docker exec -it umorosworkspace bash

detach from the shell with they key combo `CTRL+A+D`

## Directory Structure

    /opt
        poetry/
        venv/
        ros/
            foxy/
        ros2_ws/
            code/
            Lepton/