# Notes

helm package app-chart -d charts

-> Zeigen, dass die tgz erstellt wurde
-> Die 1 ist die Version im Namen
-> Kann so bereits manuell im Unternehmen an Personen verteilt werden
-> Jedoch unpraktisch, vorallem bei Continous Integration/Deployment
-> Z.B. Version von 1.0 auf 1.1
-> Nochmal packagen

helm package app-chart -d charts 

-> jetzt müssten wir die version nochmal an alle schicken

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

