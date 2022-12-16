# Containers And Terms

## Docker Desktop (and Alternatives)
- GUI - Docker Desktop
## Docker CLI

The command line interface, provides the "docker" command, and uses an API exposed by the `docker daemon` 


## Container Image

- The set of "layers" that make up what you need to run a piece of software using Docker.

Just the software, it's "environment", and all the dependencies bundled together.


## Container

A running instance of a container image.

program on hard drive : a running program :: container image : container

## Dockerfile

A file that by convention is called `Dockerfile`
And this has the instructions for creating our container image.


## "Build"
The process of taking a Dockerfile and creating a container image. Uses the `Dockerfile`

## Volumes
A way to "redirect" read and write operations inside the container to outside locations.

## Tag
A name for a container image. Often contains a "version"

## Repository
A group of related container images - can have multiple versions or targeted platforms.

## Registry
A service that stores docker container images. Docker hub is the "Default", but also available at Google, Microsoft, Github, etc.

Internally a company will have a container registry.

## Compose
A tool for running multiple containers on a machine as a "set" of related containers.

I use this sometimes for developer environments.

## Multi-Stage Build

Using multiple staged containers as part of the build process to deliver the smallest, least-exposed container ("final") to the registry.

> For Later


## Environment Variables

## Requests and Limits (Memory/CPU)