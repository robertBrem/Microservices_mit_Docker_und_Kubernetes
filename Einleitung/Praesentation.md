class: center, middle

# Microservices mit Docker und Kubernetes
## Einleitung & Kursübersicht

---

# Inhalt

* Demo
* Entwickeln & Fragen
* Fragen & Entwickeln

[Link zur Präsentation](https://rawgit.com/robertbrem/Microservices_mit_Docker_und_Kubernetes/master/Einleitung/Praesentation.html)  
Pattern:  
rawgit.com/robertbrem/Microservices_mit_Docker_und_Kubernetes/master/  
**Einleitung/Praesentation.html**

---
class: center

# Demo

.image-75[
  [![demo](images/demo.png)](http://adesso.disruptor.ninja:30180)
]

---

# Aufgabe 0

## Basic Tools installieren
[GIST](https://gist.github.com/robertBrem/2b382911e967692e240f)  
Testen ob es funktioniert hat:
```bash
rob@teama:~/Desktop$ ansible --version
ansible 2.2.0.0
  config file = /etc/ansible/ansible.cfg
  configured module search path = Default w/o overrides
```
Git installieren:
```bash
sudo apt-get update && sudo apt-get install git -y
```

---

# Aufgabe 0

## Bevorzugte Entwicklungsumgebung aufsetzen
Seine bevorzugten Entwicklungsumgebung und Tools installieren, z.B. mit Ansible:  
Ansible Repository für diesen Kurs clonen.
```bash
git clone https://github.com/robertBrem/Microservices_Ansible_Setup
```
Im File `playbooks/basicSetUp.yml` die Tools die man nicht installieren möchte kommentieren (`#`). Danach die Installation starten:
```bash
sudo ansible-playbook playbooks/basicSetUp.yml
```

---

# Aufgabe 1

## REST Service erstellen
Einen REST Service mit seiner bevorzugten Programmiersprache implementieren.

## Applikation Dockerisieren
Den REST Service in ein Docker Image verpacken.

---

# Aufgabe 3

## Zugangsfiles kopieren
`team[A,B,C].pem` und `team[A,B,C].conf` auf den Desktop kopieren.
```bash
chmod 400 team[A,B,C].pem
```
Testen ob man auf den Server connecten kann:
```bash
rob@teama:~/Desktop$ ssh -i team[A,B,C].pem ubuntu@[MASTER:IP]
The authenticity of host '[MASTER:IP] ([MASTER:IP])' can't be established.
ECDSA key fingerprint is SHA256:1WuIoToQUhYCeco87+tanj5trGe+UUH4SYwh9pfzHTk.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[MASTER:IP]' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-45-generic x86_64)
...
Last login: Wed Nov  9 08:46:56 2016 from 62.2.43.87
ubuntu@ip-172-30-0-70:~$ 
  ``` 
---
  
`kubectl` von Master Server auf den Desktop kopieren.
```bash
scp -i team[A,B,C].pem ubuntu@[MASTER:IP]:/usr/bin/kubectl .
```
Alias für `kubectl` erstellen:
```bash
alias kc='/home/rob/Desktop/kubectl --kubeconfig /home/rob/Desktop/team[A,B,C].conf'
```
Testen ob man die Kubernetes Nodes sieht:
```bash
rob@teama:~/Desktop$ kc get no
NAME             STATUS    AGE
ip-172-30-0-68   Ready     2h
ip-172-30-0-69   Ready     2h
ip-172-30-0-70   Ready     2h
ip-172-30-0-71   Ready     2h
```

