---
title: "Tutorial"
date: 2020-03-26T11:39:59-04:00
draft: true
type: tutorial
---
# Getting Started


## What are Paketo Buildpacks?

**Paketo Buildpacks** are an implementation of [Cloud Native Buildpacks](https://buildpacks.io/). They provide the dependencies your application needs so you spend less time building images and more time developing applications.

- [Try Paketo Buildpacks](#try-paketo-buildpacks)
- [Learn Paketo Buildpacks](#learn-paketo-buildpacks)
- [Write Your Own](#write-a-paketo-buildpack)


## Try Paketo Buildpacks:
Before using a paketo buildpacks to build an application image we need the following tools.

**Pack** A command line tool designed to take and application build a runnable OCI image using Cloud Native Buildpacks.

  - Installation Steps found [here](https://buildpacks.io/docs/install-pack/)

**Docker**: A suite of tooling around building and managing images.

- Installation Steps found [here](https://docs.docker.com/install/) 

### Test Drive
Now with pack installed we can start building images as simply as:


```pack build <my-image-name> -p <path-to-application-root> --builder paketobuildpacks/builders:cflinuxfs3```

### Extras

Current builders:

- paketobuildpacks/builder:cflinuxfs3
- paketobuildpacks/builder:bionic
- paketobuildpacks/builder:tiny



## Learn Paketo Buildpacks

### What is all of this stuff
The above `pack build` command gives you a image what is a builder and where are the buildpacks?

A builder is a combination of a group of `buildpacks` and a underlying stack image that your application specific dependencies will be layered on top of.

The resulting OCI image will look a bit like this:




### Internals

### How they work
All Paketo buildpacks have the following layout on disk:

```
.
├── bin
│   ├── build
│   └── detect
└── buildpack.toml
```
This is a requirement enforced by the 

Here `detect` and `build` are executables that will be run in two separate phases.

#### Detect
During this phase all buildpacks inspect the applications source code to determine if they are needed by the application.

#### Build
During this phase the buildpacks can make additions to the application image, this may be in the form of setting `env` variables, adding binaries or supplying additional libraries. 

#### Further reading
For more information about Cloud Native Buildpacks API see the [buildpack-spec](https://github.com/buildpacks/spec/blob/master/buildpack.md)

#### Example:

To get a list of optional builders run 
```pack list-builders```

Building using buildpacks
Users can also use specific buildpacks with their pack build: 

```pack build <my-image-name> -p <path-to-application-root> --builder paketobuildpacks/builders:cflinuxfs3 --buildpack <buildpack>```



