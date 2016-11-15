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
*Loop Count:* **5000**  

Rechtsklick auf *Thread Group* *Add -> Sampler -> HTTP Request*  
*Server Name or IP:* **teama.disruptor.ninja**  
*Port Number:* **31080**  
*Path:* **/cars/resources/cars**  

Rechtsklick auf *Thread Group* *Add -> Listener -> Summary Report*  

*Start* *No*  
