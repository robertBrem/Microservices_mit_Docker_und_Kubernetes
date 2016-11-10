# Aufgabe 1

## Applikation Dockerisieren
Den REST Service in ein Docker Image verpacken:
```bash
docker build -t robertbrem/cars:1.0.0 .
```
Einen Docker Container auf einem anderen Port starten:
```bash
docker run -d -p 8081:8080 --name cars robertbrem/cars:1.0.0
```
Die Applikation testen:
```bash
curl http://localhost:8081/cars/resources/cars
```
