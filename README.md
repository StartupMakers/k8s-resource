# Kubernetes Resource

Deploys [Kubernetes](http://kubernetes.io/) configuration using [kubectl](http://kubernetes.io/docs/user-guide/kubectl-overview/).

## Source Configuration

* `url`: *Required.* URL of Kubernetes API Server.
* `username`: *Required.* Username for accessing to API Server.
* `password`: *Required.* Password for accessing to API Server.
* `namespace`: *Required.* Namespace name which should be used.
* `skip_tls_verify`: *Optional.* If true, the server's certificate will not be checked for validity. This will make your HTTPS connections insecure. Default: `false`.
* `cert_data`: *Optional.* Client certificate for TLS. Default: empty.
* `key_data`: *Optional.* Client certificate key for TLS. Default: empty.
* `ca_data`: *Optional.* Certificate authority. Default: empty.

## Behavior

### `check`: *Did not implemented yet.*

### `in`: *Did not implemented yet.*

### `out`: Push a configuration.

Apply a configuration YML (or JSON) file to a resource in Kubernetes API Server with using [kubectl apply](http://kubernetes.io/docs/user-guide/kubectl/kubectl_apply/).

Also it checks that deployment has been processed successfully.

#### Parameters

* `spec_path`: *Required.* Path to configuration file.

#### Example

+ Define a resource type:

  ```yaml
  resource_types:
    - name: k8s-resource
      type: docker-image
      source:
        repository: StartupMakers/k8s-resource
  ```

+ Define a resource using this resource type:

  ```yaml
  resources:
    - name: my-cluster
      type: k8s-resource
      source:
        url: 192.168.0.1:3000/k8s-resource
        namespace: dev-space
  ```

+ Push configuration to your Kubernetes API Server:

  ```yaml
  - put: my-cluster
    params:
      spec_path: my-pod-spec.yml
  ```
