# Backend k8s resources

## Sealed Secrets

```bash
export KEY=$(openssl rand -base64 16)
export SECRET=$(openssl rand -base64 16)
export ADMIN_PASSWORD=toBeReplaced
export DB_PASSWORD=toBeReplaced
export EMAIL_SMTP_PASSWORD=toBeReplaced
export STORAGE_S3_SECRET=toBeReplaced
```

```bash
kubectl create secret generic --dry-run=client \
    backend-env \
    --namespace=time4games-prod \
    --from-literal=ADMIN_PASSWORD=$ADMIN_PASSWORD \
    --from-literal=KEY=$KEY \
    --from-literal=SECRET=$SECRET \
    --from-literal=DB_PASSWORD=$DB_PASSWORD \
    --from-literal=EMAIL_SMTP_PASSWORD=$EMAIL_SMTP_PASSWORD \
    --from-literal=STORAGE_S3_SECRET=$STORAGE_S3_SECRET \
    -o yaml \
    | kubeseal --format=yaml > env.sealed-secret.yaml
```

## Deplopy resources

```bash
kubectl apply -f .
```
