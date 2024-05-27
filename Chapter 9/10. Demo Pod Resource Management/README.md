# Managing Resource Requests and Limits in Kubernetes Pods

In Kubernetes, you can specify how much CPU and memory (RAM) each container needs within a Pod. Setting resource requests and limits helps the scheduler make better decisions about where to place Pods and ensures that containers do not consume excessive resources, potentially crashing the node.

## Step-by-Step Guide to Resource Management in Pods

### Listing Existing Pods

To begin, let's check the existing Pods in the cluster:

```sh
kubectl get pods
```

### Examining the YAML Configuration

Let's open the YAML file that defines our resource-managed Pod:

```sh
nano resource-pod.yaml
```

This file is slightly larger than previous examples because it defines a Pod with two containers: a MySQL database container and a WordPress frontend container. The Pod is named `frontend`.

### Pod and Container Specifications

#### Basic Configuration

In the `resource-pod.yaml` file, you will see typical configurations such as:
- **Pod Name**: `frontend`
- **Containers**: Two containers, one for MySQL and one for WordPress
- **Images**: Docker images for MySQL and WordPress
- **Environment Variables**: Specific to the applications

#### Resource Requests and Limits

The key section of this YAML file is the `resources` field for each container, which specifies the resource requests and limits.

Example resource specification for MySQL container:

```yaml
resources:
  limits:
    memory: "128Mi"
  requests:
    memory: "64Mi"
```

This sets the maximum memory limit to 128MB and the minimum memory request to 64MB for the MySQL container.

### Creating the Pod

Save and exit the file editor, then create the Pod using the following command:

```sh
kubectl create -f resource-pod.yaml
```

### Checking Pod Status

List the Pods to see their current status:

```sh
kubectl get pods
```

Initially, you might see that the Pod is still in the container creation state. After some time, you might notice that the Pod status changes to `CrashLoopBackOff`. This indicates that the containers are not running as expected.

### Investigating the Issue

To understand why the Pod is not running, use the describe command:

```sh
kubectl describe pod frontend
```

You may see that one container is running, while the other (MySQL) is terminated with a status of `OOMKilled` (Out Of Memory Killed). This means the resource limits provided are insufficient for the MySQL container.

### Troubleshooting and Resolution

To resolve this issue, delete the Pod:

```sh
kubectl delete pod frontend
```

Then, edit the `resource-pod.yaml` file to increase the resource limits:

```sh
nano resource-pod.yaml
```

Update the resource limits for both containers. For example:

```yaml
resources:
  limits:
    memory: "1Gi"
  requests:
    memory: "512Mi"
```

Save and exit the file, then recreate the Pod:

```sh
kubectl create -f resource-pod.yaml
```

### Verifying the Pod Status

List the Pods again to verify the status:

```sh
kubectl get pods
```

If everything is configured correctly, the Pod should be in the `Running` state within a few seconds.

To confirm the resource limits and successful creation, describe the Pod again:

```sh
kubectl describe pod frontend
```

You should see that both containers are running, and the resource limits have been applied as specified.

## Conclusion

By setting appropriate resource requests and limits, you can ensure that your containers have sufficient resources to run without risking node stability. This practice helps in better resource utilization and prevents resource contention among containers in a Kubernetes cluster.