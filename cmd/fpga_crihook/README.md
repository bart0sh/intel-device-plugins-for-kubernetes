# Intel FPGA prestart CRI-O webhook for Kubernetes

# Table of Contents

* [Introduction](#introduction)
* [Dependencies](#dependencies)
* [Building](#building)
    * [Getting the source code](#getting-the-source-code)
    * [Building the image](#building-the-image)
* [Configuring CRI-O](#configuring-cri-o)

# Introduction

The FPGA CRI-O webhook is one of the components used to add support for Intel FPGA
devices to Kubernetes.

The FPGA prestart CRI-O hook is triggered by container annotations, such as set by the
[FPGA device plugin](../fpga_plugin).  It performs discovery of the requested FPGA
function bitstream and then programs FPGA devices based on the environment variables
in the workload description.

The CRI-O prestart hook is only *required* when the
[FPGA admission webhook](../fpga_admissionwebhook) is configured for orchestration
programmed mode, and is benign (un-used) otherwise.

> **Note:** The fpga CRI-O webhook is usually installed by the same DaemonSet as the
> FPGA device plugin. If building and installing the CRI-O webhook by hand, it is
> recommended you reference the
> [fpga plugin DaemonSet YAML](../../deployments/fpga_plugin/fpga_plugin.yaml) for
> more details.

# Dependencies

This component is one of a set of components that work together. You may also want to
install the following:

-   [FPGA device plugin](../fpga_plugin/README.md)
-   [FPGA admission controller](../fpga_admissionwebhook/README.md)

All components have the same basic dependencies as the
[generic plugin framework dependencies](../../README.md#about)

# Building

The following sections detail how to obtain, build and deploy the CRI-O
prestart hook.

## Getting the source code

```bash
$ mkdir -p $(go env GOPATH)/src/github.com/intel
$ git clone https://github.com/intel/intel-device-plugins-for-kubernetes $(go env GOPATH)/src/github.com/intel/intel-device-plugins-for-kubernetes
```

## Building the image

```bash
$ cd $(go env GOPATH)/src/github.com/intel/intel-device-plugins-for-kubernetes
$ make intel-fpga-initcontainer
...
Successfully tagged intel/intel-fpga-initcontainer:devel
```

# Configuring CRI-O

Recent versions of [CRI-O](https://github.com/cri-o/cri-o) are shipped with default configuration
file that prevents CRI-O to discover and configure hooks automatically.
For FPGA orchestration programmed mode, the OCI hooks are the key component.
Please ensure that your `/etc/crio/crio.conf` parameter `hooks_dir` is either unset
(to enable default search paths for OCI hooks configuration) or contains the directory
`/etc/containers/oci/hooks.d`.
