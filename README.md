Deploy to gitlab

```
curl --request POST \
     --form 'chart=@mynginx-1.tgz' \
     --user gitlab+deploy-token-helm-registry:zM_xkvVWos6FLrrLCy5n \
     https://gitlab.imn.htwk-leipzig.de/api/v4/projects/2549/packages/helm/api/stable/charts

```

1. `helm plugin install https://github.com/chartmuseum/helm-push`
2. ````
helm repo add --username gitlab+deploy-token-helm-registry --password zM_xkvVWos6FLrrLCy5n bis-registry  https://gitlab.imn.htwk-leipzig.de/api/v4/projects/2549/packages/helm/stable

helm repo add --username gitlab+deploy-token-helm-registry --password gldt-2owPUyDRxA5syeSBBwJu bis-registry-external  https://gitlab.com/api/v4/projects/53186228/packages/helm/stable

helm cm-push mychart-0.1.0.tgz project-1

```
https://ankush-chavan.medium.com/complete-guide-for-creating-and-deploying-helm-chart-423ba8e1f0e6
`helm package nginx-chart -d charts`
`helm repo index charts`



## Notes

helm package app-chart -d charts

-> Zeigen, dass die tgz erstellt wurde
-> Version von 1.0 auf 1.1
-> Nochmal packagen

helm package app-chart -d charts 

-> Indexieren

helm repo index charts

-> index.yaml zeigen
-> Zeigen: Github Repo mit Github Page - quasi Webserver
-> https://kmathmann.github.io/bis-helm-chart/charts 

clear

curl https://kmathmann.github.io/bis-helm-chart/charts/index.yaml

clear

-> Jetzt das eigene Chart deployen
-> Zunächst Repo hinzufügen

helm repo add bis-repo https://kmathmann.github.io/bis-helm-chart/charts/

-> jetzt installieren

helm upgrade --install bis bis-repo/bis-app -n bis

-> Ausgabe zeigen: 

--set customMessage="abcd"

