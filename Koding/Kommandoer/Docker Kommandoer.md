## Docker service

```
/etc/rc.d/rc.docker <command>
```
**Available commands:** ==start== ==stop== ==restart== ==status==

## Generelle kommandoer
```
docker <command> <containername>
```
**Available commands:** ==start== ==stop== ==restart== ==pause== ==logs==

## Print all container names:
```
docker ps --format ‘{{.Names}}’
```
```bash
docker ps                         # see a list of running containers
docker ps -a                      # see a list of running and stopped containers
```
## Print all container images:
```
docker ps --format ‘{{.Image}}’
```

## Exec
[How To Use docker exec to Run Commands in a Docker Container](https://www.digitalocean.com/community/tutorials/how-to-use-docker-exec-to-run-commands-in-a-docker-container)
[Mer informasjon](https://stackoverflow.com/questions/30172605/how-do-i-get-into-a-docker-containers-shell)

[Google Disk: Innlogging](https://drive.google.com/drive/quota)

```
docker exec -it container-name sh
docker exec -ti borgmatic sh
exit
```

```
docker exec -it <id or name> <command>          # attach to a container with a command
docker exec -it immich_server sh
docker exec -it immich_microservices sh
docker exec -it immich_machine_learning sh
```
https://github.com/bigbeartechworld/big-bear-scripts/blob/master/docker-exec-helper/run.sh
> The `-i` flag keeps input open to the container, and the `-t` flag creates a pseudo-terminal that the shell can attach to. These flags can be combined like this:

[Forskjell mellom attach og exec](https://iximiuz.com/en/posts/containers-101-attach-vs-exec/)
## Attach to a Container
[Attach to docker terminal](https://docs.docker.com/engine/reference/commandline/container_attach)
``` 
docker attach container-name
```
> As the container was started without the `-i`, and `-t` options, signals are forwarded to the attached process, which means that the default `CTRL-p CTRL-q` detach key sequence produces no effect, but pressing `CTRL-c` terminates the container:



## Logs

```bash
docker logs <id or name>          # see the logs for a specific container (by id or name)

docker logs immich_server
docker logs immich_microservices
docker logs immich_machine_learning
cd /mnt/user/appdata/docker_compose_projects/Immich;docker compose logs -f -n 10
```

>tip Follow a log
Adding `--follow` to a `docker logs <id or name>` command will stream new logs, instead of immediately exiting, which is often useful for debugging.

## Volum
[Docker: where is docker volume located for this compose file - Stack Overflow](https://stackoverflow.com/questions/45271420/docker-where-is-docker-volume-located-for-this-compose-file)

# Unraid-spesefikke
## Logging og restart
Legg til dette i parametre i Unraid-template
```
 --log-driver=gelf --log-opt gelf-address=udp://192.168.0.10:12201 --restart unless-stopped
```

## Ikoner
Filepath: 
```
/mnt/user/system/icons/unRAID-Docker-Folder-Animated-Icons---Alternate-Colors-master/Pale-Collection/
```
Hentet fra denne [repoen](https://github.com/hernandito/unRAID-Docker-Folder-Animated-Icons---Alternate-Colors/tree/master)
[Forumpost](https://forums.unraid.net/topic/92824-icon-collections-for-docker-folder-plugin/)

Bruker CSS fra [GitHub - Tyree/folder.view.custom.css: Customized CSS for the Folder.View plugin by scolcipitato.](https://github.com/Tyree/folder.view.custom.css)


## Signal-cli-REST-api
![[Docker Kommandoer-1.png]]


# Arkitektur
>[!info]- Bilde
>  ![[Docker Kommandoer-2.png]]

[Youtube: 100+ Docker Concepts you Need to Know](https://www.youtube.com/watch?v=rIrNIzy6U_g)

# Troubleshooting
## 2.1. Could not connect to docker
[2. Issues — An Easy Guide to self-host Overleaf Community Edition](https://shihabkhan1.github.io/overleaf/issues.html)
> ERROR: Couldn’t connect to Docker daemon at http+docker://localhost - is it running? If it’s at a non-standard location, specify the URL with the DOCKER_HOST environment variable.

**Solution:**
Give user permissions to docker
```SH
sudo usermod -a -G docker $USER
```
