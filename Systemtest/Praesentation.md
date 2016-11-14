# Aufgabe 1

## Systemtest erstellen
Lokal einen Systemtest erstellen.  
Mit dem failsafe Maven Goal kann man den Test ausführen:
```bash
mvn clean install failsafe:integration-test
```
Den Pfad über Environment Variablen setzten.
```bash
HOST=localhost PORT=8081 mvn clean install failsafe:integration-test
```
---
 
# Aufgabe 2

## Pipeline Step: Start Test Env
Einen Pipeline Step erstellen der eine Test-Umgebung für die entsprechende Version hochfährt.  
Man kann in Nashorn Java-Klassen verwenden wie z.B. den `FileWriter`:
```javascript
var FileWriter = Java.type("java.io.FileWriter");
```
Verwendet man ein geschütztes Repository muss man die Login-Informationen dem Kubernetes Cluster zur Verfügung stellen. Dafür gibt es in Kubernetes Secrets:
```bash
kubectl create secret docker-registry teamakey --docker-username=rob --docker-password=1234 --docker-email=robert.brem@adesso.ch --docker-server=teama.disruptor.ninja:30500
```
Nun muss man noch dem Deplyoment dieses Secret mitteilen:
```yaml
imagePullSecrets:
- name: teamakey
```

---

Folgendes Script kann dazu verwendet werden zu prüfen ob eine URL verfügbar ist:
```javascript
var testUrl = "curl --write-out %{http_code} --silent --output /dev/null http://teama.disruptor.ninja:31080/cars/resources/cars --max-time 2";
$EXEC(testUrl);
while ($OUT != "200") {
    $EXEC("sleep 1");
    $EXEC(testUrl);
    print($OUT);
}
```
