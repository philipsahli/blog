---
title: "Welcome to Go"
date: 2020-02-23T20:09:48+01:00
description: My talk at Guild42.ch about Golang, why DevOps Teams must use the open source programming language as common language.
images: [/media/welcome-to-go-1.jpeg]
categories: [talk]
tags: [swisspost, golang]
language: en
slug: welcome-to-go
draft: false
---

## Golang as common language

In January 2020 I took the chance to present my talk "**Welcome to Go**" about the [Go Programming Language] at [Guild42.ch]. Guild42.ch is an association that organizes events on topics related to software development in Berne, Switzerland. 

Over 85 developers from around Berne were interested in the topic. Until there I was telling only Swiss Post stuff about Golang and argued about why the language is very useful. I felt ready to speak to more people about my personal and Swiss Posts journey with Go.

> [Announcement on Guild42.ch]
>
> The open source programming language has found many followers worldwide in recent years and mainstream technologies like Kubernetes has been written in Go. Due to the **simplicity** and wide range of use of the language, they use many DevOps teams, especially for aids in the system engineering area.
>
> Swiss Post is also following this path. In this lecture, Philip Sahli explains why and how he started Go, explains the elements of the language and the integrated tooling. The advantages of Go and the use in a DevOps team are emphasized.

### Presentation

{{< speakerdeck 987fa83270c64fe49a92d5ba9c20327c >}}

### Demo

> As a DevOps Engineer I need a kubectl plugin that lists used images in a [Kubernetes](/categories/kubernetes) cluster, so that I can list all images in the cluster easily.

The demonstration shows how to re-use code and how quickly a program is built and published on Github.

Tools used:
- Visual Studio Code with the Go extension
- goreleaser

![media/welcome-to-go-2.jpeg](/media/welcome-to-go-2.jpeg)

- Github Repositories with demo code
  - [philipsahli/kubectl-images]
  - [philipsahli/client-go-wrapper]

#### Result

     $ kubectl images
     kubectl-images:
     docker/kube-compose-controller:v0.4.23
     docker/kube-compose-api-server:v0.4.23
     k8s.gcr.io/coredns:1.3.1
     k8s.gcr.io/coredns:1.3.1
     infoblox/dnstools:latest
     k8s.gcr.io/etcd:3.3.10
     k8s.gcr.io/kube-apiserver:v1.15.5
     k8s.gcr.io/kube-controller-manager:v1.15.5
     k8s.gcr.io/kube-proxy:v1.15.5
     k8s.gcr.io/kube-scheduler:v1.15.5
     docker/desktop-storage-provisioner:v1.0
    

### More to come

Thanks to everyone who attended the event. I had a lot of fun and was **overwhelmed** by the interest.

{{< tweet 1221850625820053505 >}}


[Guild42.ch]: https://guild42.ch/
[Announcement on Guild42.ch]: https://guild42.ch/27-januar-2020-go/
[philipsahli/kubectl-images]: https://github.com/philipsahli/kubectl-images
[philipsahli/client-go-wrapper]: https://github.com/philipsahli/client-go-wrapper
[Go Programming Language]: https://golang.org/