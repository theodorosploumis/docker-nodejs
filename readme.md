![Docker logo](https://raw.githubusercontent.com/theodorosploumis/docker-nodejs/gh-pages/img/docker_logo.png)

## Docker for NodeJS

#### [NodeJS Meetup Thessaloniki](http://www.meetup.com/Thessaloniki-Node-js-Meetup/), June 2016

_________________
###### [TheodorosPloumis.com](http://www.theodorosploumis.com/en) / [@theoploumis](twitter.com/theoploumis)
###### Get them: [online presentation](http://theodorosploumis.github.io/docker-nodejs/) / [source code](https://github.com/theodorosploumis/docker-nodejs) / [docker image](https://hub.docker.com/r/tplcom/docker-nodejs/)

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

### Steps of a Docker workflow

```
docker run -i -t ubuntu /bin/bash
```

 - Pulls the ubuntu [image](https://docs.docker.com/engine/userguide/containers/dockerimages/ "A read-only layer that is the base of your container. It can have a parent image to abstract away the more basic filesystem snapshot.") from the [registry](https://docs.docker.com/registry/ "The central place where all publicly published images live. You can search it, upload your images there and when you pull a docker image, it comes the repository/hub.")
 - Creates a new [container](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/ "A runnable instance of the image, basically it is a process isolated by docker that runs on top of the filesystem that an image provides.")
 - Allocates a filesystem and mounts a read-write [layer](https://docs.docker.com/engine/reference/glossary/#filesystem "A set of read-only files to provision the system. Think of a layer as a read only snapshot of the filesystem.")
 - Allocates a [network/bridge interface](https://www.wikiwand.com/en/Bridging_%28networking%29 "")
 - Sets up an [IP address](https://www.wikiwand.com/en/IP_address "An Internet Protocol address (IP address) is a numerical label assigned to each device (e.g., computer, printer) participating in a computer network that uses the Internet Protocol for communication.")
 - Executes a process that you specify (``` /bin/bash ```)
 - Captures and provides application output

---

### Agenda

 1. Public [NodeJS](https://hub.docker.com/search/?page=1&q=nodejs&starCount=0) images and Dockerfiles
 2. Try NodeJS* apps
 3. Dockerizing NodeJS
 4. Docker for development
 5. Test with Docker
 6. CI/CD
 7. Scaling NodeJS apps

---

### Public images and Dockerfiles

Let's explore [hub.docker.com](https://hub.docker.com)

 - [node/0.10.45](https://github.com/nodejs/docker-node/blob/5e058d36cc69303d1f62d424615fa03e050f20ef/0.10/Dockerfile)
 - [node/slim](https://hub.docker.com/r/library/node/tags/slim/)
 - [jprjr/tinynode](https://hub.docker.com/r/jprjr/tinynode/)
 - [shawnzhu/ruby-nodejs](https://hub.docker.com/r/shawnzhu/ruby-nodejs/)
 - [scratch](https://hub.docker.com/_/scratch/)
 - [nodesource explicit images](https://github.com/nodesource/docker-node#usage)

###### Topics: basics, images, Dockerfile, hub

---

### Try apps and software

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

### Dockerizing NodeJS

```
FROM nodesource/jessie:0.12.13

# Set the NodeJS environment to dev (vs production)
ENV NODE_ENV dev

# cache package.json and node_modules to speed up builds
ADD package.json package.json
RUN npm install

# Add your local files to the image
ADD . /path/to/app

# Setup the workdir
WORKDIR /path/to/app

# Expose ports
EXPOSE 3000

CMD ["npm","start"]
```
###### Topics: npm, cache layers

---

### Using Docker for NodeJS development

Some basic NodeJS-specific tips

 - Keep the dependencies out of your app
 - Think of (micro)services
 - Use start scripts for containers with executable
 - Use data only containers and share volumes
 - Keep images small and version-specific
 - In .dockerignore exclude ```.git, .gitignore, node_modules/```

---

### Using Docker for NodeJS - Example 1



---

### Continuous Integration & Deployment

---

### Scaling NodeJS apps

---

### Docker tips

There are known best practices (see a list at [examples/tips](https://github.com/theodorosploumis/docker-presentation/tree/gh-pages/examples/tips))

- Optimize containers (check [fromlatest.io](https://www.fromlatest.io/))
- Create your own tiny base
- Containers are not Virtual Machines
- Full stack Images vs 1 process per Container
- Create your private registry
- Create shortcut commands
- Volume database and code source to save state

---

### Questions?

![NodeJS with Docker!](https://raw.githubusercontent.com/theodorosploumis/docker-nodejs/gh-pages/img/docker_nodejs.png)

###### Tools used: [oh my zsh](http://ohmyz.sh/), [reveal.js](https://github.com/hakimel/reveal.js) and [docker 1.11.1](https://github.com/docker/docker/releases/tag/v1.11.1).

---

### Bonus!

> Get the [SKGTech.io docker image](https://github.com/skgtech/skgtech.io-docker)
