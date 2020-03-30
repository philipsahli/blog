---
title: "Kubernetes Admission Controller"
date: 2020-02-23T20:21:52+01:00
categories: [tutorial]
tags: [kubernetes]
language: de
slug: asdf
draft: true
---

## Kubernetes Controlplane

Die Kubernetes Controlplane besteht aus folgenden Komponenten:

- apiserver
- controller-manager
- scheduler
- etcd

## Admission Controller

"Admission" heisst übersetzt auf deutsch "Eintritt".

### Anwendungsbeispiele

- Automatische Anpassung von Labels Kubernetes Ressourcen

## Umsetzung

### Aktivierung des "admission controller"

    --enable-admission-plugins=ValidatingAdmissionWebhook,MutatingAdmissionWebhook,...

### Webhook Konfiguration


    apiVersion: admissionregistration.k8s.io/v1beta1
    kind: MutatingWebhookConfiguration
    metadata:
    name: demo-webhook
    webhooks:
    - name: webhook-server.webhook-demo.svc
        clientConfig:
        service:
            name: webhook-server
            namespace: webhook-demo
            path: "/mutate"
        caBundle: ${CA_PEM_B64}
        rules:
        - operations: [ "CREATE" ]
            apiGroups: [""]
            apiVersions: ["v1"]
            resources: ["pods"]

### Implementierung

#### Webhook Server in Go

### Deployment

### Testen

    kubectl create -f

## References

- [https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/)
- [https://kubernetes.io/blog/2019/03/21/a-guide-to-kubernetes-admission-controllers/](https://kubernetes.io/blog/2019/03/21/a-guide-to-kubernetes-admission-controllers/)
- [https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/)