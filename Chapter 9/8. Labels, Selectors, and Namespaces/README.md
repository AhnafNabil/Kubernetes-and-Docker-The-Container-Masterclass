# Using Labels and Selectors in Kubernetes for Pod Management

This documentation provides an overview of using labels and selectors in Kubernetes to manage and group Pods. We will explore how labels can be used for logical grouping and how selectors can efficiently search for and manipulate these groups. Additionally, we will touch upon the concept of Namespaces in Kubernetes.

## Overview

Kubernetes offers powerful orchestration capabilities, allowing more sophisticated management of containerized applications compared to Docker Swarm. One of these capabilities is the use of labels and selectors.

### Labels

Labels are key-value pairs associated with Kubernetes objects such as Pods. They provide a way to organize and manage objects logically. Each label is a tag that can be used to group Pods for sorting and operational purposes.

#### Example:

Consider we have four Pods:
- `Pink Light`
- `Pink Dark`
- `Blue Light`
- `Blue Dark`

We can label these Pods as follows:
- `Pink Light` and `Pink Dark` with the label `color: pink`
- `Blue Light` and `Blue Dark` with the label `color: blue`

Labels can be more elaborate to provide finer control, such as `shade: light` or `shade: dark`.

### Selectors

Selectors are used to filter and search for Kubernetes objects based on their labels. They complement the functionality of labels by enabling efficient grouping and manipulation of objects that share the same labels.

#### Example:

If we want to select all Pods labeled `color: pink`, we use a selector to filter them:
- This will return `Pink Light` and `Pink Dark`.

Selectors can also be combined to narrow down the search. For instance, to select the `Pink Light` Pod, we can use:
- `color: pink` and `shade: light`

### Namespaces

Namespaces in Kubernetes provide a way to logically isolate resources. Each Namespace is a separate environment, allowing resources to be managed independently. This means we can have two Pods with the same name in different Namespaces.

#### Example:

- `namespace1` has a Pod named `example-pod`
- `namespace2` also has a Pod named `example-pod`

Both Pods can coexist because they are isolated in different Namespaces.

## Practical Demonstration

### 1. Listing Existing Pods

Start by listing the available Pods:

```sh
kubectl get pods
```

### 2. Adding Labels to Pods

Create a YAML file `pods-with-labels.yaml` to define our Pods with labels:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pink-light
  labels:
    color: pink
    shade: light
spec:
  containers:
  - name: nginx
    image: nginx

---
apiVersion: v1
kind: Pod
metadata:
  name: pink-dark
  labels:
    color: pink
    shade: dark
spec:
  containers:
  - name: nginx
    image: nginx

---
apiVersion: v1
kind: Pod
metadata:
  name: blue-light
  labels:
    color: blue
    shade: light
spec:
  containers:
  - name: nginx
    image: nginx

---
apiVersion: v1
kind: Pod
metadata:
  name: blue-dark
  labels:
    color: blue
    shade: dark
spec:
  containers:
  - name: nginx
    image: nginx
```

Apply the configuration:

```sh
kubectl apply -f pods-with-labels.yaml
```

### 3. Using Selectors to Filter Pods

To select Pods with the label `color: pink`:

```sh
kubectl get pods -l color=pink
```

This will return `pink-light` and `pink-dark`.

To select the `Pink Light` Pod specifically:

```sh
kubectl get pods -l color=pink,shade=light
```

### 4. Working with Namespaces

Create two Namespaces and deploy Pods with the same name:

```sh
kubectl create namespace namespace1
kubectl create namespace namespace2
```

Deploy a Pod named `example-pod` in both Namespaces using YAML files:

`example-pod-namespace1.yaml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
  namespace: namespace1
spec:
  containers:
  - name: nginx
    image: nginx
```

`example-pod-namespace2.yaml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
  namespace: namespace2
spec:
  containers:
  - name: nginx
    image: nginx
```

Apply the configurations:

```sh
kubectl apply -f example-pod-namespace1.yaml
kubectl apply -f example-pod-namespace2.yaml
```

List Pods in each Namespace:

```sh
kubectl get pods -n namespace1
kubectl get pods -n namespace2
```

### Summary

In this documentation, we explored how to use labels and selectors in Kubernetes to logically group and manage Pods. Labels provide a flexible way to tag Kubernetes objects, while selectors enable efficient filtering and grouping. Additionally, we covered how Namespaces allow logical isolation of resources, enabling the use of duplicate names in different contexts. These features enhance the orchestration capabilities of Kubernetes, making it a powerful tool for managing containerized applications.