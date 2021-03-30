# Simple Terraria server container

This project is a Dockerfile to containerize [TShock](https://github.com/Pryaxis/TShock) and [Terraria](https://terraria.org/) TerrariaServer.exe to run on linux.

## Quick start

First you need a linux machine with [Docker](https://www.docker.com/) installed. 

### Create directory to save your files

Next create a directory for your world file, configuration and logs.

```bash
mkdir ~/data
```

### Run the imagen

Start the container, set the port and the location of the configuration files.

```bash
docker run -it --rm \
-p 7777:7777 \ 
-v ~/data:/root \
jidef/terraria
```

**Note:** If you close the the terminal, the server will stop running.

### To start with a preexisting world

Just move all your stuff to the directory you created before starting the container.


## Building from source

Assuming [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [docker](https://www.docker.com/) are installed..

1. Clone this repository

    ```bash
    git clone https://github.com/jidef/terraria.git
    ```

2. Open a terminal window into the directory downloaded by the git
3. Build the container

    ```bash
    docker build -t <name_here> .
    ```

## Plugin support

A volume exists to support plugins.  Create a folder, not inside your `/data` folder, for your plugins

```bash
mkdir ServerPlugins
```

Mount the plugins directory with an additional -v switch on your `docker run ...` command

```bash
-v <path_to_your_ServerPlugins_folder>:/tshock/ServerPlugins/
```