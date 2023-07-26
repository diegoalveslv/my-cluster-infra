1. Steps to create kind cluster https://kind.sigs.k8s.io/docs/user/ingress/#create-cluster
2. Create NGINX Ingress https://kind.sigs.k8s.io/docs/user/ingress/#ingress-nginx
3. Install kubernetes dashboard https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
3. Install ArgoCD https://argo-cd.readthedocs.io/en/stable/operator-manual/installation/
    * Helm installation https://github.com/argoproj/argo-helm/tree/main/charts/argo-cd#installing-the-chart
>  kubectl create ns argocd
helm install -n argocd argocd argo/argo-cd --set server.ingress.enabled=true --set server.ingress.hosts={argocd.172.18.253.215.nip.io}  
kubectl patch ingress argocd-server -n argocd -p '{"metadata":{"annotations":{"nginx.ingress.kubernetes.io/ssl-passthrough":"true"}}}'  
kubectl patch deployment ingress-nginx-controller -n ingress-nginx --type='json' -p='[{"op": "add", "path": "/spec/template/spec/containers/0/args/-", "value": "--enable-ssl-passthrough"}]'  
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d


Get WSL ip address: ip addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}'