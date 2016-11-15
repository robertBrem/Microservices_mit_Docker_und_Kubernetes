# Aufgabe 1

## Canary Release erstellen
Eine neue `stage` für einen Canray Release erstellen.  
Hierzu kann man das `restart.js` Script von Test-Env kopieren und anpassen.  
Mit folgendem Script kann man die Ausgabe des Services testen.
```bash
while true; do curl http://teama.disruptor.ninja:30080/cars/resources/cars; echo ""; sleep 1; done
```
