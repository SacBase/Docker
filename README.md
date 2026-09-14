[![build status](https://github.com/SacBase/sac-jupyter-notebook/workflows/docker/badge.svg)](https://github.com/SacBase/sac-jupyter-notebook/actions?query=workflow%3A"docker")
[![docker pulls](https://img.shields.io/docker/pulls/sacbase/sac-jupyter-notebook)](https://hub.docker.com/r/sacbase/sac-jupyter-notebook)

SaC Docker
==========

This repository contains the base Dockerfiles used for compiling and running SaC programs.

Pre-built Docker images are available on [DockerHub](https://hub.docker.com/u/sacbase).

SaC Compiler
============

This Docker image provides everything needed to compile and run Single Assignment C (SaC) programs.
You do not need to install SaC on your computer.

> We recommend using Docker from a terminal rather than using the Docker Desktop graphical interface. The commands below are all you need.

## 1. Start the SaC environment

From inside the folder where your SaC files are located, run:

```bash
docker run -it --rm \
  -v "$PWD:/home" \
  sacbase/sac-compiler:latest
```

You are now inside the SaC environment.
Your current directory on your computer (`PWD`) is now available under `/home`.

> **Important:** Run all SaC programs from inside this Docker environment. The compiled programs need the SaC runtime libraries, which are installed in the container.

### What does the Docker command do?

* `-it` gives you an interactive terminal inside the container.
* `--rm` automatically removes the container when you exit. Files in the mounted directory are not removed.
* `-v "$PWD:/home"` mounts your current directory as `/home` inside the container. Files you create there are therefore stored on your computer.
* `sacbase/sac-compiler:latest` specifies the Docker image to use.

### Optional: Create an alias

You can create an alias so you don't have to type the full Docker command every time:

```bash
alias saccompiler='docker run -it --rm -v "$PWD:/home" sacbase/sac-compiler:latest'
```

You can then start the SaC environment with:

```bash
saccompiler
```

The alias only lasts for the current terminal session.
To make it permanent, add the `alias` command to your shell's configuration file, such as `~/.bashrc` or `~/.zshrc`.

## 2. Compile and run

Inside the container:

```bash
sac2c program.sac
./a.out
```

The source files and generated files are stored in your normal directory on your computer because it is mounted as `/home`.

## 3. Finish

When you are done:

```bash
exit
```

The Docker container is automatically removed.
Files in the mounted directory are not deleted.

SaC Jupyter Notebook
====================

This Docker image provides a ready-to-use Jupyter Notebook environment for SaC.
You do not need to install SaC or Jupyter on your computer.

> We recommend using Docker from a terminal rather than using the Docker Desktop graphical interface. The commands below are all you need.

## 1. Start the Jupyter environment

From inside the folder where you want to store your notebooks, run:

```bash
docker run --rm -p 8888:8888 \
  -v "$PWD:/home/jovyan/work" \
  sacbase/sac-jupyter-notebook:latest
```

Jupyter will start and print in the console a URL containing a login token, for example:

```text
http://127.0.0.1:8888/tree?token=...
```

Open that URL in your web browser.

### What does the Docker command do?

* `--rm` automatically removes the container when you exit. Files in the mounted directory are not removed.
* `-p 8888:8888` makes Jupyter's port 8888 available on your computer.
* `-v "$PWD:/home/jovyan/work"` mounts your current directory as the `work` directory inside the container. Files you create there are therefore stored on your computer.
* `sacbase/sac-jupyter-notebook:latest` specifies the Docker image to use.

### Optional: Create an alias

You can create an alias so you don't have to type the full Docker command every time:

```bash
alias sacjupyter='docker run --rm -p 8888:8888 -v "$PWD:/home/jovyan/work" sacbase/sac-jupyter-notebook:latest'
```

You can then start Jupyter with:

```bash
sacjupyter
```

The alias only lasts for the current terminal session.
To make it permanent, add the `alias` command to your shell's configuration file, such as `~/.bashrc` or `~/.zshrc`.

## 2. Create a SaC notebook

In Jupyter, open the `work` directory.

Create a new notebook and select the SaC kernel.
You can now write and execute SaC code directly in the notebook.

## 3. Finish

When you are done, return to the terminal running Jupyter and press:

```text
Ctrl+C
```

The Docker container is automatically removed.
Your notebooks and other files in the mounted directory are not deleted.

To start Jupyter again, run the command from step 1.

## Updating the image

We generate a fresh image every week for both environments.
To update the Docker image to the latest version, run:

```bash
docker pull sacbase/sac-compiler:latest
```

To pull or run a specific image, use `sacbase/sac-compiler:yyyy-ww` instead, where `yyyy` is the year, and `ww` is the week number.
A list of available versions is available on [Docker Hub](https://hub.docker.com/u/sacbase).
