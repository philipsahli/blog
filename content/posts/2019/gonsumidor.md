---
title: Gonsumidor
date: 2019-01-06T12:17:01+02:00
categories: [writing,golang]
tags: [typography, elements]
language: en
slug: gonsumidor
---
Gonsumidor

Zweck

Gonsumidor ist ein in Go implementierte Applikation, die den Counter-Service von Gontador verwendet.
Als Protokoll wird gRPC (HTTP/2 bases RPC) verwendet. Somit braucht es zwei Implementationen:

- Erweiterung von Contador durch ein gRPC Server-Interface https://github.com/philipsahli/gontador/pull/2  
- Erstellung von Gonsumidor als gRPC Client https://github.com/philipsahli/gonsumidor 

Was kommt als nächstes

SSL: https://medium.com/pantomath/how-we-use-grpc-to-build-a-client-server-system-in-go-dd20045fa1c2 
