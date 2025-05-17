## Set up

### Prerequisites

- Use kind to create a Kubernetes cluster.
- Use Ingress-nginx as the Ingress controller.

Step 1. Create a Kubernetes cluster with kind

```bash
cat <<EOF | kind create cluster --config=-
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
  extraPortMappings:
  - containerPort: 80
    hostPort: 80
    protocol: TCP
  - containerPort: 443
    hostPort: 443
    protocol: TCP
EOF
```

Step 2. Install Ingress-nginx

```bash
kubectl apply -f https://kind.sigs.k8s.io/examples/ingress/deploy-ingress-nginx.yaml
```

Check if the Ingress-nginx controller is running:

```bash
kubectl get pods -n ingress-nginx
```

Step 3. Verify the Ingress-nginx installation

```bash
kubectl apply -f https://kind.sigs.k8s.io/examples/ingress/usage.yaml
```

Check if the Ingress-nginx is working:

```bash
# should output "foo-app"

curl localhost/foo

# should output "bar-app"

curl localhost/bar
```

ref. https://kind.sigs.k8s.io/docs/user/ingress
