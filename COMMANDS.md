
helm package app-chart -d charts


helm repo index charts


git add * && git commit -m "add charts" && git push


curl https://kmathmann.github.io/bis-helm-chart/charts/index.yaml

## Chart installieren


helm repo add bis-repo https://kmathmann.github.io/bis-helm-chart/charts/



helm repo list



helm upgrade --install bis bis-repo/bis-app -n bis



kubectl get all -n bis



curl department1.local



helm upgrade --install bis bis-repo/bis-app -n bis --set message="Greetings to BIS!!" --set replicas=3


kubectl get pods -n bis

curl department1.local


## zweite Abteilung

helm upgrade --install bis bis-repo/bis-app -n bis2 -f department2-values.yaml


kubectl get pods -n bis2


curl department2.local
curl department1.local
