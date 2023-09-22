# General

Deploys the rocket-chat helm [chart](https://artifacthub.io/packages/helm/rocketchat-server/rocketchat).
Also deploys TLS issuers to the respective namespace and an Ingress for TLS.
# Deploy

Assumes godaddy as DNS provider.

```bash
$ export GODADDY_API_KEY=<your creds here>
$ export GODADDY_SECRET_KEY=<your creds here>
$ export MONGO_USER_SECRET="placeholder"
$ export MONGO_ROOT_SECRET="placeholder"
$ export OWNER_ID=<random id>
$ helm dependency update ./rocketchat
$ helm upgrade rocket-infra ./rocketchat --install --namespace default --set infra.enabled=true --set apiKey=$GODADDY_API_KEY --set secretKey=$GODADDY_SECRET_KEY --set external-dns.txtOwnerID=$OWNER_ID
$ helm upgrade rocket-app ./rocketchat --install --namespace default --set app.enabled=true --set rocketchat.mongodb.auth.passwords={$MONGO_USER_SECRET} --set rocketchat.mongodb.auth.rootPassword=$MONGO_ROOT_SECRET
```
