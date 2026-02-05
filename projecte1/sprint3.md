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


## 2. Proves LDAP

### Reconfiguracio

Netejem la bd de ldap per fer noves proves

<img width="727" height="136" alt="Captura de pantalla de 2026-01-27 10-36-38" src="https://github.com/user-attachments/assets/dad5c42e-11d2-4f9d-83ec-19f94f608dfe" />


Borrem la base de dades anterior

<img width="724" height="435" alt="Captura de pantalla de 2026-01-27 10-35-51" src="https://github.com/user-attachments/assets/341519b1-d338-4a53-86e9-c4f44cf9f3d3" />


Comprovem en un slapcat

<img width="491" height="294" alt="Captura de pantalla de 2026-01-27 10-36-26" src="https://github.com/user-attachments/assets/e8771507-fee9-4fff-b51d-b716329c683d" />


Ens descarregem un fitxer de dades de prova

<img width="412" height="73" alt="Captura de pantalla de 2026-01-27 10-53-12" src="https://github.com/user-attachments/assets/3dafb766-f987-4019-9203-c88bb2cce75f" />


I modifiquem els dn per que sigue el nostre

<img width="700" height="541" alt="Captura de pantalla de 2026-01-27 10-56-28" src="https://github.com/user-attachments/assets/0dac397f-b44b-4517-ac9e-f70fbb627fdd" />


<img width="700" height="541" alt="Captura de pantalla de 2026-01-27 10-56-39" src="https://github.com/user-attachments/assets/535ef68d-b961-4519-b181-d96a13e9ddf8" />


<img width="700" height="541" alt="Captura de pantalla de 2026-01-27 10-56-53" src="https://github.com/user-attachments/assets/f3bfe396-abf5-4c29-b55f-1dd2763f3515" />


En un ldapadd afegim les entrades

<img width="743" height="318" alt="Captura de pantalla de 2026-01-27 12-00-45" src="https://github.com/user-attachments/assets/a7f451cc-ec8b-4ec8-9dbc-6af84250cd00" />


Comprovem de nou en slapcat que ara tenim informacio

<img width="555" height="700" alt="Captura de pantalla de 2026-01-27 12-01-22" src="https://github.com/user-attachments/assets/b2c11432-9364-463e-8974-e226a8decbde" />


### Proves

1. 

Comencem afegint un nou usuari a partir d'un fitxer ldif modificat com una entrada normal

<img width="568" height="26" alt="Captura de pantalla de 2026-01-27 12-08-56" src="https://github.com/user-attachments/assets/32c31104-dca5-4c7c-8993-f62772f717e9" />


<img width="358" height="284" alt="Captura de pantalla de 2026-01-27 12-07-20" src="https://github.com/user-attachments/assets/c72e0310-185c-43c5-8e3b-9cde650fece4" />


I amb ldapadd el podem afegir

<img width="956" height="74" alt="Captura de pantalla de 2026-01-27 12-07-54" src="https://github.com/user-attachments/assets/2223e6ae-ea50-488b-8419-2c4946c746b3" />


El podem buscar amb ldapsearch amb el parametre de la uid

<img width="825" height="272" alt="Captura de pantalla de 2026-01-27 12-10-27" src="https://github.com/user-attachments/assets/4d59b2a6-55c1-4f6e-9489-615e8e675abd" />



2.

Ara afegirem de la mateixa manera una nova uo

Creem primer l'entrada al fitxer

<img width="321" height="111" alt="image" src="https://github.com/user-attachments/assets/dfed1401-ca24-4d32-b366-48071835b93a" />


I l'afegim amb ldapadd

<img width="935" height="77" alt="Captura de pantalla de 2026-01-27 12-13-00" src="https://github.com/user-attachments/assets/5bea62cc-cf3a-421d-9be2-cc8b615d3c09" />


Comprovem buscant amb ldapsearch amb el parametre de "ou=nomines"

<img width="823" height="108" alt="Captura de pantalla de 2026-01-27 12-13-37" src="https://github.com/user-attachments/assets/815abd00-3fe3-46a9-a27a-29055b88f842" />



3.

Per afegir l'usuari que em creat a la ou que em creat utilitzarem changetype modify per remplaçar la ou al fitxer ldif

