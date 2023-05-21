# Adminer

## Sealed Secrets

```bash
export AUTH_USER=toBeReplaced
export AUTH_PASSWORD=$(openssl rand -base64 16)
echo "${AUTH_USER}:$(openssl passwd -stdin -apr1 <<< ${AUTH_PASSWORD})" >> auth
kubectl create secret generic --dry-run=client \
    adminer-basic-auth \
    --namespace=game-point-club \
    --from-file=auth \
    -o yaml \
    | kubeseal --format=yaml > adminer-auth.sealed-secret.yaml
rm auth
```
