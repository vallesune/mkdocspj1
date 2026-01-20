---
layout: default
title: "Sprint 3.Dominis LDAP"
permalink: projecte1/sprint3/
---

## 1. LDAP

### Configurar servidor

#### Configuracions previes

Configurem la maquina virtual que utilitzarem com a servidor amb xarxa nat

<img width="462" height="257" alt="image" src="https://github.com/user-attachments/assets/f972ea6d-145d-4639-9f2b-53bf4e6b3ef7" />


Dins la mv configurem una ip fixa

<img width="462" height="257" alt="image" src="https://github.com/user-attachments/assets/1657dbf2-1061-491a-b354-0fc2185d7f1d" />


Ens descarregem del moodle els archius base de configuracio

<img width="462" height="257" alt="image" src="https://github.com/user-attachments/assets/2a5011b4-8e6a-46ee-a945-b6970043480e" />


Cambiem el hostname de la maquina a /etc/hostname i despres a /etc/hosts, indicant tambe el nom del domini

<img width="548" height="162" alt="Captura de pantalla de 2026-01-08 13-26-55" src="https://github.com/user-attachments/assets/5e113d96-e5ac-48fe-8be0-7bda0850e3bb" />
<img width="548" height="162" alt="Captura de pantalla de 2026-01-08 13-28-18" src="https://github.com/user-attachments/assets/8b2dfa3e-a899-41e4-9dc7-0e5fd0c68532" />



##### Configuracio LDAP

Instalem el paquet ldap-utils

<img width="724" height="440" alt="Captura de pantalla de 2026-01-08 13-30-07" src="https://github.com/user-attachments/assets/985b8b07-c9ae-462d-82db-6794ae24cfe5" />


S'obrira l'instalador i indiquem que no volem ometre la configuracio

<img width="724" height="440" alt="Captura de pantalla de 2026-01-08 13-40-21" src="https://github.com/user-attachments/assets/baa93469-6d89-4eef-8aa9-b2c869ef1738" />


Indiquem el nom del domini

<img width="724" height="440" alt="Captura de pantalla de 2026-01-08 13-42-38" src="https://github.com/user-attachments/assets/644e5f7c-dd40-4ff2-95fc-714e36afd14f" />


I el de la organitzacio

<img width="724" height="440" alt="Captura de pantalla de 2026-01-08 13-40-39" src="https://github.com/user-attachments/assets/a2b08988-4a7d-4eed-975d-bdd4df95d079" />


Indiquem la contrasenya admin

<img width="724" height="440" alt="Captura de pantalla de 2026-01-08 13-40-55" src="https://github.com/user-attachments/assets/c062a72a-31ee-49d9-92f7-8c617d98371f" />


Indiquem que si es purgui l'anterior base de dades

<img width="724" height="440" alt="Captura de pantalla de 2026-01-08 13-41-05" src="https://github.com/user-attachments/assets/e7d6df2e-9f93-4eec-ad5d-7030d76bfe78" />


Despres de crearse podem comprovar que es correcte amb slapcat

<img width="724" height="440" alt="Captura de pantalla de 2026-01-08 13-41-46" src="https://github.com/user-attachments/assets/0174f8ac-9db2-44fa-ad65-0e8106f3b525" />


Si ens em equivocat en algun punt de l'instalador o volem modificar alguna cosa podem utilitzar la comanda "dpkg-reconfigure slapd"

<img width="724" height="440" alt="Captura de pantalla de 2026-01-08 13-41-46" src="https://github.com/user-attachments/assets/ea1f772a-2c3b-4904-9109-a18306c612bb" />


Si esta tot correcte descomprimirem el zip d'archiu que ens em baixat abans y desde terminal accedirem dins el fitxer uo.ldif i modificarem els dos dc (dominis) als nostres

<img width="724" height="440" alt="Captura de pantalla de 2026-01-08 13-41-46" src="https://github.com/user-attachments/assets/fc9eeae4-631e-484c-8721-93cf3b7ec46f" />


Guardem els canvis i amb ldapadd afegim el uo a partir del fitxer

<img width="724" height="440" alt="Captura de pantalla de 2026-01-08 13-41-46" src="https://github.com/user-attachments/assets/77c8874c-019b-4e42-bcf9-b7c617b9d466" />


Repetim la correcio amb el fitxer de grups i d'usuari

<img width="724" height="440" alt="Captura de pantalla de 2026-01-08 13-41-46" src="https://github.com/user-attachments/assets/5956f9a2-2e74-4fbe-8b32-d896734099ce" />