<img width="360" height="104" alt="Captura de pantalla de 2026-01-27 12-20-45" src="https://github.com/user-attachments/assets/934d049d-6df0-4e55-b2cb-af7db56d73cb" />


Despres executem ldapmodify sobre el fitxer

<img width="973" height="76" alt="Captura de pantalla de 2026-01-27 12-18-51" src="https://github.com/user-attachments/assets/aff54be6-e2d3-4e00-a3f2-6b1438309074" />


I si comprobem tot i que al dn seguiex apareixen la ou rrhh que ja tenia tambe apareix la nova 

<img width="819" height="380" alt="Captura de pantalla de 2026-01-27 12-20-00" src="https://github.com/user-attachments/assets/67d63bdd-a09f-4a8f-a9f2-07717776a38b" />



4.

Podem buscar tots els grups que hi ha utilitzant el parametre "objectClass=posixGroup" al ldapsearch, en aquest cas son dos informatica i administracio

<img width="939" height="284" alt="Captura de pantalla de 2026-01-27 12-24-26" src="https://github.com/user-attachments/assets/490cc494-e814-4cd8-ae35-300a56a56d4c" />



5.

Per afegir l'usuari Alu1 al grup d'informatica modifiquem el fitxer ldif sobre el grup, no l'usuari, i amb changetype modify indiquem l'uid del usuari com a "memberuid" per a que sigui un grup secundari

<img width="475" height="99" alt="image" src="https://github.com/user-attachments/assets/417c0baa-679d-47fd-9e1f-b14fdb0aad61" />


apliquem els canvis

<img width="739" height="94" alt="image" src="https://github.com/user-attachments/assets/4bf2f6d8-455a-4be0-adf8-9a562c207831" />


I comprovem en ldapsearch filtrant per el grup que apareix la uid del usuari

<img width="734" height="198" alt="image" src="https://github.com/user-attachments/assets/fa03ce9c-3018-438b-8c05-927ba8586c79" />



6.

Ara podem fer dos modificacions a la vegada des del mateix fitxer que s'executen a la mateixa comanda ja que son dos changetype modify i separem cada parametre amb una linia i un guio "-"

Aqui afegim un atribut opcional com l'email i modifiquem el cognom

<img width="389" height="164" alt="Captura de pantalla de 2026-01-27 12-38-26" src="https://github.com/user-attachments/assets/de970db6-8003-48c3-bf6b-d1ce9a25673b" />


Executem una sola comada per realitzar els dos canvis

<img width="961" height="84" alt="Captura de pantalla de 2026-01-27 12-38-53" src="https://github.com/user-attachments/assets/fb9e62c0-3de9-4a7f-8ccb-bfc4683c80aa" />


I comprovem filtrant per la uid del usuari que els dos canvis s'han fet correctament

<img width="803" height="291" alt="Captura de pantalla de 2026-01-27 12-39-22" src="https://github.com/user-attachments/assets/66d63b03-d797-43cc-8cfc-1da41061c7eb" />



7.

Podem buscar quins usuaris hi ha a una uo concreta afegint la ou al dn i despres buscant unicamnent uids per buscar usuaris 

En aquest cas hi ha quatre usuaris

<img width="833" height="280" alt="Captura de pantalla de 2026-01-27 12-40-38" src="https://github.com/user-attachments/assets/5b16f729-94f7-45fa-955c-ed45c4f70ce0" />



8.

Si provem d'eliminar un atribut obligatori com el gidnumber d'un grup ens dona l'error de que es un atribut obligatori per tant primer eliminiem l'atribut "posixGroup" 
i el modificarem per un tipus de grups logics en "groupOfNames"


i despres ja podem eliminar l'atribut gidnumber 

(se podra hacer todo de un doc i de un comando de una? mejor si si)

(probar esto)
<img width="482" height="85" alt="Captura de pantalla de 2026-01-27 12-44-00" src="https://github.com/user-attachments/assets/b3395c60-970b-4199-bbe5-fa7c63ba4858" />

<img width="1005" height="117" alt="Captura de pantalla de 2026-01-27 12-44-37" src="https://github.com/user-attachments/assets/35336c9e-6b08-4aa3-9951-d1c3f394c11a" />



9.

Per buscar cuantes uo hi ha al nostre ldap podem buscar per object class de tipo "organizationalUnit" i veiem que en el nostre cas ni ha tres

