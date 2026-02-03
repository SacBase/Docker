[![build status](https://github.com/SacBase/sac-jupyter-notebook/workflows/docker/badge.svg)](https://github.com/SacBase/sac-jupyter-notebook/actions?query=workflow%3A"docker")
[![docker pulls](https://img.shields.io/docker/pulls/sacbase/sac-jupyter-notebook)](https://hub.docker.com/r/sacbase/sac-jupyter-notebook)

# SaC Docker

This repository contains the base Dockerfiles used for compiling and running SaC programs.

Pre-built Docker images are available on [DockerHub](https://hub.docker.com/u/sacbase).

## Try out SaC interactively

For an interactive, no-install experience, you can try out one of our docker images available through [GitHub](https://github.com/SacBase/Docker) or directly on [DockerHub](https://hub.docker.com/u/sacbase).
Before you start, install [Docker](https://docs.docker.com/engine/install/) or [Docker desktop](https://docs.docker.com/desktop/setup/install/windows-install/) and make sure you can run the [hello world](https://hub.docker.com/_/hello-world/) example.

For first time users we recommend the interactive Jupyter Notebook environment.
In a terminal, run the following command start the SaC Jupyter container.
Multiple URLs will appear, open the one starting with `127.0.0.1`.

```bash
sudo docker run -p 8888:8888 sacbase/sac-jupyter-notebook
```

- `-p 8888:8888` maps port 8888 from the host to port 8888 on the container.

Most likely you will want to access an existing notebook on your system.
You can use a [bind mount](https://docs.docker.com/engine/storage/bind-mounts/) for this.
Open a terminal and change directory to where your existing notebook is.
Then, run the following command.

```bash
sudo docker run --rm -p 8888:8888 -v "$(pwd):/home/jovyan/work" sacbase/sac-jupyter-notebook
```

- `--rm` removes the container once it is done running.
- `-v` tells Docker to mount your current working directory to `/home/jovyan/work` inside the container.
  The Jupyter image's root directory is `/home/jovyan` and you can only access or save notebooks to that directory in the container.
