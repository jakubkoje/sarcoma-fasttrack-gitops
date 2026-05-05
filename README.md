# Sarcoma FastTrack GitOps

Minimal GitOps repository for the early WAC deployment points.

It demonstrates:

- frontend WebComponent deployment
- backend API deployment
- frontend-backend connection through `api-base`
- Polyfea link and content registration
- image version bumping through Kustomize Components
- Flux GitOps objects for the shared WAC cluster

## Render

```bash
kubectl kustomize clusters/localhost/prepare
kubectl kustomize clusters/localhost/install
kubectl kustomize clusters/wac-aks/install
kubectl kustomize clusters/wac-aks
```

## Local Smoke

Build images locally:

```bash
docker build -t xjelinekj/sarcoma-fasttrack-api:latest ../sarcoma-fasttrack-api
docker build -t xjelinekj/sarcoma-fasttrack-frontend:latest ../sarcoma-fasttrack-frontend
```

Apply locally when Polyfea and Envoy Gateway should be installed too:

```bash
kubectl apply -k clusters/localhost/prepare
kubectl apply -k clusters/localhost/install
```

Open:

```text
http://localhost/fea/sarcoma-fasttrack
```

Mongo Express is exposed locally through:

```text
http://localhost/fea/mongo-express
```

## Shared Cluster

After creating the three GitHub repositories and pushing images/releases, update URLs if needed, then use the WAC cluster context:

```bash
kubectl apply -k clusters/wac-aks
```

The application should appear at:

```text
https://wac-hospital.westeurope.cloudapp.azure.com/fea/sarcoma-fasttrack
```

The backend should be reachable through:

```text
https://wac-hospital.westeurope.cloudapp.azure.com/sarcoma-fasttrack-api/api/message
```
