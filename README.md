# FreyaCluster

helm repo add argo-cd https://argoproj.github.io/argo-helm

helm install --create-namespace -n argocd argo-cd argo-cd/argo-cd  --set server.ingress.enabled=true --set server.ingress.paths[0]='/' --set server.extraArgs[0]="--insecure" --set server.ingress.hosts[0]='argocd.zxyxyhome.duckdns.org' --set controller.metrics.rules.enabled=true --set controller.metrics.serviceMonitor.enabled=true --set server.metrics.serviceMonitor.enabled=true



helm install --create-namespace -n argocd argo-cd argocd/argo-cd -f value-argocd.yaml

helm upgrade --create-namespace -n argocd argo-cd argocd/argo-cd -f value-argocd.yaml


curl https://raw.githubusercontent.com/zzxyxy/FreyaCluster/main/apps.yaml | kubectl apply -f -


# k3d

k3d cluster create --api-port 6550 \
    -p "0.0.0.0:80:80@loadbalancer" \
    -p "0.0.0.0:443:443@loadbalancer" \
    -p "0.0.0.0:1883:1883@loadbalancer" \
    -p "0.0.0.0:6379:6379@loadbalancer" \
    -p "0.0.0.0:5432:5432@loadbalancer" \
    -p "0.0.0.0:20001:20001@loadbalancer" \
    -p "0.0.0.0:20001:20001/udp@loadbalancer" \
    -p "0.0.0.0:20002:20002@loadbalancer" \
    -p "0.0.0.0:20002:20002/udp@loadbalancer" \
    -p "0.0.0.0:20003:20003@loadbalancer" \
    -p "0.0.0.0:20003:20003/udp@loadbalancer" \
    -p "0.0.0.0:20004:20004@loadbalancer" \
    -p "0.0.0.0:20004:20004/udp@loadbalancer" \
    --agents 4 z --subnet 172.18.0.0/16
