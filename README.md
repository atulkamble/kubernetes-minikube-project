# kubernetes-minikube-project
Create a basic Minikube project to host an application and check its output.

Minikube is a great tool for running a local Kubernetes cluster. Here's a step-by-step guide to create a basic Minikube project to host an application and check its output.

### Prerequisites

1. **Install Minikube:** Follow the instructions for your operating system from the [official Minikube documentation](https://minikube.sigs.k8s.io/docs/start/).
2. **Install kubectl:** The Kubernetes command-line tool. Follow the instructions from the [official Kubernetes documentation](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

### Step 1: Start Minikube

Open your terminal and start Minikube:

```sh
minikube start
```

### Step 2: Create a Simple Application

Let's use a simple Nginx web server as our application.

Create a YAML file called `nginx-deployment.yaml` with the following content:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

### Step 3: Deploy the Application

Use kubectl to apply the deployment:

```sh
kubectl apply -f nginx-deployment.yaml
```

### Step 4: Expose the Deployment

To access the application from outside the cluster, expose the deployment as a service:

```sh
kubectl expose deployment nginx-deployment --type=NodePort --port=80
```

### Step 5: Get the URL to Access the Application

Minikube provides a convenient way to get the URL for the service:

```sh
minikube service nginx-deployment --url
```

This command will return a URL. Open this URL in your web browser to see the Nginx welcome page.

### Step 6: Verify the Deployment

To check the status of your pods and services, use the following commands:

```sh
kubectl get pods
kubectl get services
```

You should see your Nginx pods running and the service exposed.

### Step 7: Clean Up

When you're done, you can delete the deployment and stop Minikube:

```sh
kubectl delete deployment nginx-deployment
minikube stop
```

### Summary

You've created a basic Minikube project, deployed a simple Nginx application, exposed it as a service, and accessed it via a URL. This setup is perfect for testing and development purposes. For production environments, you would typically use a more robust Kubernetes setup.
