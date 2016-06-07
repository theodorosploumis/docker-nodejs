![Docker logo](https://raw.githubusercontent.com/theodorosploumis/docker-nodejs/gh-pages/img/docker_logo.png)

## Docker for NodeJS

#### [NodeJS Meetup Thessaloniki](http://www.meetup.com/Thessaloniki-Node-js-Meetup/events/231574221/), June 2016

_________________

###### [TheodorosPloumis.com](http://www.theodorosploumis.com/en) / [@theoploumis](twitter.com/theoploumis)

###### Get them: [online presentation](http://theodorosploumis.github.io/docker-nodejs/) / [source code](https://github.com/theodorosploumis/docker-nodejs) / [docker image](https://hub.docker.com/r/tplcom/docker-nodejs/) / [video](https://www.youtube.com/watch?v=ALEE6oTUQOE)

###### Share under [CC BY 4.0](http://creativecommons.org/licenses/by/4.0/)

---

### Let me ask you

- Who knows about [Docker](http://docker.com)?
- Who uses Docker for development?
- Who uses Docker in production?
- Who tried but could not do it?

---

### What is Docker (v1.11)

> Docker is an open platform for developing, shipping, and running applications.

###### See more on the [Docker introduction slides](http://theodorosploumis.github.io/docker-presentation/)

---

### Docker vs VMs

![Docker vs traditional Virtualization](https://insights.sei.cmu.edu/assets/content/VM-Diagram.png)

---

### Docker Benefits

- Fast (deployment, migration, restarts)
- Secure
- Lightweight (save disk & CPU)
- Open Source
- Portability
- Microservices and integrations (APIs)
- Simplify DevOps
- Version control capabilities
- Docker: 1-process-per-container && NodeJS: single-process

---

### Technology behind Docker

- Linux [x86-64](https://www.wikiwand.com/en/X86-64)
- [Go](https://golang.org/) language
- [Client- Server](https://www.wikiwand.com/en/Client%E2%80%93server_model) (deamon) architecture
- Union file systems ([UnionFS](https://www.wikiwand.com/en/UnionFS): AUFS, btrfs, vfs etc)
- [Namespaces](https://en.wikipedia.org/wiki/Cgroups#NAMESPACE-ISOLATION) (pid, net, ipc, mnt, uts)
- Control Groups ([cgroups](https://www.wikiwand.com/en/Cgroups))
- Container format ([libcontainer](https://github.com/opencontainers/runc/tree/master/libcontainer "Libcontainer provides a native Go implementation for creating containers with namespaces, cgroups, capabilities, and filesystem access controls. It allows you to manage the lifecycle of the container performing additional operations after the container is created."))

###### See more at [Understanding docker](https://docs.docker.com/engine/understanding-docker/)

---

### Steps of a Docker workflow

```
docker run -i -t ubuntu /bin/bash
```

- Pulls the ubuntu [image](https://docs.docker.com/engine/userguide/containers/dockerimages/ "A read-only layer that is the base of your container. It can have a parent image to abstract away the more basic filesystem snapshot.") from the [registry](https://docs.docker.com/registry/ "The central place where all publicly published images live. You can search it, upload your images there and when you pull a docker image, it comes the repository/hub.")
- Creates a new [CONTAINER_ID](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/ "A runnable instance of the image, basically it is a process isolated by docker that runs on top of the filesystem that an image provides.")
- Allocates a filesystem and mounts a read-write [layer](https://docs.docker.com/engine/reference/glossary/#filesystem "A set of read-only files to provision the system. Think of a layer as a read only snapshot of the filesystem.")
- Allocates a [network/bridge interface](https://www.wikiwand.com/en/Bridging_%28networking%29 "")
- Sets up an [IP address](https://www.wikiwand.com/en/IP_address "An Internet Protocol address (IP address) is a numerical label assigned to each device (e.g., computer, printer) participating in a computer network that uses the Internet Protocol for communication.")
- Executes a process that you specify (``` /bin/bash ```)
- Captures and provides application output

---

### The Docker terminology

- docker engine
- docker client
- docker machine
- docker image
- docker container
- docker-compose
- docker swarm
- docker distribution

---

### Agenda

- Public Dockerfiles
- The docker hub
- Try NodeJS* apps
- Explore docker cli
- Dockerizing NodeJS
- Using Docker with NodeJS

---

### Public Dockerfiles

Popular Dockerfiles from [hub.docker.com](https://hub.docker.com)

- A list of [NodeJS](https://hub.docker.com/search/?page=1&q=nodejs&starCount=0) public images
- [node/0.10.45](https://github.com/nodejs/docker-node/blob/5e058d36cc69303d1f62d424615fa03e050f20ef/0.10/Dockerfile)
- [node/slim](https://hub.docker.com/r/library/node/tags/slim/)
- [jprjr/tinynode](https://hub.docker.com/r/jprjr/tinynode/)
- [shawnzhu/ruby-nodejs](https://hub.docker.com/r/shawnzhu/ruby-nodejs/)
- [scratch](https://hub.docker.com/_/scratch/)
- [nodesource explicit images](https://github.com/nodesource/docker-node#usage)

Documented [Dockerfile reference](https://github.com/theodorosploumis/docker-presentation/blob/gh-pages/examples/dockerfile/Dockerfile).

###### Topics: basics, images, Dockerfile, hub

---

### The docker hub

- [hub.docker.com](https://hub.docker.com/)
- [REST API v1](https://docs.docker.com/v1.6/reference/api/docker-io_api/)
- [REST API v2](https://docs.docker.com/registry/spec/api/)
- [page of readytalk/nodejs](https://hub.docker.com/r/readytalk/nodejs/)
- [images of readytalk/nodejs, v1](https://registry.hub.docker.com/v1/repositories/readytalk/nodejs/images)
- [info about tplcom namespace. v2](https://registry.hub.docker.com/v2/repositories/tplcom/docker-nodejs/)

###### Topics: hub, registry, public images

---

### Try NodeJS* apps and software

```
// Try mean.io stack. Open localhost:8010
docker pull gbevan/meanio
docker run -d -p 8010:3000 --name meanio gbevan/meanio

// Try Nagios. Open localhost:8120/nagios (user: nagiosadmin pass: admin)
docker pull quantumobject/docker-nagios
docker run -d -p 8125:25 -p 8120:80 --name nagios quantumobject/docker-nagios

// Try Wekan. Open localhost:8040
docker pull mongo
docker pull mquandalle/wekan
docker run -d --name wekan-db mongo
docker run -d --link "wekan-db:db" \
           -e "MONGO_URL=mongodb://db" -p 8040:80 mquandalle/wekan

```
###### Topics: run, link, ports, containers

---

### Explore docker cli commands

```
// General info
man docker // man docker-run
docker help // docker help run
docker info
docker version
docker network ls

// Images
docker images // docker [IMAGE_NAME]
docker pull [IMAGE] // docker push [IMAGE]

// Containers
docker run ...
docker exec ...
docker ps // docker ps -a, docker ps -l
docker stop/start/restart [CONTAINER_ID]
docker stats [CONTAINER_ID]
docker top [CONTAINER_ID]
docker port [CONTAINER_ID]
docker inspect [CONTAINER_ID]
docker inspect -f "{{ .State.StartedAt }}" [CONTAINER_ID]
docker rm [CONTAINER_ID]

```

###### Topics: dry, wharfee, docker simple ui, cli

---

### Dockerizing NodeJS

```
FROM nodesource/jessie:0.12.13

# Set the NodeJS environment to dev (vs production)
ENV NODE_ENV dev

# cache package.json and node_modules to speed up builds
ADD package.json /package.json
RUN npm install

# Add your local files to the image
ADD . /path/to/app

# Setup the workdir
WORKDIR /path/to/app

# Optional volume the app
VOLUME /path/to/app

# Expose ports
EXPOSE 3000

CMD ["npm","start"]
```

Other basic examples: [1](https://docs.docker.com/engine/examples/nodejs_web_app/).

###### Topics: npm, cache layers

---

### Using Docker with NodeJS

A simple [NodeJS app with redis](https://github.com/thess-docker/docker-scale-node/).

```
git clone git@github.com:thess-docker/docker-scale-node.git
cd docker-scale-node

docker-compose up -d
...

docker-compose run web env
docker-compose logs
docker-compose stop
docker-compose restart
docker-compose down
docker-compose up redis

```

Other useful examples [1](https://github.com/docker/example-voting-app), [2](https://github.com/thess-docker/docker-compose-nodejs), [3](https://github.com/thess-docker/nodejs-loadbalanced-dockercompose), [4](https://github.com/thess-docker/docker-nodejs-postgres)

###### Topics: docker-compose, ci, testing

---

### Docker tips

There are known best practices (get a list at [examples/tips](https://github.com/theodorosploumis/docker-presentation/tree/gh-pages/examples/tips))

- Optimize containers (check [fromlatest.io](https://www.fromlatest.io/))
- Create your own tiny base
- Containers are not Virtual Machines
- Full stack Images vs 1 process per Container
- Create your private registry
- Create shortcut commands
- Volume database and code source to save state

---

### Docker NodeJS specific tips

- Keep the dependencies out of your app (npm_modules)
- Think of (micro)services and roles
- Use start scripts for containers with executable
- Use data only containers and share volumes
- Keep images small and version-specific
- In .dockerignore exclude ```.git, .gitignore, node_modules/```
- Prefer ```ENTRYPOINT ["npm", "start"]```

---

### Docker tools for NodeJS

[npm with/for Docker](https://www.npmjs.com/search?q=docker)

- [dockerode](https://www.npmjs.com/package/dockerode)
- [dockunit](https://www.npmjs.com/package/dockunit)
- [docker node tester, dnt](https://www.npmjs.com/package/dnt)
- [generator-docker](https://www.npmjs.com/package/generator-docker)

The [Docker ecosystem](http://comp.photo777.org/wp-content/uploads/2015/09/Docker-ecosystem-8.5.1.pdf) grows exponentially.

---

### Instead of Resources

- Join [beta.docker.com](https://beta.docker.com/) now!
- [Awesome Docker](https://github.com/veggiemonk/awesome-docker) (list of Docker resources & projects)
- [Docker cheat sheet](https://github.com/wsargent/docker-cheat-sheet)
- [Docker in Practice](https://www.manning.com/books/docker-in-practice), [The Docker Book](http://www.dockerbook.com/) (books)
- [Docker aliases/shortcuts](https://github.com/theodorosploumis/docker-presentation/tree/gh-pages/examples/shortcuts/docker-aliases.sh)
- [Docker introduction presentation](http://theodorosploumis.github.io/docker-presentation/)

---

### Questions

res.send('[Feedback](https://goo.gl/T7rE1o)');

![NodeJS with Docker!](https://raw.githubusercontent.com/theodorosploumis/docker-nodejs/gh-pages/img/docker_nodejs.png)

###### Tools used: [oh my zsh](http://ohmyz.sh/), [reveal.js](https://github.com/hakimel/reveal.js), [Simple Docker UI for Chrome](https://github.com/felixgborrego/docker-ui-chrome-app), [wharfee](https://github.com/j-bennet/wharfee), [dry](https://github.com/moncho/dry) and [docker 1.11.1](https://github.com/docker/docker/releases/tag/v1.11.1).

---

### Wait, Bonus!

> [SKGTech.io](http://skgtech.io) has a docker image and a **docker-compose.yml** file now.
