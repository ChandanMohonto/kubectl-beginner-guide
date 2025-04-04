# Kubectl Beginner Guide

## What is `kubectl`?
`kubectl` is a command-line tool used to interact with Kubernetes clusters. It allows users to deploy applications, inspect and manage cluster resources, and troubleshoot applications running in Kubernetes.

## Installation
Follow the official Kubernetes documentation to install `kubectl`:
- [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

## Basic Commands

### Check Kubernetes Cluster Information
```sh
kubectl cluster-info  # Shows basic information about the cluster
```
Output:
```
Kubernetes control plane is running at https://192.168.1.1:6443
CoreDNS is running at https://192.168.1.1:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
```

### List Nodes (Requires Permission)
```sh
kubectl get nodes -o wide  # Lists all nodes in the cluster with detailed information
```
Possible Error Output (If permission is denied):
```
Error from server (Forbidden): nodes is forbidden: User "demo@example.com" cannot list resource "nodes" in API group "" at the cluster scope.
```

## Basic Functions of `kubectl`

### View Cluster Information
```sh
kubectl cluster-info  # Displays the cluster control plane information
kubectl get nodes  # Lists all available nodes in the cluster
```

### Manage Pods
```sh
kubectl get pods  # Lists all running pods in the current namespace
kubectl describe pod <pod-name>  # Shows detailed information about a specific pod
kubectl logs <pod-name>  # Fetches logs from a specific pod
kubectl delete pod <pod-name>  # Deletes a specific pod
```

### Manage Services
```sh
kubectl get svc  # Lists all services running in the cluster
kubectl describe svc <service-name>  # Shows detailed information about a specific service
kubectl delete svc <service-name>  # Deletes a specific service
```

### Manage Deployments
```sh
kubectl get deployments  # Lists all deployments in the cluster
kubectl describe deployment <deployment-name>  # Shows detailed information about a specific deployment
kubectl delete deployment <deployment-name>  # Deletes a specific deployment
```

### Port Forwarding (Expose a Service Locally)
```sh
kubectl port-forward svc/<service-name> <local-port>:<service-port>  # Forwards a service port to local machine
```
Example:
```sh
kubectl port-forward svc/demo-service 8080:80  # Exposes the service on localhost:8080
```
This lets you access `http://localhost:8080` as if you were inside the cluster.

## Example Output for `kubectl get svc`
```sh
kubectl get svc -n default  # Lists services in the 'default' namespace
```
Example Output:
```
NAME                        TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)         AGE
backend-demo                NodePort      10.96.1.10      <none>          3001:31234/TCP  50d
demo-web                    LoadBalancer  10.96.1.20      34.123.45.67    80:31241/TCP    20d
demo-service-producer       ClusterIP     10.96.1.30      <none>          9001/TCP        10d
```

## Explanation of `kubectl get svc` Output

| Column       | Description |
|-------------|-------------|
| NAME        | The name of the service |
| TYPE        | Type of service (`ClusterIP`, `NodePort`, `LoadBalancer`) |
| CLUSTER-IP  | Internal IP address of the service |
| EXTERNAL-IP | External IP assigned (if applicable) |
| PORT(S)     | Ports exposed by the service, with mappings for NodePort |
| AGE         | How long the service has been running |

## Common Use Cases
- Checking the health of your cluster
- Deploying applications
- Debugging and troubleshooting
- Scaling applications
- Managing network access (e.g., port-forwarding)

## More Resources
- [Kubernetes Official Docs](https://kubernetes.io/docs/)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

---
Happy Learning! 🚀
