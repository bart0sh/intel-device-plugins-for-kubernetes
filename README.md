[![Build Status](https://travis-ci.org/intel/intel-device-plugins-for-kubernetes.svg?branch=master)](https://travis-ci.org/intel/intel-device-plugins-for-kubernetes)
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/intel/intel-device-plugins-for-kubernetes/issues)

# Intel Device Plugins for Kubernetes

## Table of Contents

- [About](#about)
- [GPU device plugin](cmd/gpu_plugin/README.md)
- [FPGA device plugin](cmd/fpga_plugin/README.md)

## About

This repository contains set of Intel Device Plugins that enable usage of Intel hardware in Kubernetes cluster.

These are prerequisites for building and running Intel Device Plugins:

- Intel hardware
- Fully [configured kubernetes cluster]
- Working [Go environment]

## Supported Kubernetes versions

| Branch            | Kubernetes branch/version      |
|-------------------|--------------------------------|
| master            | Kubernetes 1.10 branch v1.10.x |
| master            | Kubernetes master branch       |

[Go environment]: https://golang.org/doc/install
[Configured Kubernetes cluster]: https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/