<img width="724" height="440" alt="Captura de pantalla de 2026-01-08 13-41-46" src="https://github.com/user-attachments/assets/ce5c3007-8984-40e6-b142-e99c07675ca2" />


Tornem a comprovar amb slapcat que esta correcte

<img width="558" height="660" alt="Captura de pantalla de 2026-01-08 13-50-39" src="https://github.com/user-attachments/assets/cdfa2d5f-fd47-4518-bdd7-23e3752c6960" />




### Configurar un client

Al igual que la maquina servidor, volem que la maquina client estigui en xarxa nat

<img width="462" height="257" alt="image" src="https://github.com/user-attachments/assets/9e05d00f-aec5-4962-a65e-a0410b34ff24" />


Comprovem que la conexio es correcta entre maquines amb un ping al server

<img width="739" height="267" alt="image" src="https://github.com/user-attachments/assets/1aa4493c-165d-438e-803f-bfd2e66ad9de" />


Instalem els paquets libnss-ldap, libpam-ldap i nscd

<img width="734" height="176" alt="image" src="https://github.com/user-attachments/assets/cb6c6c26-af56-4f91-aa98-2a438792723d" />


S'obrira l'instalador i indiquem la ip del server

<img width="736" height="439" alt="Captura de pantalla de 2026-01-08 13-56-51" src="https://github.com/user-attachments/assets/22ff01ce-d263-4452-91de-c851693fb33e" />


Despres el nom de domini

<img width="736" height="439" alt="Captura de pantalla de 2026-01-08 13-57-09" src="https://github.com/user-attachments/assets/fe60518a-4ad3-459a-9a25-cabaec27fb8e" />


Amb cn=admin en indiquem com a usuari

<img width="736" height="439" alt="Captura de pantalla de 2026-01-08 13-57-42" src="https://github.com/user-attachments/assets/fa640eab-3b05-4050-87a0-3d9d714cd1da" />


Si volem modificar o corregir alguna cosa podem utilitzar la comanda "dpkg-reconfigure ldap-auth-config"


Ara modificarem una serie de fitxers

Primer a /etc/nsswitch.conf afegirem els cuatre "ldap compat" davant de "files" per asegurar que busca els usuaris del ldap

<img width="736" height="439" alt="Captura de pantalla de 2026-01-08 14-02-50" src="https://github.com/user-attachments/assets/c6ec9901-6992-4046-b53a-43318b576d00" />



Despres al fitxer de configuracio seguent afegirem la linea "greeter-show-manual-login=true" per a que cuan iniciem sessio grafica per primera vegada amb un usuari del domini ens aparegui el menu de benvinguda d'ubuntu

<img width="731" height="164" alt="Captura de pantalla de 2026-01-08 14-07-10" src="https://github.com/user-attachments/assets/619e2dca-a563-4eff-906a-522d17b20b40" />


Al fitxer common-session afegim la ultima linea "session optional pam_mkhomedir.so skel=/etc/skel umask=022" per configurar les home dels nous usuaris de domini

<img width="736" height="439" alt="Captura de pantalla de 2026-01-08 14-05-55" src="https://github.com/user-attachments/assets/a2ae919c-543c-4d7a-ab45-afa99728641e" />


Per ultim al fitxer common-password a les linies remarcades s'ha borrat un token anomenat "useauthtok"

<img width="816" height="455" alt="Captura de pantalla de 2026-01-13 13-44-23" src="https://github.com/user-attachments/assets/1411ec1a-3b2f-4c7c-9580-7792c341c5ea" />



### Validacio del client

Si tot l'anterior esta correcte, des del client hauriem de poder veure i entrar a alu1, l'usuari de prova que em afegit amb el fitxer de usuari al servidor

Podem comprovar amb "getent passwd" que apareix alu1

<img width="731" height="164" alt="Captura de pantalla de 2026-01-08 14-08-47" src="https://github.com/user-attachments/assets/4d540fcc-d157-47a3-bf1e-35fcf909c8eb" />


Tambe intentant accedir amb "su alu1"

<img width="586" height="124" alt="Captura de pantalla de 2026-01-13 13-45-09" src="https://github.com/user-attachments/assets/27bb5281-3eb3-45e8-8017-051f32a42cfa" />


Per ultim podem reiniciar la maquina client i al moment d'inciar sessio triar "no esta a la llista" i entrar amb alu1 - alu1

<img width="588" height="133" alt="Captura de pantalla de 2026-01-13 13-49-31" src="https://github.com/user-attachments/assets/ae94cb14-7786-4b4f-9000-133466991efe" />


