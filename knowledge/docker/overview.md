# Docker

## What is a container?

- A container is an isolated process running on a host machine.
- It leverages kernel namespaces and cgroups in Linux to separate the container from the host machines OS. 
- It essentially a portable, runnable version of the a Docker image.

## What is an image?

- A running container uses an isolated filesystem provided by the image.
- Everything needed to run the container should be included in the image (e.g. dependencies, configurations, scripts, binaries, etc.).