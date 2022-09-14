#### Install the Bank-Vaults operator
```shell
helm repo add banzaicloud-stable https://kubernetes-charts.banzaicloud.com
helm upgrade --install vault-operator banzaicloud-stable/vault-operator --namespace <namespace>
```
    
#### Vault Instance
- Set the namespace in the rbac.yml file on line 48.
- Set the namespace in the cr.yml file on line 93, 110 and 168.
- Deploy the Vault Instance
```shell
kubectl apply -f rbac.yaml --namespace <namspace>
kubectl apply -f cr.yaml --namespace <namspace>
```

#### Deploy the webhook
```shell
helm repo add banzaicloud-stable https://kubernetes-charts.banzaicloud.com
helm upgrade --install vault-secrets-webhook banzaicloud-stable/vault-secrets-webhook --namespace <namespace>
```
    
#### Access Vault
- Get login token
```shell
kubectl get secrets vault-unseal-keys -o jsonpath={.data.vault-root} | base64 --decode
```
- Login Vault
```shell
export VAULT_SKIP_VERIFY=true
vault login <token>
```
