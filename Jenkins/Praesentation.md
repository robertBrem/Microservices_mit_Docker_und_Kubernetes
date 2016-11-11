# Aufgabe 1

## Jenkins einrichten
Auf Basis [dieses Deployments](https://gist.github.com/robertBrem/77e7a97b57565921792631f70088c706) Jenkins analog zu Gogs aufsetzen.  
`jenkins_home` ist speziel, da dieser Folder initial nicht leer ist sondern gefüllt. Daher muss man hier den Pod zuerst **ohne** `jenkins_home` Volume starten und dann den Inhalt auf den entsprechenden Node an die entsprechende Stelle kopieren. Dazu geht man wie Folgt vor:  
Man startet das Jenkins-Deployment ohne das `jenkins_home` Volume zu mounten - entsprechende Stellen in der Definition kommentieren. Danach meldet man sich auf dem Node mit dem entsprechenden Label an und sucht mit Hilfe von `docker ps` die Container ID von Jenkins:  
```bash
ubuntu@[MASTER:IP]:~$ sudo docker ps
CONTAINER ID        IMAGE                                              COMMAND                  CREATED             STATUS              PORTS               NAMES
cb435aac4587        robertbrem/jenkins:1.0.2                           "/bin/bash -c ./run.s"   3 minutes ago       Up 3 minutes                            k8s_jenkins.378e8601_jenkins-901550487-xvhub_default_8e264b64-a7a5-11e6-aab3-027250afa2a1_8317a739
1a9399def0d1        gcr.io/google_containers/pause-amd64:3.0           "/pause"                 4 minutes ago       Up 4 minutes                            k8s_POD.d8dbe16c_jenkins-901550487-xvhub_default_8e264b64-a7a5-11e6-aab3-027250afa2a1_a25bac71
fba407160666        weaveworks/weave-npc:1.8.0                         "/usr/bin/weave-npc"     39 hours ago        Up 39 hours                             k8s_weave-npc.b0329552_weave-net-v47pb_kube-system_3e17e7b5-a65a-11e6-aab3-027250afa2a1_53f37b64
...
```
In diesem Fall: **cb435aac4587**.

---

Nun Kopiert man den `jenkins_home` Folder auf den Node und benennt ihn entsprechend:
```bash
sudo docker cp cb435aac4587:/var/jenkins_home .
mv jenkins_home/ jenkins-home
```
Nun muss man noch die Berechtigungen des Folders und der Dateien auf dem Node anpassen:
```bash
sudo chown -R 1000:1000 jenkins-home/
```
Danach wechselt man wieder aud den lokalen Host und fährt das Deployment runter:
```bash
kc delete deployment jenkins
```
Kommentier das `jenkins_home` Volume wieder ein und startet das Deployment und den Service.

---

# Aufgabe 2

## Jenkins Pipeline mit REST Service erstellen
Die erste Stage der Jenkins Pipeline für den REST Service erstellen - `git pull`, `mvn clean install` und gegebenenfalls die JUnit-Testergebnisse veröffentlichen.  
Als Vorlage kann [dieses Script](https://gist.github.com/robertBrem/b18dee521176a3d75026cbe902d16b2f) verwendet werden.
