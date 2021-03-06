# Aufgabe 1

## Registry einrichten
Auf Basis [dieses Deployment](https://gist.github.com/robertBrem/3df0c7d672a9942bbbddb45d0b6f297a) eine Registry deployen.  
Um die Registry einzurichten meldet man sich zuerst auf dem Node mit dem entsprechenden Label an.  
**Wichtig:** Es muss der Node verwendet werden der im DNS eingetragen ist.  

Damit das Repository geschützt ist, erstellen wir einen Benutzer mit einem Passwort und legen diesen im Folder `registry/auth` ab.
```bash
mkdir registry
mkdir registry/images
mkdir registry/certs
mkdir registry/auth
sudo docker run --entrypoint htpasswd registry:2 -Bbn rob 1234 > registry/auth/htpasswd
```
---

Um HTTPS zu aktivieren braucht man SSL Zertifikate diese können auch direkt auf dem Node mit LetsEncrypt erstellt werden.  
```bash
sudo apt-get install letsencrypt -y
sudo letsencrypt certonly -d teama.disruptor.ninja
```
Die Zerfifkate werden dann in folgendem Folder abgelegt:  
```bash
/etc/letsencrypt/live/teama.disruptor.ninja
```
Den `fullchain.pem` und den `privkey.pem` verschiebt man nun in den `registry/certs` Folder.
```bash
sudo cp /etc/letsencrypt/live/teama.disruptor.ninja/fullchain.pem registry/certs/
sudo cp /etc/letsencrypt/live/teama.disruptor.ninja/privkey.pem registry/certs/
```

---

Hat man das Deployment und den Service gestartet kann man das Repository mit folgender URL testen:
```bash
https://teama.disruptor.ninja:30500/v2/_catalog
```

---

# Aufgabe 2

## Docker Image in Repository pushen
Nach jedem Build der Jenkins Pipeline soll ein neues Dockerimage erstellt werden und dieses soll dann in die Registry gepushed werden.

---

# Aufgabe 3

## Docker Registry UI
[Dieses Deployment](https://gist.github.com/robertBrem/750aef6a133824171573fe9db7e81266) und ein Service für eine Registry Visualisierung starten.
