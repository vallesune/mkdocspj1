---
layout: default
title: "Sprint 5.Logs"
permalink: projecte1/sprint5/
---

## 1. Logs

### Explicacio i proves

syslog

### Centralitzar

centralitzar


# TASCA CONJUNTA: Configuració de Rsyslog per a Enviament de Logs entre Hosts

**Data:** 03/03/26
**Components:**
Valle (Grup A)  
Pau (Grup B)

En aquesta pràctica configurem un sistema de **centralització de logs** utilitzant `rsyslog` entre dues màquines Ubuntu dins la mateixa xarxa.
Imaginem que un profe vol visualitzar els logs dels alumnes. En aquesta pràctica simularem aquest escenari:
Un host actuarà com a **servidor de logs (Profe)** i l’altre com a **client (Alumne)** que enviarà els seus registres al servidor.

---

# Pas 1: Preparació de les màquines (ambdós hosts)

Primer de tot configurem la xarxa i preparem les màquines perquè es puguin comunicar correctament.

## Configuració de les IPs

Configurem les adreces IP a cada màquina, ja sigui des de la configuració de xarxa d’Ubuntu o utilitzant eines de terminal com `nmcli` o `netplan`.

![Configuració IP](https://github.com/user-attachments/assets/814be02b-72eb-4080-949a-ea548ac7281b)

Comprovem que les IPs s'han aplicat correctament amb una comanda com:

```
ip a
````

![IPs dels hosts](https://github.com/user-attachments/assets/02725cad-a757-4603-b749-912b4c455b21)

---

## Desactivació del Firewall

Per evitar que el firewall bloquegi el tràfic de logs, desactivem `ufw` temporalment:

```
sudo ufw disable
```

![Desactivar firewall](https://github.com/user-attachments/assets/4d003f67-a7aa-41c5-8639-ddeed38214e7)

---

## Instal·lació de rsyslog

Normalment `rsyslog` ja està instal·lat per defecte a Ubuntu, però per assegurar-nos-ho executem:

```
sudo apt update
sudo apt install rsyslog -y
```

![Instal·lació rsyslog](https://github.com/user-attachments/assets/15559735-4340-4c36-8d2a-0ac76828cd47)

---

# Pas 2: Configuració del servidor (Profe)

Ara configurem la màquina que actuarà com a **servidor de logs**, és a dir, la que rebrà els registres dels altres hosts.

Editem el fitxer de configuració principal de `rsyslog`:

```
sudo nano /etc/rsyslog.conf
```

![Edició rsyslog.conf](https://github.com/user-attachments/assets/f8f893e9-ca0b-4071-a5db-36da1901ec52)

Busquem les següents línies i eliminem el comentari (`#`) per habilitar la recepció de logs via **UDP**:

```
module(load="imudp")
input(type="imudp" port="514")
```

Aquestes línies indiquen a `rsyslog` que escolti missatges entrants al **port 514**, que és el port estàndard per a syslog.

> Si volguéssim utilitzar **TCP**, hauríem d'habilitar també el mòdul `imtcp`.

---

## Reiniciar el servei

Un cop guardada la configuració reiniciem el servei:

```
sudo systemctl restart rsyslog
```

![Reiniciar rsyslog](https://github.com/user-attachments/assets/bd66d1dd-3309-44c8-b6cd-ba75f6b37fb8)

---

# Pas 3: Configuració del client (Alumne)

Ara configurem la màquina client perquè **envii tots els logs al servidor**.

Editem el fitxer de configuració de regles per defecte:

```
sudo nano /etc/rsyslog.d/50-default.conf
```

![Configuració client](https://github.com/user-attachments/assets/fd5a27fd-61de-4f79-84cf-d400db2a5288)

Al final del fitxer afegim la següent línia:

```
*.* @192.168.1.10:514
```

Significat de la configuració:

* `*.*` → enviem **tots els logs de tots els serveis**
* `@` → enviament via **UDP**
* `@@` → enviament via **TCP**
* `192.168.1.10` → IP del servidor de logs
* `514` → port de recepció del servidor

---

## Reiniciar el servei al client

Després de modificar la configuració reiniciem `rsyslog`:

```
sudo systemctl restart rsyslog
```

![Reiniciar rsyslog client](https://github.com/user-attachments/assets/bd66d1dd-3309-44c8-b6cd-ba75f6b37fb8)

---

# Pas 4: Verificació i prova final

Finalment comprovem que el sistema de logs funciona correctament.

## Al servidor (Profe)

Deixem el servidor escoltant els logs en temps real:

```
tail -f /var/log/syslog
```

---

## Al client (Alumne)

Enviem un missatge de prova amb la comanda `logger`:

```
logger "prova d’enviament de logs"
```

I tal com es veu a la captura, ho ha rebut correctament:

![Recepció dels logs](https://github.com/user-attachments/assets/46ea9d4c-5cdd-4f0f-b5a1-86968e57fade)

---

# Conclusió

Amb aquesta configuració hem aconseguit implementar un sistema de **centralització de logs** utilitzant `rsyslog`.

Això permet que un servidor rebi i emmagatzemi els registres de múltiples màquines, facilitant:

* la **monitorització del sistema**
* la **detecció d’errors**
* l’**anàlisi de seguretat**

Aquest tipus de configuració és molt utilitzada en **infraestructures de sistemes i xarxes** per tenir un control centralitzat de tots els esdeveniments del sistema.

---




## Actualitzacions centralitzades

### Server

jjj


### Client

ssss
