# distroless-python
TLDR: This repo contains sample apko.yaml files to generate containers for building and running Chainguard's distroless images for python. Please read about distroless at [distroless.dev].

## Overview
This repo contains file to help you build distroless base images for use with python containerized applications. `example/Dockerfile` demostrates a sample multi-stage build (separate builder and run base images). These two base images are generated by [apko](https://github.com/distroless/apko). The builder image is generated using `apko-python-builder.yaml` and the run image is generated using `apko-python.yaml`. Note, this example is tailored around a python flask application with gunicorn. You may need to adjust base image packages in the `apko-python.yaml` file for your use case.

## Get the apko development image
To create these distroless images you will need the [apko](https://github.com/distroless/apko) tool. Follow the instructions to pull the docker image.

## Creating the builder image
1. Use the apko image to build and output the python-builder.tar file:

```
docker run -v $PWD:/work distroless.dev/apko build apko-python-builder.yaml \ 
YOUR-REPO/python-distroless-builder:latest python-builder.tar
```

Be sure to replace YOUR-REPO.

2. Load the builder image from the tar file:

`docker image load --input python-builder.tar`

3. Replace YOUR-REPO and push the image:

`docker push YOUR-REPO/python-distroless-builder:latest`

## Creating the run image
1. Use the apko image to build and output the python.tar file:

```
docker run -v $PWD:/work distroless.dev/apko build apko-python.yaml \
YOUR-REPO/python-distroless:latest python.tar
```

Be sure to replace YOUR-REPO.

2. Load the builder image from the tar file:

`docker image load --input python.tar`

3. Replace YOUR-REPO and push the image:

`docker push YOUR-REPO/python-distroless:latest`

## Use the produced base images

See the `example/Dockerfile` for example usage. 

## Feedback
Please send me any feedback and pull requests.
