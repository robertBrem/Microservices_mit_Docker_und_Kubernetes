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
