# Service Binding

![Test Workflow](https://github.com/kadras-io/package-for-service-binding/actions/workflows/test.yml/badge.svg)
![Release Workflow](https://github.com/kadras-io/package-for-service-binding/actions/workflows/release.yml/badge.svg)
[![The SLSA Level 3 badge](https://slsa.dev/images/gh-badge-level3.svg)](https://slsa.dev/spec/v1.0/levels)
[![The Apache 2.0 license badge](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Follow us on Bluesky](https://img.shields.io/static/v1?label=Bluesky&message=Follow&color=1DA1F2)](https://bsky.app/profile/kadras.bsky.social)

A Carvel package for [Service Binding](https://servicebinding.io), a standard and automated way for communicating service secrets to workloads.

## 🚀&nbsp; Getting Started

### Prerequisites

* Kubernetes 1.31+
* Carvel [`kctrl`](https://carvel.dev/kapp-controller/docs/latest/install/#installing-kapp-controller-cli-kctrl) CLI.
* Carvel [kapp-controller](https://carvel.dev/kapp-controller) deployed in your Kubernetes cluster. You can install it with Carvel [`kapp`](https://carvel.dev/kapp/docs/latest/install) (recommended choice) or `kubectl`.

  ```shell
  kapp deploy -a kapp-controller -y \
    -f https://github.com/carvel-dev/kapp-controller/releases/latest/download/release.yml
  ```

### Dependencies

Service Binding requires [cert-manager](https://github.com/kadras-io/package-for-cert-manager). You can install it from the [Kadras package repository](https://github.com/kadras-io/kadras-packages).

### Installation

Add the Kadras [package repository](https://github.com/kadras-io/kadras-packages) to your Kubernetes cluster:

  ```shell
  kctrl package repository add -r kadras-packages \
    --url ghcr.io/kadras-io/kadras-packages \
    -n kadras-system --create-namespace
  ```

<details><summary>Installation without package repository</summary>
The recommended way of installing the Service Binding package is via the Kadras <a href="https://github.com/kadras-io/kadras-packages">package repository</a>. If you prefer not using the repository, you can add the package definition directly using <a href="https://carvel.dev/kapp/docs/latest/install"><code>kapp</code></a> or <code>kubectl</code>.

  ```shell
  kubectl create namespace kadras-system
  kapp deploy -a service-binding-package -n kadras-system -y \
    -f https://github.com/kadras-io/package-for-service-binding/releases/latest/download/metadata.yml \
    -f https://github.com/kadras-io/package-for-service-binding/releases/latest/download/package.yml
  ```
</details>

Install the Service Binding package:

  ```shell
  kctrl package install -i service-binding \
    -p service-binding.packages.kadras.io \
    -v ${VERSION} \
    -n kadras-system
  ```

> **Note**
> You can find the `${VERSION}` value by retrieving the list of package versions available in the Kadras package repository installed on your cluster.
> 
>   ```shell
>   kctrl package available list -p service-binding.packages.kadras.io -n kadras-system
>   ```

Verify the installed packages and their status:

  ```shell
  kctrl package installed list -n kadras-system
  ```

## 📙&nbsp; Documentation

Documentation, tutorials and examples for this package are available in the [docs](docs) folder.
For documentation specific to Service Binding, check out [servicebinding.io](https://servicebinding.io).

## 🛡️&nbsp; Security

The security process for reporting vulnerabilities is described in [SECURITY.md](SECURITY.md).

## 🖊️&nbsp; License

This project is licensed under the **Apache License 2.0**. See [LICENSE](LICENSE) for more information.