### Configuracio i us d'entorn grafic

#### Apache Directory Studio

Desde la pagina oficial ens descargem el .tar

<img width="1113" height="572" alt="Captura de pantalla de 2026-01-20 12-41-36" src="https://github.com/user-attachments/assets/7fa8cc19-2560-41ee-90b3-a2f922cf3496" />

Desde terminal accedim on tenim el .tar i el descomprimim

<img width="737" height="190" alt="Captura de pantalla de 2026-01-20 12-42-53" src="https://github.com/user-attachments/assets/60e44f2f-5115-4ccc-a0be-95d858a859a9" />


entrem dins la carpeta de continguts i podem iniciar l’executable

<img width="1198" height="287" alt="Captura de pantalla de 2026-01-20 12-49-28" src="https://github.com/user-attachments/assets/4aa22dc2-9cde-4f7a-bec1-d0322967464e" />

<img width="736" height="376" alt="Captura de pantalla de 2026-01-20 12-47-59" src="https://github.com/user-attachments/assets/e6c0f49c-db4b-4b00-a8db-1cf929026363" />


Amb apache directory studio podem crear i gestionar uo, grups, usuaris a nivell de proves, entre altres

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 12-52-45" src="https://github.com/user-attachments/assets/a87e3f29-de40-46fa-848e-4857c9db8a20" />


Primer em de crear una conexio ja existent, a "nou" triem "nova connexio"

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 12-52-45" src="https://github.com/user-attachments/assets/7e4f1cdb-6b2d-43ae-96bd-d9d95e991c9f" />


Configurem un nom de conexio, un hostname i el port de ldap

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-38" src="https://github.com/user-attachments/assets/1a76bb60-2a28-49b1-ad74-065008580237" />


configurem el dn amb l'usuari admin i la nostra contrasenya i comprovem que la connexio funciona abans de seguir

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-30" src="https://github.com/user-attachments/assets/72701bca-084b-49c1-8ca4-5b26469b5961" />

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/4c510fe5-36e0-40f8-9493-d8d0d1cc2e5f" />

#### UO

Ara podem crear una UO nova, triem "nova entrada"

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-14-34" src="https://github.com/user-attachments/assets/6933a630-4a86-42d4-ad72-1e9e02de074a" />


Despres afegim organizationalUnit

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-20-09" src="https://github.com/user-attachments/assets/81470b35-8f54-4930-93ab-38a782df3722" />


Configurem que volem afegir una uo i el nom

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-20-17" src="https://github.com/user-attachments/assets/bbd6f6b8-f037-4779-a805-eda6d13c58df" />


Veiem el resum i com es crea correctament a la connexio

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-20-22" src="https://github.com/user-attachments/assets/d9509ad0-afc1-4de8-ba0a-c7c42d30ecf7" />

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-20-29" src="https://github.com/user-attachments/assets/00310021-eb33-4f85-9081-0f1f69edb5c8" />


#### Grup

Per crear un grup tornem a afegir entrada nova i triem posixGrup per afegir

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-27-58" src="https://github.com/user-attachments/assets/6038a75c-db50-43ca-9ac3-da86e688c0fe" />


Configurem el cn

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-28-44" src="https://github.com/user-attachments/assets/6bae23a8-1196-4022-8574-74f9a05deabc" />


i un gid de grup

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-32-32" src="https://github.com/user-attachments/assets/277c1aff-c9df-499e-b300-806dccdb7bde" />


Es crea correctament

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-32-41" src="https://github.com/user-attachments/assets/9376cf7a-86ca-4090-b58c-42a56065db49" />


#### Usuari

Per crear un usuari al afegir entrada nova afegim inetOrgPerson i posixAccount per poder vincular l'usuari a un grup

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-39-37" src="https://github.com/user-attachments/assets/4bdd4187-3a7a-4575-b1e8-78ef584e0607" />


Afegim el uid del usuari i el de grup, que coinicdeixi amb el que tenim creat

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-40-37" src="https://github.com/user-attachments/assets/6d6dc1fd-eec2-4e01-8b2d-67a0a8e35db5" />


Acabem d'afegir mes informacio com el directori de home 

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-41-15" src="https://github.com/user-attachments/assets/1cc5a965-a9a3-401c-b69e-39a008f05329" />


Resultat final creat

<img width="1038" height="743" alt="Captura de pantalla de 2026-01-20 13-42-18" src="https://github.com/user-attachments/assets/fb1dbb2b-db46-4226-8c49-b9e8794c9f40" />



