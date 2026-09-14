# SaC Compiler

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

## Updating the image

To update the Docker image to the latest version, run:

```bash
sudo docker pull sacbase/sac-compiler:latest
```

We generate a fresh image every week.
To pull or run a specific image, use `sacbase/sac-compiler:yyyy-ww` instead, where `yyyy` is the year and `ww` is the week number.
A list of available versions is available on [Docker Hub](https://hub.docker.com/r/sacbase/sac-compiler).
