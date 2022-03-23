# Docker best practice
- Choose right Base image
    - [Use official as Base image](#use-official)
    - [Using specific version of image](#using-specific)
    - [Select small-sized of image](#select-small-sized)
- Make docker build faster
    - [Exclude un-using resource](#exclude-un-using-resource)
    - [Optimize cached image layers](#optimize-cached)
- Security and/with less contents
    - [Use of Multiple-stage builds](#multiple-stage-builds)
    - [Least Privileged User](#privileged-User)
    - [Scan Images for Security Vulnerabilities](#security-vulnerabilities)
## Use official
## Using specific
## Select small-sized

## Exclude un-using resource
.dockerignore
### Multiple .dockerignore
We can now use multiple *.dockerignore* files in Docker.
#### First step
We need to enable BuildKit mode; this is done either by setting:

```sh
    $ export DOCKER_BUILDKIT=1
```
or configure the Docker daemon by typing a json Docker [daemon configuration](https://docs.docker.com/engine/reference/commandline/dockerd/) file. by adding this configuration or set buildkit is true:
```json
{ "features": { "buildkit": true } }
```
to the Docker daemon configuration in *~/.docker/daemon.json* and restarting the daemon. This will be enabled by default in future.

#### Next step:
We also need to prefix the name of our *.dockerignore* file with the Dockerfile name. so we Dockerfile is called *prod.Dockerfile* the ignore file needs to be called *prod.dockerignore*.

## Optimize cached
## Multiple stage builds
## Privileged-User
## Security Vulnerabilities
