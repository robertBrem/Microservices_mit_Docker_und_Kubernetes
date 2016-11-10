# Aufgabe 1

## Applikation Dockerisieren
Den REST Service in ein Docker Image verpacken:
```bash
docker build -t robertbrem/cars .
```
Einen Docker Container auf einem anderen Port starten:
```bash
docker run -d 8081:8080 --name cars robertbrem/cars
```
Die Applikation testen:
```bash
curl http://localhost:8081/cars/resources/cars
```
