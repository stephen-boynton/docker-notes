# Docker

Originally there was a server. There was a difficulty in running multiple
software at the same times.

Then came virtualization. Now you could create virtual environments and evenly
spread resources across software. If one app went down, the others would be
okay. Problem? It was very time consuming.

Finally, Docker came out! It takes care of all of the above problems. You have
Containers that are essentially virtual machines.

## Docker Hub/Store

Think of this as the App Store. Some of it is free and some of it is paid for.

Docker Hub is open source for anyone. Docker Store is for enterprise setups.

## Basic Docker Commands

* `docker search [item]` - Search the Hub for repos.
* `docker pull [item]` - Download any repo by name.
  * you can also use `docker pull [item]:[version]`
* `docker images` - will list all images available on your machine.
* `docker rmi [image]` - removes the image from your machine

## More Docker Commands

An image is your code, a running instances of that image is known as a
container!.

* `docker run -d -p [port] [image]` - This will be different depending on the
  image that you're running. Any port that you map to this will be available to
  the browser.
  * `-d` - run in the background as daemon
  * `-p 8080:80` - map to port 8080
  * If you use this command without the image being installed, Docker will
    automatically download the image needed to run your command.

- `docker ps` - This shows you all containers that are running and the
  associated information.
  * `-a` - shows all run commands, successful or not

* `docker exec -ti [image] [location]` - this command is used to login to a
  **running** container.

  * `-ti` - terminal interactive
  * `location` - used above in the example was `/bin/bash`

* `docker rm` - remove a docker container
* `docker kill` - force stop a container, this **cannot** be started again
  later, chances for corruption are greater with this command
* `docker start` - start a container
* `docker stop` - gracefully stop a container, this can be started again later

You can also nest docker commands like this `docker rm $(docker ps -aq)`.

## Advanced Run Command

New flags!

* `--link` - Use this to connect containers
  * `docker run --name wordpress --link mysql:mysql -p 8080:80 -d wordpress`
* `-e` - is the environment variable aka `process.env` info.
  * `docker run --name mysql -e MYSQL_ROOT_PASSWORD=password -d mysql`
  * You can also chain `-e` flags if you have multiple env variables!

## Docker Volumes and Persistence

* `-v` and `--volumes from` are the commands.
* `docker run --name datastore -v /datatutorial -d busybox sleep 5000` - creates
  empty folder `datatutorial`;
* `docker run --name datastore2 -v /root:/datatutorial -d busybox sleep 5000` -
  takes all of the data from `root` and puts it into `datatutorial`
  * The files created in this `-v` are also created on the local machine.
  * Multiple containers can share the same folder
  * you can also add `:ro` after the `datatutorial` folder to make it only have
    read-only permissions
