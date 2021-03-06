---
title: "Install Using Yaml"
description: ""
lead: "Install KubeDL with YAML files."
date: 2021-03-30T17:46:36-07:00
lastmod: 2021-03-30T17:46:36-07:00
draft: false
images: []
menu:
  docs:
    parent: "prologue"
weight: 300
toc: true
---


## Install CRDs

From [git root directory](https://github.com/alibaba/kubedl), run

{{< btn-copy text="kubectl apply -f helm/kubedl/crds/" >}}
```bash
kubectl apply -f helm/kubedl/crds/
```

## Install KubeDL controller

A single yaml file including everything: deployment, rbac etc.

{{< btn-copy text="kubectl apply -f https://raw.githubusercontent.com/alibaba/kubedl/v0.3.0/config/manager/all_in_one.yaml" >}}
```bash
kubectl apply -f https://raw.githubusercontent.com/alibaba/kubedl/v0.3.0/config/manager/all_in_one.yaml
```
KubeDL controller is installed under `kubedl-system` namespace.

The official KubeDL controller image is hosted under [docker hub](https://hub.docker.com/r/kubedl/kubedl).

## Uninstall KubeDL controller

{{< btn-copy text="kubectl delete namespace kubedl-system" >}}
```bash
kubectl delete namespace kubedl-system
```

## Delete CRDs
```bash
kubectl delete crd elasticdljobs.training.kubedl.io marsjobs.training.kubedl.io mpijobs.training.kubedl.io pytorchjobs.training.kubedl.io tfjobs.training.kubedl.io xdljobs.training.kubedl.io xgboostjobs.training.kubedl.io
```

## Enable specific job Kind

KubeDL supports all kinds of jobs(tensorflow, pytorch etc.) in a single Kubernetes operator. You can selectively enable the kind of jobs to support.
There are three options:
1. Default option. Just install the job CRDs required. KubeDL will automatically enable the corresponding job controller.
2. Set env `WORKLOADS_ENABLE` in KubeDL container. The value is a list of job types to be enabled. For example, `WORKLOADS_ENABLE=TFJob,PytorchJob` means only Tensorflow and Pytorch Job are enabled.
3. Set startup flags `--workloads` in KubeDL container command args. The value is a list of job types to be enabled like `--workloads TFJob,PytorchJob`.
