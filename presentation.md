![Docker logo](https://raw.githubusercontent.com/theodorosploumis/docker-nodejs/gh-pages/img/docker_logo.png)

## Docker for NodeJS

#### [NodeJS Meetup Thessaloniki](http://www.meetup.com/Thessaloniki-Node-js-Meetup/), June 2016

###### [TheodorosPloumis.com](http://www.theodorosploumis.com/en) / [@theoploumis](twitter.com/theoploumis)
________________________

###### Get them: [online presentation](http://theodorosploumis.github.io/docker-nodejs/) / [source code](https://github.com/theodorosploumis/docker-nodejs) / [docker image](https://hub.docker.com/r/tplcom/docker-nodejs/)

---

### Let me ask you

- Who knows about [Docker]([docker.com](http://docker.com))?
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
 - Portable software
 - Microservices and integrations (APIs)
 - Simplify DevOps
 - Version control capabilities

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
 3. Docker for development
 4. Test with Docker
 5. CI/CD
 6. Scaling NodeJS apps

---

### Public images and Dockerfiles

---

### Try NodeJS apps

---

### Using Docker for NodeJS development

---

### Test with NodeJS and Docker

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

---

### Questions?

![NodeJS with Docker!](https://raw.githubusercontent.com/theodorosploumis/docker-nodejs/gh-pages/img/docker_nodejs.png)

###### In this presentation I have used [oh my zsh](http://ohmyz.sh/), [reveal.js](https://github.com/hakimel/reveal.js),  

---

### Bonus!

> Get the [SKGTech.io docker image](https://github.com/skgtech/skgtech.io-docker)
