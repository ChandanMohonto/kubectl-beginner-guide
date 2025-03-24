# Kubectl Beginner Guide

## What is `kubectl`?
`kubectl` is a command-line tool used to interact with Kubernetes clusters. It allows users to deploy applications, inspect and manage cluster resources, and troubleshoot applications running in Kubernetes.

## Installation
Follow the official Kubernetes documentation to install `kubectl`:
- [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

## Basic Commands

### Check Kubernetes Cluster Information
```sh
kubectl cluster-info
```
Output:
```
Kubernetes control plane is running at https://127.0.0.1:6443
CoreDNS is running at https://127.0.0.1:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
```

### List Nodes (Requires Permission)
```sh
kubectl get nodes -o wide
```
Possible Error Output (If permission is denied):
```
Error from server (Forbidden): nodes is forbidden: User "demo@example.com" cannot list resource "nodes" in API group "" at the cluster scope.
```

### Get All Services in a Namespace
```sh
kubectl get svc -n default
```
Example Output:
```
NAME                                TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)          AGE
backend-demo                        NodePort      10.117.71.175   <none>          3001:31739/TCP   88d
kubernetes                          ClusterIP     10.117.64.1     <none>          443/TCP          376d
demo-web                            LoadBalancer  10.117.75.22    34.165.251.243  3000:31241/TCP   111d
demo-service-producer               ClusterIP     10.117.70.114   <none>          9001/TCP         55d
demo-token-streams                  ClusterIP     10.117.68.183   <none>          9001/TCP         4d2h
```

### Port Forward a Service to Local Machine
```sh
kubectl -n default port-forward svc/demo-service-producer 9001:9001
```
This command forwards traffic from port `9001` on your local machine to port `9001` of `demo-service-producer` running in Kubernetes.

### Describe a Service
```sh
kubectl describe svc demo-service-producer -n default
```
This provides detailed information about the specified service.

### Delete a Service
```sh
kubectl delete svc demo-service-producer -n default
```
Deletes the specified service from the cluster.

## Explanation of `kubectl get svc` Output

| Column         | Description |
|---------------|-------------|
| NAME          | The name of the service |
| TYPE          | Type of service (`ClusterIP`, `NodePort`, `LoadBalancer`) |
| CLUSTER-IP    | Internal IP address of the service |
| EXTERNAL-IP   | External IP assigned (if applicable) |
| PORT(S)       | Ports exposed by the service, with mappings for NodePort |
| AGE           | How long the service has been running |

## More Resources
- [Kubernetes Official Docs](https://kubernetes.io/docs/)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

---
Happy Learning! 🚀