<img width="988" height="291" alt="Captura de pantalla de 2026-01-27 12-49-49" src="https://github.com/user-attachments/assets/a76e599d-c132-44b9-b1a1-a2fd3e00af4d" />

comando found que "cuenta" las entradas:
ldapsearch -xLLL -b "dc=gina,dc=cat" dn | grep -c "^dn:"



10.

Per modificar un cn i dn principals utilitzem el changetype "modrdn" i podrem modificar el cn primer i despres eliminarem el dn antic i l'indicarem de nou sense el cn antic

<img width="359" height="121" alt="Captura de pantalla de 2026-01-27 12-53-13" src="https://github.com/user-attachments/assets/11922d55-54cd-476d-b03f-4260f7d1b182" />


Per realitzar els canvis utlitzem ldapmodify 

<img width="986" height="77" alt="Captura de pantalla de 2026-01-27 12-56-53" src="https://github.com/user-attachments/assets/abcbefcd-e7a0-4228-b3fc-ffc6f79671ea" />


Si busquem per en seu antic cn no trobem cap resultat

<img width="805" height="42" alt="Captura de pantalla de 2026-01-27 12-57-57" src="https://github.com/user-attachments/assets/e3d1e538-d776-492d-949c-9bebc0fa5578" />


En canvi si busquem per la uid, que no esta modificada veiem els canvis

<img width="828" height="282" alt="Captura de pantalla de 2026-01-27 12-57-42" src="https://github.com/user-attachments/assets/b009a054-0311-43ac-81fd-24044ba96020" />



11. revisar? alomejor si hago los cambios de lo de alu1 tmb cambio esto?

Per eliminar una uo que te usuaris que forment part primer em d'eliminar aquests usuaris de la uo

<img width="367" height="104" alt="Captura de pantalla de 2026-01-27 13-03-09" src="https://github.com/user-attachments/assets/88be28c2-dc94-466d-b33c-909f0d486ed8" />

<img width="991" height="77" alt="Captura de pantalla de 2026-01-27 13-02-15" src="https://github.com/user-attachments/assets/ac70dbbc-9f2b-402b-91ed-b4661cd2711f" />


Despres amb "ldapdelete" podem directament eliminar la ou amb el seu dn

<img width="1054" height="49" alt="Captura de pantalla de 2026-01-27 13-03-38" src="https://github.com/user-attachments/assets/85331d82-c0a6-4fc4-9dc7-c2f29cc162bc" />


Ja no existeix

<img width="811" height="39" alt="Captura de pantalla de 2026-01-27 13-04-10" src="https://github.com/user-attachments/assets/1536ba99-f09b-4a40-b3d9-9f9f91731970" />




12.

Pod
(aqui solo habia buscado por el cn del grupo i no es eso a partir del grupo sacas la gidnumber i luego buscas los users que tengan ese gid, los que tienen gid son grupo principal
los que tienen memberid son secundarios)

esto es lo q tenia

<img width="883" height="166" alt="Captura de pantalla de 2026-01-27 13-24-04" src="https://github.com/user-attachments/assets/127f212d-9c73-47e7-ad76-558a3a4e0abf" />



13.

Per buscar un usuari concret del que sabem la seva uid unicament hem de buscar com a parametre "uid=1002"

<img width="870" height="271" alt="Captura de pantalla de 2026-01-27 13-06-12" src="https://github.com/user-attachments/assets/62fb4353-aa6a-400d-8735-12009639bfa7" />


14.

obtenim unicament a Alu1
parametre “(&(uidNumber>=1003)(sn=R*))”
utilitzem & per que hagui de cumplir els dos parametres

<img width="990" height="269" alt="Captura de pantalla de 2026-01-27 13-10-10" src="https://github.com/user-attachments/assets/127ac345-cf8c-4dac-8a2f-7edb2c624f84" />



15.

objectClass=posixAccount “(|(gidNumber=1001)(sn=Pallares))” dn uid cn sn gidNumber
utilitzem “|” per que nomes tingui que cumplir un parametre o el altre
el resultat son dos usuaris del grup informatica i un usuari en cognom pallares

