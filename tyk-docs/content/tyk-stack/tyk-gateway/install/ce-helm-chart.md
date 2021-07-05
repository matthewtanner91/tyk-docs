---
title: "With Tyk Helm Chart"
date: 2021-07-01
tags: [""]
description: ""
menu:
  main:
    parent: "Kubernetes"
weight: 1
url: "/tyk-oss/ce-helm-chart/"
---

## Introduction

## Prerequisites

 - Redis. Redis is required for all of the Tyk installations and must be installed in the cluster or reachable from inside K8s.
 - MongoDB. If you are using the MongoDB pumps with your open source installation you will require MongoDB installed as well.

### Installing Redis and Mongo (if required)

{{< warning  success >}}
**Warning**

To get started quickly, you can use `redis.yaml` and `mongo.yaml` manifests to install Redis inside your Kubernetes cluster. Please note that these provided manifests must never be used in production and for a quick start evaluation only. Use external DBs or Official Helm charts for MongoDB and Redis in any other case. We provide these manifests so you can quickly have Tyk up and running, however they are not meant for long term storage of data.
{{< /warning >}}

```{copy.Wrapper}
kubectl create namespace tyk
kubectl apply -f deploy/dependencies/mongo.yaml -n tyk
kubectl apply -f deploy/dependencies/redis.yaml -n tyk
```
 ### Installing the Open Source Gateway

 See our short video on how to install the Tyk Open Source Gateway:

 {{< youtube mkyl38sBAF0 >}}

 ```{copy.Wrapper}
 helm install tyk-ce ./tyk-headless -n tyk
 ```

 ## Using TLS

 You can turn on the TLS option under the gateway section in your `values.yaml` file which will make a Gateways listen on port 443 and load up a dummy certificate. You can set your own default certificate by replacing the file in the `certs/` folder.

## Mounting Files

To mount files to any of the Tyk stack components, add the following to the mounts array in the section of that component. For example:

 ```{copy.Wrapper}
 - name: aws-mongo-ssl-cert
  filename: rds-combined-ca-bundle.pem
  mountPath: /etc/certs
```

 ## Next Steps Tutorials

Follow the Tutorials on the Open Source tabs for the following:

1. [Add an API](/docs/getting-started/tutorials/create-api/)
2. [Create a Security Policy](/docs/getting-started/tutorials/create-security-policy/)
3. [Create an API Key](/docs/getting-started/tutorials/create-api-key/)