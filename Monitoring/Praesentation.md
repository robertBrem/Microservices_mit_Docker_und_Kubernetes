# Aufgabe 1

## Dashboard einrichten.  
```bash
kc create -f https://rawgit.com/kubernetes/dashboard/master/src/deploy/kubernetes-dashboard.yaml
```
Der Service für das Dashboad definiert, dass es einen NodePort gibt, definiert jedoch nicht selber einen Port. 
Den Port kann man jedoch auslesen.  
```bash
kc describe --namespace kube-system svc kubernetes-dashboard
```
Danach kann man das Dashboard auf diesem Port aufrufen.  
**Achtung: ** Security!  
Eine andere sicherere Lösung wäre den automatisch generierten Service zu löschen und selber einen Service zu erstellen der 
auf einen Port mapped der noch nicht belegt ist. Danach kann man den Service mit `kc proxy` auf seinen `localhost` umleiten und 
er ist nicht im Internet verfügbar sondern nur auf seinem lokalen Host.

---

# Aufgabe 2

## Monitoring mit Prometheus
Monitoring mit Prometheus einrichten.  
```bash
kc create -f https://raw.githubusercontent.com/coreos/blog-examples/master/monitoring-kubernetes-with-prometheus/prometheus.yml
```
Danach einen Service für Prometheus einrichten.

---

# Aufgabe 3

## Scope einsetzen
Einen User auf [cloud.weave.works](https://cloud.weave.works) erstellen.  
Danach das Addon im Cluster installieren:
```bash
kc apply -f 'https://cloud.weave.works/launch/k8s/weavescope.yaml?service-token=[TOKEN]'
```
