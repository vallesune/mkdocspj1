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

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/613ee3e9-5367-4ff7-82a6-5f73f2394f15" />


Despres afegim organizationalUnit

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/85dc5551-b52a-411c-9c43-c6623e4ab6d3" />


Configurem que volem afegir una uo i el nom

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/083d8569-7024-4306-9371-47ad06975013" />


Veiem el resum i com es crea correctament a la connexio

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/893658c1-709d-4585-a100-e09c6d8e9062" />

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/e7c690d6-cec8-4560-b5c7-21a6a25b3104" />


#### Grup

Per crear un grup tornem a afegir entrada nova i triem posixGrup per afegir

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/730f6832-7774-4ffc-9ec5-91319e3390a7" />

Configurem el cn

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/8da78e62-262f-4027-8383-ee8c8ab8b1c3" />

i un gid de grup

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/2b818b0c-c857-4e45-9db5-88b79c204a30" />

Es crea correctament

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/ab55cbf5-b847-4362-b3b1-d420cb755727" />


#### Usuari

Per crear un usuari al afegir entrada nova afegim inetOrgPerson i posixAccount per poder vincular l'usuari a un grup

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/966e5995-5b0d-4ff9-8ca2-572bd4fa608b" />


Afegim el uid del usuari i el de grup, que coinicdeixi amb el que tenim creat

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/49bcbf6b-4d01-4031-9fa6-c8441619a5f5" />


Acabem d'afegir mes informacio com el directori de home 

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/9c102786-4e07-44cc-8f13-bf208e942810" />

Resultat final creat

<img width="962" height="743" alt="Captura de pantalla de 2026-01-20 13-10-10" src="https://github.com/user-attachments/assets/7fabd410-321e-4252-8b8b-5208c4f197ee" />


