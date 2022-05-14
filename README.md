# vault-unseal-helper
A container that can be used to unseal vault automatically in on-prem or dev clusters
This solution is recommended for those use case, where you are running Vault in DEV/QA/Staging cluster or an On Premise cluster, where you can afford to keep the keys and root token of the vault in the same cluster but you cant afford to maintain cloud based KMS or another Vault cluster to unseal vault.

The given solution defeats one of the use case of Vault where the attacker has got access to the cluster and want to get access to the credentials of the vault. But, it helps you maintain and use other usecases of Vault.

It is recommended to run it as K8s deployment so that if the cluster goes down and comes up, the deployment will automatically unseal the Vault and you get everything up and running in no time.

The container expects the following as environment variables:
- vault URL: VAULT_URL
- unseal keys: VAULT_KEYS
- retry frequency in seconds: RETRY_FREQUENCY

CURL requests will be made to the vault URL in fixed frequency to check if the vault is in sealed state. If the vault is not initialized, it will just skip the attempt to unseal Vault.

If the vault is in unseal, then it wont do anything and will again try for retry after a fixed frequency.

