# Vorbereitung
Namespaces:
- bis 
- bis2

Domains: 
- department1.local 
- department2.local

# Notes
- Robert hat gezeigt, wie man ein Helm Chart installiert welches z.B. von der Community für bestimmte Dienste bereitgestellt wird. Im Unternehmen gibt es aber genauso den Use Case die eigene Software über ein Helm Chart zu deployen.
- Chart kurs vorstellen
    - Idee: Webseite für die einzelnen Abteilungen des Unternehmens
- Um das Package anderen im Unternehmen den Abteilungen zur Verfügung zu stellen, müssen wir es zu einem Paket zusammenfassen
  
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

- index.yaml zeigen

- Der Ordner charts kann mit einem beliebigen Werbserver bereitgestellt werden.  
- z.B. Gitlab oder Harbor als spezielle Registry  
- Ich nutze zum Hosten der Dateien eine Github Page

```
git add *
git commit -m "add charts"
git push
```

- Github Repo mit Github Page - quasi Webserver  
- https://kmathmann.github.io/bis-helm-chart/charts 

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
kubectl get all -n bis
```

- Ausgabe zeigen  
- Browser: department1.local

```
curl department1.local
```

```
helm upgrade --install bis bis-repo/bis-app -n bis --set message="Greetings to BIS!!" --set replicas=3
```
```
kubectl get pods -n bis
```


- nochmal Website zeigen
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
- Browser: department2.local
```
curl department2.local
curl department1.local
```