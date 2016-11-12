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