<img width="1205" height="370" alt="Captura de pantalla de 2026-01-27 13-17-40" src="https://github.com/user-attachments/assets/1946ae4c-80b6-44ea-903c-998740f9918e" />





## 3. Servidor Samba

### Part Servidor

Previament a instalar el samba configurarem una serie de carpetes i usuaris per proves 

Creem tres usuaris amb "useradd" i no amb "adduser" per que no es creen en configuracions de home,login,altres per defecte i afegim el parametre /sbin/nologin 

Tambe crearem un grup per ficar alguns dels usuaris per comprovar diferents permisos

Despres afegim dos dels usuaris al grup i podem comprovar que s'han creat en un cat del fitxer /etc/passwd

<img width="502" height="396" alt="Captura de pantalla de 2026-01-29 12-50-51" src="https://github.com/user-attachments/assets/a218de75-ff63-4acb-b1fc-e4bfa67c5d49" />


Configurem una contrasenya per cada usuari

<img width="387" height="253" alt="Captura de pantalla de 2026-01-29 13-12-29" src="https://github.com/user-attachments/assets/24ed3cea-8fb2-4df0-99b2-36fcb820f070" />


Creem una carpeta amb tots el permisos i cap usuari ni grup propietari

<img width="646" height="145" alt="Captura de pantalla de 2026-01-29 12-47-55" src="https://github.com/user-attachments/assets/13012311-ee89-4680-b3cd-de97176f2621" />


Per instalar Samba al servidor unicament instalem el paquet "samba" amb "apt install samba"

<img width="647" height="173" alt="Captura de pantalla de 2026-01-29 12-45-13" src="https://github.com/user-attachments/assets/3c0a1406-f458-499f-9041-9eb149b1cbec" />


Ara modifiquem el fitxer smb.conf i afegim els permisos que creguem necessaris per els diferents usuaris o grups

<img width="502" height="396" alt="Captura de pantalla de 2026-01-29 12-56-16" src="https://github.com/user-attachments/assets/231c2683-e223-4a39-8354-44fd3c8df6ef" />


Reiniciem el servei samba per aplicar els canvis

<img width="478" height="55" alt="Captura de pantalla de 2026-01-29 12-58-09" src="https://github.com/user-attachments/assets/6605709c-6c07-49f4-8da8-4ec0ce73e564" />


Per ultim comprovem que el servei esta actiu correctament 

<img width="620" height="474" alt="Captura de pantalla de 2026-01-29 12-58-47" src="https://github.com/user-attachments/assets/e3b37d79-425e-4b8f-9b9d-e761d0175948" />




### Part Client

Per la part client l'unic que em de fer es amb "apt install" instalar el paquet "smbclient"

<img width="813" height="290" alt="Captura de pantalla de 2026-01-29 13-05-39" src="https://github.com/user-attachments/assets/de8414bf-98af-483b-80b3-b43f1989a9cb" />


Despres ja des del gestor de fitxers propi d'ubuntu podem accedir a conectar amb altres i li pasem el servei samba, la ip del servidor i la carpeta compartida

<img width="601" height="80" alt="Captura de pantalla de 2026-01-29 13-10-50" src="https://github.com/user-attachments/assets/8850efe0-c99a-43d5-88df-96cd34c5657a" />


Si provem a conectar com invitat, segons la configuracio mostrada anteriorment, podem conectar i crear contingut

(cap)


Si entrem amb l'usuari naim, igualment pot entrar i crear (comprov)

<img width="497" height="439" alt="Captura de pantalla de 2026-01-29 13-13-40" src="https://github.com/user-attachments/assets/39b1d2d8-aac5-4c58-97b7-d8ee48eb2a15" />

<img width="525" height="209" alt="Captura de pantalla de 2026-01-29 13-09-53" src="https://github.com/user-attachments/assets/bf4c1035-b7ff-4ca3-962d-80832b22f4e5" />


En canvi si entrem en l'usuari edgar, pot entrar pero no crear

<img width="497" height="439" alt="Captura de pantalla de 2026-01-29 13-14-21" src="https://github.com/user-attachments/assets/bcc93dcc-1f04-4331-a201-2095341ccab5" />

<img width="606" height="219" alt="Captura de pantalla de 2026-01-29 13-15-28" src="https://github.com/user-attachments/assets/42808178-73a8-4852-a032-136fb48b0208" />
