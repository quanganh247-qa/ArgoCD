# ArgoCD

``` kubectl create secret generic azure-secret -n crossplane-system --from-file=creds=./azure-credentials.json --dry-run=client -o yaml > azure-secret.yaml ```

``` cat azure-secret.yaml | kubeseal --controller-name=sealed-secrets-controller --controller-namespace=kube-system --format=yaml > sealed-secret.yaml ```

``` kubeseal --fetch-cert --controller-namespace=kube-system > sealed-secrets.crt ```

``` kubectl create secret generic azure-secret -n crossplane-system --from-file=creds=./azure-credentials.json --dry-run=client -o yaml | kubeseal --cert=sealed-secrets.crt --format=yaml > sealed-secret.yaml ```
