Golang s2i container image
===================

This repository contains the source for building various versions of
the Go application as a reproducible s2i container image.
Users can choose between RHEL, Fedora and CentOS based builder images.
The resulting image can be run using [podman](https://github.com/containers/libpod), [Docker](http://docker.io) or using [source-to-image](https://github.com/openshift/source-to-image/).
Also the whole pipeline from build to app deployment could be run on top of the [Openshift Origin](https://www.okd.io/) or [Red Hat's Openshift](https://www.openshift.com/).

Build
---------------------
```
$ podman build -t quay.io/smileyfritz/golang-builder:1.20.10
```

Usage
---------------------
Create the imagestreams:
```
$ oc replace -f imagestreams/golang-fedora.json
```
Create a test application:
```
$ oc new-app golang:1.20.10~https://github.com/kondohiroki/go-boilerplate.git
```
Verify that the application has started:
```
$ oc get builds
NAME               TYPE     FROM          STATUS     STARTED         DURATION
go-boilerplate-1   Source   Git@c32c51a   Complete   3 minutes ago   2m6s
```



* **IMPORT_URL**

    Used to specify the golang application import URL (i.e. usually something like github.com/someorg/somerepo), that is build. Necessary for the incremental build to function.

* **INSTALL_URL**

    Used to specify the golang application import URL of the main package (i.e. usually something like github.com/someorg/somerepo/subfolder). Necessary if the main package is not in the root folder of the repository.
