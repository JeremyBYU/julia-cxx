# julia-cxx

Docker files for Cxx.jl pre-installed Julia language environments

- **latest**: Cxx.jl pre-installed ubuntu 16.04
- **ubuntu14.04**: Cxx.jl pre-installed ubuntu 14.04. Uses Julia Stable 0.5.2 with r9y9/Cxx.jl fork.
- **pcl**: PCL.jl pre-instaleld Ubuntu 14.04.
- **pcl-nv**: PCL.jl with Nvidia Driver bindings to be used with `nvidia-docker`.  Allows use of graphics and CUDA libraries.

## Running Instructions

1. To run a Julia environment with Cxx installed
    1. `docker run -it --rm jeremybyu/julia-cxx:ubuntu14.04`
2. To run a Julia environment with PCL and Cxx installed
    1. `docker run -it --rm jeremybyu/julia-cxx:pcl`
3. To run a Julia Environment with Nvidia Docker 
    1. Ensure you have installed Nvidia Docker. Follow these [instructions](https://github.com/NVIDIA/nvidia-docker/wiki/Installation).
    2. 
    ```
    nvidia-docker run -it \
        --name=julia-nv \
        --env="DISPLAY" \
        --env="QT_X11_NO_MITSHM=1" \
        --workdir="/home/$USER" \
        --volume="/home/$USER:/home/$USER" \
        --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
        jeremybyu/julia-cxx:pcl-nv && \
    export containerId=$(docker ps -l -q)
    ```
    3. Temporarily detatch from the docker terminal by typing ctrl-p-q
    4. Paste the following to give access X-server access rights to your docker container. 
    ```
    xhost +local:`docker inspect --format='{{ .Config.Hostname }}' $containerId`
    ```


