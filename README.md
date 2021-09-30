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
2. Add [overlays](./src/bundle/config/overlays/) and [values](./src/bundle/config/values.yaml)
3. Test your bundle: `ytt --data-values-file src/example-values/minikube.yaml  -f target/bundle/config` providing a sample values file from [example-values](./src/examples-values/)
4. Build your bundle `./hack/build.sh`
5. Add it to the [failk8s-repo](https://github.com/failk8s-packages/failk8s-repo) and publish the new repo and test the package from there, or [test with local files](./target/test)

**NOTE**: `develop` versions will not be image locked and will have a version of 0.0.0+develop to comply with semver.