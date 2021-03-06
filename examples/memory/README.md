# Memory examples

Memory example contains setup and tear down logic with default NSM infrastructure and memroy based registry backend.

## Requires

- [spire](../spire)

## Includes

- [Local Connection](../use-cases/LocalConnection)
- [Remote Connection](../use-cases/RemoteConnection)

## Run

Create ns for deployments:
```bash
kubectl create ns nsm-system
```

Register `nsm-system` namespace in spire:

```bash
kubectl exec -n spire spire-server-0 -- \
/opt/spire/bin/spire-server entry create \
-spiffeID spiffe://example.org/ns/nsm-system/sa/default \
-parentID spiffe://example.org/ns/spire/sa/spire-agent \
-selector k8s:ns:nsm-system \
-selector k8s:sa:default
```
Apply NSM resources for basic tests:

```bash
kubectl apply -k .
```

## Cleanup

```bash
kubectl delete ns nsm-system
```