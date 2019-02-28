# Deploying OPA

## Local installation

See [openpolicyagent.org/docs/get-started](https://www.openpolicyagent.org/docs/get-started.html#prerequisites).

## Plain Docker

OPA releases are available as images on Docker Hub:
[hub.docker.com/r/openpolicyagent/opa/](https://hub.docker.com/r/openpolicyagent/opa/)

See [openpolicyagent.org/docs/deployments](https://www.openpolicyagent.org/docs/deployments.html#docker)

## Deployment as a Central Service on Kubernetes

See [openpolicyagent.org/docs/deployments](https://www.openpolicyagent.org/docs/deployments.html#kubernetes)

## Sidecar Deployment on Kubernetes (Recommended)

```yaml
# ...

containers:
- name: application
# ...

- name: opa
image: openpolicyagent/opa:latest
ports:
- name: http
    containerPort: 8181
args:
- "run"
- "--ignore=.*"  # exclude hidden dirs created by Kubernetes
- "--server"
- "/policies"
volumeMounts:
- readOnly: true
    mountPath: /policies
    name: example-policy
# ...
```