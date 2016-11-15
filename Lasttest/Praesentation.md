# Aufgabe 1

## Lokal einen JMeter Test ausführen
Zuerst muss man JMeter installieren.
```bash
sudo apt-get update && sudo apt-get install jmeter -y
```
Mit dem Befehl `jmeter` kann man JMeter starten. Nun erstellt man einen ersten Last Test:  
Rechtsklick auf *Test Plan* *Add -> Threads (User) -> Thread Group*  
*Number of Threads (users):* **5**  
*Ramp-Up Period (in seconds):* **1**  
*Loop Count:* **100**  

Rechtsklick auf *Thread Group* *Add -> Sampler -> HTTP Request*  
*Server Name or IP:* **teama.disruptor.ninja**  
*Port Number:* **31080**  
*Path:* **/cars/resources/cars**  

Rechtsklick auf *Thread Group* *Add -> Listener -> Summary Report*  

*Start*

Den Testplan in einem neuen Projekt unter **/src/test/jmeter/test.jmx** speichern.  
Den Test ausprobieren mit:
```bash
mvn clean verify
```

Den Test Parametrisieren:
```bash
${__property(host)}
```
```bash
mvn clean verify -Dperformancetest.webservice.host=teama.disruptor.ninja -Dperformancetest.webservice.port=31080
```
