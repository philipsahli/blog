---
title: "An introduction to the Operator SDK"
date: 2020-02-23T20:09:48+01:00
categories: [tutorial]
tags: [kubernetes, operator, golang]
language: en
slug:
draft: true
---

## Extending Kubernetes with an Operator

> The Operator Framework is an open source toolkit to manage Kubernetes native applications, called Operators, in an effective, automated, and scalable way.


[Operator-SDK][Operator-SDK] is an SDK for building operators using the Operator-Framework. There are several operator types with a [different set of capabilities](https://github.com/operator-framework/operator-sdk#operator-capability-level) (Helm / Ansible / Go). As Go covers the most features and has less limitations this tutorial covers the Go operator type.

![Operator-SDK](https://github.com/operator-framework/operator-sdk/raw/master/doc/images/operator_logo_sdk_color.svg?sanitize=true)

## Initialization

Create the project structure.

    operator-sdk new app-operator --repo github.com/philipsahli/myoperator
    cd myoperator

Add an API.
 
    operator-sdk add api --api-version=app.example.com/v1alpha1 --kind=AppService

## Building the operator

    USERNAME=philipsahli
    operator-sdk build quay.io/$USERNAME/myoperator

## Running the operator

[Operator-SDK]: https://github.com/operator-framework/operator-sdk 

### Locally

    operator-sdk run local

> Caveat that it runs not under the serviceaccount, but as user 

### In-cluster

    kubectl create -f deploy/service_account.yaml
    ...
    kubectl create -f deploy/operator.yaml

## Testing

As Test-driven development and to ensure the functionality over time and the operator evolves and gets more complex, Testing is very important.

### Unittesting

    go test ./...

This tries to run also the tests in the e2e directory. Therefore build-tags help to run 

    go test ./... --tags=unittest

### E2E

    operator-sdk test local ./test/e2e --go-test-flags "-v -parallel=2"

This deploys the operator with the Kubernetes resource defined in `deploy/operator.yaml`.

## Versioning

- [ ] Explain
- [ ] Workflow
- [ ] Where to replace

## More to come

- [ ] Prometheus

## References

- [https://github.com/operator-framework/operator-sdk/blob/master/doc/test-framework/writing-e2e-tests.md](https://github.com/operator-framework/operator-sdk/blob/master/doc/test-framework/writing-e2e-tests.md)