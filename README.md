# Kubernetes MongoDB + WebApp Demo

## Concepts Learned

- Kubernetes Deployments
- Services
- Labels and Selectors
- ConfigMaps
- Secrets
- Service Discovery
- NodePort Networking
- Minikube

## Architecture

Browser
  ↓
WebApp Service
  ↓
WebApp Pod
  ↓
Mongo Service
  ↓
Mongo Pod

## Secret Management

The repository includes a `mongo-secret.yaml` manifest with placeholder values, not real credentials. Before deploying to a cluster, generate a secure MongoDB username and password and create the secret locally.

Example commands:

- Linux / macOS:
  ```bash
  kubectl create secret generic mongo-secret \
    --from-literal=mongo-user="your-username" \
    --from-literal=mongo-password="your-password" \
    --dry-run=client -o yaml > mongo-secret.yaml
  ```

- Windows PowerShell:
  ```powershell
  kubectl create secret generic mongo-secret `
    --from-literal=mongo-user="your-username" `
    --from-literal=mongo-password="your-password" `
    --dry-run=client -o yaml > mongo-secret.yaml
  ```

If you prefer, replace the placeholder values in `mongo-secret.yaml` with base64-encoded credentials and apply the manifest with:

```bash
kubectl apply -f mongo-secret.yaml
```

## Key Debugging Experience

Resolved a Service-to-Pod connectivity issue caused by a label-selector mismatch that resulted in empty endpoints.