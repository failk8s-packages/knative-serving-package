# knative-serving-package

This package provides knative-serving functionality using [knative-serving](https://knative.dev/).

## Components

* knative-serving
  * knative-net-contour
  * knative-cert-manager

## Configuration

The following configuration values can be set to customize the knative-serving installation.

### Global

| Value | Required/Optional | Description |
|-------|-------------------|-------------|
| `namespace` | Optional | The namespace in which to deploy knative-serving. |
| `domain.type` | Optional | DNS service to use. real means you're integrating with a cloud DNS, in which case you need to provide `domain.name`. Possible values: `real`, `xip.io`, `nip.io`, `sslip.io` (Defaults to: `real`|
| `domain.name` | Optional | Domain to use for your knative services when using a `real` DNS service. (Defaults to: ` `|
| `ingress.external.namespace` | Optional | Namespace where the ingress controller for externally exposed services is installed. (Defaults to: `projectcontour`|
| `ingress.internal.namespace` | Optional | Namespace where the ingress controller for internally exposed services is installed. (Defaults to: `projectcontour`|
| `tls.certmanager.clusterissuer` | Optional | Configure AutoTLS using the name of this ClusterIssuer. (Defaults to: ` `|

## Usage Example

This walkthrough guides you through using knative-serving...

## Develop checklist

1. Update your [config.json](./config.json) with the package info
2. Update your [vendir.yml](./src/bundle/vendir.yml) with your upstreams
3. `vendir sync` in `src/bundle` to fetch your new upstream files
4. Add [overlays](./src/bundle/config/overlays/) and [values](./src/bundle/config/values.yaml)
5. Update your [bundle.yml](./src/bundle/.imgpkg/bundle.yml) file
6. Test your bundle: `ytt -f config`
7. Lock images used: `kbld -f . --imgpkg-lock-output .imgpkg/images.yml`
8. Publish your bundle: `imgpkg push --bundle quay.io/failk8s/knative-serving-package:develop --file .`. These steps can be done via [hack/build-package.sh](./hack/build-package.sh)
9. Package up your k8s manifests and test in k8s [hack/package-manifests.sh](./hack/package-manifests.sh). The files will be in `target` folder.
