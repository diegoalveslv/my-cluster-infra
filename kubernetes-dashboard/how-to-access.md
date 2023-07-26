After deploying and creating ClusterRoleBinding, run

> kubectl proxy

Then access through <http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login>

And generate a token with

> kubectl -n kubernetes-dashboard create token admin-user
