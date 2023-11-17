---
tags:
  - docker
---
## Storage driver
Writing into a container's writable layer requires a [storage driver](https://docs.docker.com/storage/storagedriver/) to manage the filesystem.
Docker has two options for containers to store files on the host machine, so that the files are persisted even after the container stops: volumes, and bind mounts.

> [!tip]+ Memory storage
> Docker also supports containers storing files in-memory on the host machine. Such files are not persisted. If you're running Docker on Linux, tmpfs mount is used to store files in the host's system memory. If you're running Docker on Windows, named pipe is used to store files in the host's system memory.

 - Volumes are stored in a part of the host filesystem which is _managed by Docker_ (`/var/lib/docker/volumes/` on Linux). Non-Docker processes should not modify this part of the filesystem. Volumes are the best way to persist data in Docker.
 - Bind mounts may be stored anywhere on the host system. They may even be important system files or directories. Non-Docker processes on the Docker host or a Docker container can modify them at any time.
 - `tmpfs` mounts are stored in the host system's memory only, and are never written to the host system's filesystem

## Volumes
- Created and managed by Docker. You can create a volume explicitly using the `docker volume create` command, or Docker can create a volume during container or service creation.
- Volumes also support the use of volume drivers, which allow you to store your data on remote hosts or cloud providers, among other possibilities.
## Bind Mounts
- Bind mounts have limited functionality compared to volumes. When you use a bind mount, a file or directory on the host machine is mounted into a container. The file or directory is referenced by its full path on the host machine.
Can be sepcified using -v or --mount
- `-v` or `--volume`: Consists of three fields, separated by colon characters (`:`). The fields must be in the correct order, and the meaning of each field is not immediately obvious.
    
    - In the case of bind mounts, the first field is the path to the file or directory on the **host machine**.
    - The second field is the path where the file or directory is mounted in the container.
    - The third field is optional, and is a comma-separated list of options, such as `ro`, `z`, and `Z`. These options are discussed below.

> [!warning]- Folder creation
> If you use -v or --volume to bind-mount a file or directory that does not yet exist on the Docker host, -v creates the endpoint for you. It is always created as a directory.
> 
> If you use --mount to bind-mount a file or directory that does not yet exist on the Docker host, Docker does not automatically create it for you, but generates an error.

## TMPFs Mounts
-  A `tmpfs` mount is not persisted on disk, either on the Docker host or within a container. It can be used by a container during the lifetime of the container, to store non-persistent state or sensitive information. <mark style="background: #FFDE0080;">For instance, internally, swarm services use `tmpfs` mounts to mount [secrets](https://docs.docker.com/engine/swarm/secrets/) into a service's containers.</mark>

> [!note]+ Mounting Volumes
> Bind mounts and volumes can both be mounted into containers using the -v or --volume flag, but the syntax for each is slightly different. For tmpfs mounts, you can use the --tmpfs flag. We recommend using the --mount flag for both containers and services, for bind mounts, volumes, or tmpfs mounts, as the syntax is more clear.

### NOTES 
- When you need to back up, restore, or migrate data from one Docker host to another, volumes are a better choice. You can stop containers using the volume, then back up the volume's directory (such as `/var/lib/docker/volumes/<volume-name>`).
- When the Docker host is not guaranteed to have a given directory or file structure. Volumes help you decouple the configuration of the Docker host from the container runtime.
- When you want to store your container's data on a remote host or a cloud provider, rather than locally.