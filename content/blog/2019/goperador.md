---
title: Goperador
date: 2019-01-06T12:17:01+02:00
categories: [tutorial]
tags: [operator, golang]
language: en
slug: goperador
draft: true
---

Goperador

https://blog.openshift.com/introducing-the-operator-framework/

Neben Go operator gibt es auch Ansible und Helm operators.

Workflow

The following workflow is for a new Go operator:
1. Create a new operator project using the SDK Command Line Interface(CLI)
2. Define new resource APIs by adding Custom Resource Definitions(CRD)
3. Define Controllers to watch and reconcile resources
4. Write the reconciling logic for your Controller using the SDK and controller-runtime APIs
5. Use the SDK CLI to build and generate the operator deployment manifests


operator-sdk new operator
cd operator
operator-sdk add api --api-version=app.example.com/v1alpha1 --kind=GontadorService
operator-sdk add controller --api-version=app.example.com/v1alpha1 --kind=GontadorService

Edit 
     deploy/crds/app_v1alpha1_gontadorservice_cr.yaml -> to define the resources for the service
     deploy/operator.yaml -> to use our operator image

Eval `minishift docker-env`

operator-sdk build $(minishift openshift registry)/gontador/goperador

docker push $(minishift openshift registry)/gontador/goperador

oc login -u admin

docker login -u admin -p $(oc whoami -t) $(minishift openshift registry)
docker push $(minishift openshift registry)/gontador/goperador:latest

oc login -u system:admin

cc new-project gontador-operator

kubectl create -f deploy/service_account.yaml 
kubectl create -f deploy/role.yaml
kubectl create -f deploy/role_binding.yaml
kubectl create -f deploy/crds/app_v1alpha1_gontadorservice_crd.yaml

oc get crd | grep gontador                                                               
   gontadorservices.app.example.com                                         2019-01-09T11:06:05Z

kubectl create -f deploy/operator.yaml

oc get deployments                                                                       
NAME       DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
operator   1         1         1            0           29s

kubectl create -f deploy/crds/app_v1alpha1_gontadorservice_cr.yaml

oc login -u system:admin

oc get gontadorservice






Common errors:
- Docker push needs to push in the repository with the same name like the namespace
- 

