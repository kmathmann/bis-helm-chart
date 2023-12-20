# Vorbereitung
Namespaces:
- bis 
- bis2

Domains: 
- department1.local 
- department2.local

# Notes
- Robert hat gezeigt, Helm Chart von extern installieren
- Ich zeige: Eigene App über Helmchart bereitstellen
  - Im Unternehmen
  - Für Kunden
- Als Beispiel soll jede Abteilung im Unternehmen eine Website bekommen und dafür wurde ein Helm Chart erstellt
- Chart.yaml und Values.yaml zeigen
- configmap.yaml zeigen
- zum bereitstellen packen
```
helm package app-chart -d charts
```

- Zeigen, dass die tgz erstellt wurde  
- Die 1 ist die Version im Namen  
- Kann so bereits manuell im Unternehmen an Personen verteilt werden  
- Jedoch unpraktisch, vorallem bei Continous Integration/Deployment  
- Z.B. **Version von 1.0 auf 1.1** 

```
helm package app-chart -d charts
```

- jetzt müssten wir die version nochmal an alle schicken
- Besser: Registry

- Hierzu indexieren wir zunächst den charts Ordener

```
helm repo index charts
```

```
git add *
git commit -m "add charts"
git push
```

- index.yaml zeigen

- Der Ordner charts kann mit einem beliebigen Werbserver bereitgestellt werden.  In diesem Fall Github Pages
- z.B. Gitlab oder Harbor als spezielle Registry

```
curl https://kmathmann.github.io/bis-helm-chart/charts/index.yaml
```

## Chart installieren

- Jetzt das eigene Chart deployen  
- Zunächst Repo hinzufügen

```
helm repo add bis-repo https://kmathmann.github.io/bis-helm-chart/charts/
```
```
helm repo list
```

- jetzt installieren


```
helm upgrade --install bis bis-repo/bis-app -n bis
```

```
curl department1.local
```

- Message für das Department anpassen und replicas erhöhen
```
helm upgrade --install bis bis-repo/bis-app -n bis --set message="Greetings to BIS!!" --set replicas=3
```

```
kubectl get pods -n bis
```

```
curl department1.local
```

## zweite Abteilung

- Jetzt wollen wir das gleiche Chart nochmal für eine zweite Abteilung releasen in einem neuen Namespace
```
helm upgrade --install bis bis-repo/bis-app -n bis2 -f department2-values.yaml
```
```
kubectl get pods -n bis2
```

```
curl department2.local
curl department1.local
```