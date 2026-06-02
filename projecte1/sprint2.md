---
layout: default
title: "Sprint 2. Instal·lació, Configuració de Programari de Base i Gestió de Fitxers"
permalink: projecte1/sprint2/
---

## 1. Sistemes de fitxers i particions

A Ubuntu, les particions i els sistemes de fitxers són essencials per organitzar i gestionar l'emmagatzematge. Les particions divideixen el disc en espais independents, mentre que els sistemes de fitxers permeten emmagatzemar i accedir a la informació de manera eficient.

  Particions i volums

		Partició: fragment físic d’un disc.

		Volum: agrupació lògica de particions o discos, que permet unificar espai de diversos discos sota una sola unitat virtual.


  Mida de sector
	    
		Unitat mínima física del disc per guardar dades.
	    
		Normalment: 512 bytes i no es modificable

  Mida de bloc
	
		 Unitat mínima lògica que utilitza el sistema operatiu per gestionar les dades.
    
    	 Per defecte: 4 KB (4096 bytes), però es pot modificar durant la formatació.
    
     	 Cada partició pot tenir una mida de bloc diferent segons el sistema de fitxers.

		 Podem comprovar que la mida de bloc per defecte d'una particio d'un disc es 4096 amb la comanda seguent

<img width="549" height="83" alt="image" src="https://github.com/user-attachments/assets/46e92f62-08dd-4b81-b67e-6030d8113f30" />

		 Si volem modificar la mida de bloc, amb la particio no montada executem aquesta comanda amb la nova mida

<img width="549" height="83" alt="image" src="https://github.com/user-attachments/assets/42e367f8-066b-4ba9-9614-ef1b211f4023" />

		 tornem a comprovar la mida i veiem que s'ha modificat correctament

<img width="544" height="86" alt="image" src="https://github.com/user-attachments/assets/486b16d1-f9a9-4096-baca-700d72927d49" />


  Fragmentació

    	 Interna (lògica): pèrdua d’espai per blocs massa grans o petits.
    
		 Externa (física): fitxers separats en diferents blocs del disc, reduint el rendiment.

		 Podem comprovar si la nostra particio de dades necessita desframentacio amb la comanda e4defrag

<img width="654" height="317" alt="image" src="https://github.com/user-attachments/assets/3bc8211a-b935-4d01-abcb-efbabc67fa40" />


  Tipus de formatació
    
		 Formatació d’alt nivell: crea o reinicia el sistema de fitxers però manté el contingut.
    
		 Formatació de baix nivell: esborra completament el contingut, repara errors físics i crea de nou la estructura de sectors. Es fa amb eines especialitzades.
    
		 Formatació de nivell mitjà: recrea el sistema de fitxers però només marca els blocs defectuosos, no els repara.

  Gestió de particions

		 Eines com GParted o línies d’ordres (fdisk, parted) permeten:
    
    	 Crear, esborrar i redimensionar particions.
    
		 Assignar sistemes de fitxers diferents.
    
		 Comprovar l’estat dels blocs i sectors.


## 2. Gestio d'usuaris, grups i permisos

### Gestio d'usuaris i grups

Un usuari dins d'un equip es una entitat que representa normalment a una unica persona i que s'idenitfica per un nom i uid.

Un grup es un conjunt d'usuaris agrupats per que comparteixen permisos.

La gestió d'usuaris i grups a Linux es basa principalment en quatre fitxers del sistema, ubicats a /etc, que emmagatzemen la informació essencial per identificar usuaris, assignar-los a grups i controlar l'accés al sistema.

	/etc/passwd
		Conté la informació bàsica de cada usuari: nom dusuari, UID, GID principal, directori home i shell. 		Les contrasenyes ja no es guarden aquí per seguretat.

	/etc/shadow
		Deseu les contrasenyes xifrades dels usuaris, juntament amb paràmetres com la caducitat, el temps mínim entre canvis i polítiques de seguretat de la contrasenya.

	/etc/group
		Emmagatzema els grups del sistema, assignant un GID a cadascun i llistant els usuaris que pertanyen a grups secundaris.

	/etc/gshadow
		Conté les contrasenyes dels grups (si n'hi ha), així com els administradors i els membres amb permisos especials dins d'aquests grups.


Per modificar el contingut d'aquests fitxers, o per modificar algun parametre d'usuaris, grups, contrasenyes, no hem de modificar directament el contingut dels fitxers, sino utilitzar comandes, ja que podem provocar errors de sintaxi o corrupcio.

Algunes comandes basiques per crear o modificar usaris son:
		
		> Crear usuaris o grups:
		
		'adduser' per crear un usuari de manera automatica, unicament introduim el nom de l'usuari i la password al moment i ens crea la carpeta home i els permisos automaticament.

<img width="741" height="319" alt="Captura de pantalla de 2026-06-01 17-37-37" src="https://github.com/user-attachments/assets/f1c7cc16-2e89-453e-8f46-f4726c3e52ed" />

		`useradd` s'utilitza tambe per crear usuaris pero de manera manual, despres de crearlo hem de configurarli la contrasenya, la home i si volem tambe el shell ja que no ve en bash per defecte.

		Primer creem l'usuari, li assignem una password i creem la carpeta home amb el mateix nom
		
<img width="518" height="151" alt="Captura de pantalla de 2026-06-01 17-43-23" src="https://github.com/user-attachments/assets/94adb86b-bf13-419f-ae8d-34122a19578d" />

		Despres assegurem permisos fent propietari de la home al usuari
		
<img width="523" height="138" alt="Captura de pantalla de 2026-06-01 17-43-36" src="https://github.com/user-attachments/assets/03ecb5b4-46b6-4c03-808d-d8c0acd30f7d" />

		Per ultim com en useradd el shell que ve per defecte es sh podem canviarlo a bash
		
<img width="573" height="108" alt="Captura de pantalla de 2026-06-01 18-07-57" src="https://github.com/user-attachments/assets/39dbc151-2fe6-48b3-9c71-3436d3bf6202" />

		'addgroup' serveix per crear un grup. 

<img width="413" height="77" alt="Captura de pantalla de 2026-06-01 17-43-01" src="https://github.com/user-attachments/assets/30709e91-029b-4445-ac69-b99fd3176ef8" />


		> Modificar usuaris, grups o contraseñes:

		'usermod' permet modifcar usuaris per exemple per bloquejarlos. Podem comprovar que un usuari esta bloquejat si al shadow apareix el simbol "!".

		Per bloquejar utilitzem -L i per desbloquejar -U

<img width="515" height="102" alt="Captura de pantalla de 2026-06-01 17-46-12" src="https://github.com/user-attachments/assets/750d3874-a8e4-42eb-9edc-d40539c3598a" />

<img width="576" height="77" alt="Captura de pantalla de 2026-06-01 17-47-26" src="https://github.com/user-attachments/assets/4b62f046-8ff8-414f-8973-ff5f7cdde1b5" />


		'groupmod' permet modificar un grup, per exemple canviarli el nom

<img width="515" height="102" alt="Captura de pantalla de 2026-06-01 17-45-02" src="https://github.com/user-attachments/assets/0a2fe4e2-96c5-4724-a9be-e9d39cb9c4a2" />

		'change' permet afegir una caducitat a les contrasenyes
		

		> Eliminar usuaris o grups:

		'userdel'

		'deluser'

		'groupdel'


		> Afegir un usuari a un grup:

		'adduser usuari grup'

		'gpasswd -a usuari grup' (afegig user grup com secundari tipo apend) (-A hace al user admin de ese grupo)

<img width="487" height="53" alt="Captura de pantalla de 2026-06-01 17-47-55" src="https://github.com/user-attachments/assets/3b0683d8-d054-47a8-8d67-806457edd94a" />

		'usermod -a -G grup usuari' (-a lo mismo i la -G es para modif el grupo principal del user q de primeras es el q se crea auto igual q el nombre del usu)


		> Modifiquem el nom d'usuari funcionalment:
		
		'usermod -l' (nounom anticnom) per canviar l'user

<img width="508" height="33" alt="Captura de pantalla de 2026-06-01 18-24-13" src="https://github.com/user-attachments/assets/2ed63e25-a535-4782-920d-66551011b2b4" />

		canviar nom de carpeta home mv /home/ant ''/nou

<img width="431" height="110" alt="Captura de pantalla de 2026-06-01 18-24-36" src="https://github.com/user-attachments/assets/234fba68-dd4c-48ef-99c7-dffc53074595" />

		usermod -d /home/nou per a q la home del user sigui la nova 

<img width="546" height="32" alt="Captura de pantalla de 2026-06-01 18-25-37" src="https://github.com/user-attachments/assets/0c2955f5-9516-460e-bc1d-1c3018256120" />

		groupmod -n nounom anti canvia el nom del grup del user

<img width="492" height="30" alt="Captura de pantalla de 2026-06-01 18-27-58" src="https://github.com/user-attachments/assets/37131f4b-a93c-420b-9a39-120cb5317ffa" />

		comprov rapid de id, cat passwd, group que estan correct 

<img width="903" height="267" alt="Captura de pantalla de 2026-06-01 18-28-07" src="https://github.com/user-attachments/assets/bcdcf62c-d1bd-4882-a480-6896a007f7f4" />

		iniciar grafico con el user (deveria func)

<img width="360" height="263" alt="Captura de pantalla de 2026-06-01 18-29-16" src="https://github.com/user-attachments/assets/59d28481-d6f8-4a90-8189-920c876dc39e" />

		abrir term i poner whoaim para la cap

<img width="473" height="97" alt="Captura de pantalla de 2026-06-01 18-31-40" src="https://github.com/user-attachments/assets/bc0fcadb-874b-40d3-b96d-26b25bb2759d" />



### Fitxers de Configuracio 

A la carpeta etc/skel conte tres fitxers de configuracio d'usuari: bashrc, bash_logout i profile

Bashrc serveix principalment per definir el contingut de la shell, com alies, variables d'entorn o personalitzacio

Bash_logout s'executa cuan es tanca una sessio activa de shell 

Profile definiex l'inici de sessio i podem definir variables d'entorn o procesos que s'han d'executar al iniciar

Adduser i useradd copien el contigut d'/etc/skel al home d'un usuari nou, si modifiquem aquests fitxers podem fer que els usuaris que es creen despres tinguin aquesta configuracio per defecte, mes efectiu que tenir que modificar cada usuari despres de crearlo. Igualment si afegim algun fitxer o carpeta al skel es copiaran als nous usuaris sense tenir que indicarho a cap fitxer.

En cas de que vulgem modificar la configuracio d'un usuari ja creat es creen els mateixos fitxers dins la carpeta home de cada usuari, per tan els podem modificar desde alli.

Tambe podem modificar el que fan les comandes adduser i user add desde "/etc/adduser.conf" i "/etc/default/useradd", pugent modificar coses com el directori de homes per defecte, les uids utilitzades, la shell que tindra l'user,etc. La diferencia principal entre adduser i useradd es que 'adduser' esta mes automatizada, et demana la password cuan crees l'usuari i crea la carpeta al home, mentre que en useradd tots aquests pasos s'han de fer manualment.

Per ultim tenim el fitxer login.defs que el que fa es definir principalment configuracions relacionades en la gestio d'usuaris, com els rangs d'uid que utilitzaran, els limits de temps de contrasenyes, entre altres. 


Prova practica

Podem modificar algun petit parametre de cada fitxer i veure com afecta al final en la creacio de nous usuaris

El primer que podem fer es afegir un directori a /etc/skel per veure com es copia a la home del user

<img width="426" height="73" alt="Captura de pantalla de 2026-06-01 21-56-48" src="https://github.com/user-attachments/assets/dee9c88a-8d3c-450d-8f30-ad24a9d7f18b" />

A adduser modificarem la uid minima i canviarem els permisos de la carpeta home
	
	Cambiem la uid de 1000 a 1500

<img width="248" height="145" alt="Captura de pantalla de 2026-06-01 21-58-19" src="https://github.com/user-attachments/assets/75e3819c-e81f-4f4f-98c4-bfbcae8dcf7c" />

	Cambiem els permisos de la carpeta home de 750 a 755 (rwxr-xr-x)
	
<img width="162" height="72" alt="Captura de pantalla de 2026-06-01 21-58-57" src="https://github.com/user-attachments/assets/b14689a5-1051-482e-a1e8-e9eb2ca7e3d3" />

	Cambiem on es creen per defecte les homes a /mnt
	
<img width="373" height="74" alt="Captura de pantalla de 2026-06-01 21-59-32" src="https://github.com/user-attachments/assets/92d890b6-0f4b-4b45-9157-98c61e7eaa91" />

A useradd canviarem la shell per defecte a bash 

<img width="174" height="55" alt="Captura de pantalla de 2026-06-01 22-00-09" src="https://github.com/user-attachments/assets/634bfb40-7d78-4836-9cb0-2b0c5fb20ba2" />

A logins.def modificarem la data de caducitat de les contrasenyes a 31 dies i l'uid minim que tindran els users

<img width="234" height="104" alt="Captura de pantalla de 2026-06-01 22-03-40" src="https://github.com/user-attachments/assets/8f174fda-5aa1-4897-83bb-3ad22eb6d3ba" />

<img width="292" height="87" alt="Captura de pantalla de 2026-06-01 22-04-12" src="https://github.com/user-attachments/assets/e5fb4319-6f20-43e4-9645-64a2f3823134" />

A bashrc podem crear un alias nou

<img width="182" height="53" alt="Captura de pantalla de 2026-06-01 22-08-17" src="https://github.com/user-attachments/assets/07d437ec-58bb-41d4-b3a7-20e553fbbb7e" />

A bash_logout indicarem que es borri el contingut de la carpeta temporal, afegirem un misatge de tancat i registrarem en un log la data de cada cop que tanquem sessio.

<img width="597" height="286" alt="Captura de pantalla de 2026-06-01 22-07-25" src="https://github.com/user-attachments/assets/e62f38d5-57f6-42c4-be94-da42477fd25f" />

Per ultim, profile podem crear un missatge de benvinguda

<img width="256" height="56" alt="Captura de pantalla de 2026-06-01 22-09-13" src="https://github.com/user-attachments/assets/20c90b7c-0b57-4b3e-a31e-456ca0e69479" />


Per comprovar que els canvis funcionen primer crearem un nou usuari en useradd, al fitxer passwd podem comprovar que l'uid es correcte i que el directori de la home tambe, al fitxer shadow a mes podem comprovar la caducitat de la contrasenya on el 31 son els dies que tarda en caducar i el 7 els dies en antelacio que avise.

<img width="724" height="112" alt="Captura de pantalla de 2026-06-01 22-17-17" src="https://github.com/user-attachments/assets/bc71fbd6-711c-4862-a4a2-a0bc3c72c3fb" />

Tambe podem comprovar que s'han copiat els fitxers del etc/skel, incluit el directori que em creat

<img width="454" height="124" alt="Captura de pantalla de 2026-06-01 22-17-27" src="https://github.com/user-attachments/assets/02e29786-6187-4c65-b499-daa09a0cb648" />

Si iniciem un bash en l'usuari podem crear la carpeta temporal i crear algun fitxer dins

Tanquem la sessio del bash i comprovem que el contingut s'ha borrat


Despres podem crear un nou usuari pero en useradd i comprovar al passwd que igualment la id es correcta, que el bash tambe s'ha canviat i al shadow la caducitat de la contrasenya. 

<img width="555" height="127" alt="Captura de pantalla de 2026-06-01 22-18-01" src="https://github.com/user-attachments/assets/4748a12d-19d2-4530-b612-5b01c5889c6f" />

<img width="728" height="115" alt="Captura de pantalla de 2026-06-01 22-18-28" src="https://github.com/user-attachments/assets/2f6596e6-7234-4102-a2b0-0e9d3843e928" />


### Gestio de permisos
A Ubuntu, els permisos són un mecanisme de seguretat que determina quins usuaris poden llegir, modificar o executar fitxers i directoris. Cada fitxer o directori té un propietari, un grup associat i un conjunt de permisos que controlen les accions que es poden realitzar sobre ell.

**UGO (user,group,other)**
Els permisos tradicionals es basen en tres categories d'usuaris:

User (u): propietari del fitxer o directori.
Group (g): grup propietari del fitxer o directori.
Others (o): qualsevol altre usuari del sistema.

Per a cadascuna d'aquestes categories es poden assignar tres permisos bàsics:

r (read): lectura.
w (write): escriptura.
x (execute): execució.

Per exemple, si executem "ls -l proves/" obtenim les tres primeres lletres son del propietari, les tres seguents del grup propietari, i els tres ultims de la resta en este cas l'usari propietari pot llegir,escriur i executar i el grup propietar i la resta poden llegir i executar (pero no escriure)

<img width="513" height="273" alt="Captura de pantalla de 2026-06-01 22-35-09" src="https://github.com/user-attachments/assets/547859e7-43a0-4029-bb3b-8110f481f81e" />


**Permisos especials**

A més dels permisos tradicionals, ubuntu disposa de tres permisos especials.

	SUID (Set User ID)

Quan un executable té aquest bit activat, s'executa amb els privilegis del propietari del fitxer.

Podem comprovar que el programa passwd te el bit activat i per tant una "s" esta sustituint la "x" del usuari

<img width="547" height="52" alt="Captura de pantalla de 2026-06-01 23-33-05" src="https://github.com/user-attachments/assets/2ae792de-4f4e-4329-87d4-e13fab3ecfde" />

Per assignar esta flag a cualsevol programa utilitzem "chmod u+s programa"


	SGID (Set Group ID)

En fitxers executables, el programa s'executa amb el grup propietari.

En directoris, els fitxers nous hereten el grup del directori.

Podem donarli aquest permis a proves en "chmod g+s proves" i veure com apareix la "s" al grup

<img width="516" height="239" alt="Captura de pantalla de 2026-06-01 23-34-31" src="https://github.com/user-attachments/assets/5127486c-9ca1-4355-8fd8-87bad2d807f9" />



	Sticky Bit

S'utilitza principalment en directoris compartits.

Permet que només el propietari d'un fitxer (o root) pugui esborrar-lo, encara que altres usuaris tinguin permisos d'escriptura sobre el directori.

Comprovem que /tmp te aquest permis indicat en una "t"

<img width="458" height="64" alt="Captura de pantalla de 2026-06-01 23-35-00" src="https://github.com/user-attachments/assets/92fd076e-4a83-4898-80f1-6b0cf5d829c1" />

Per assignarlo utilitzem +t al chmod


**ACL (Access Control Lists)**

Les ACL permeten definir permisos més detallats que el model UGO tradicional, per exemple, podem voler donar permisos a un usuari concret sense canviar el propietari ni el grup.

Per veure les ACL d'un directori usem "getfacl proves/"

<img width="504" height="143" alt="Captura de pantalla de 2026-06-01 22-36-36" src="https://github.com/user-attachments/assets/88eed98f-3f46-435b-ba51-ab6ae5a53013" />


> Configurar ACL

Donar permisos complets a l'usuari user1:

setfacl -m u:user:rwx prova

Donar permisos de lectura a un grup:

setfacl -m g:asix2:r-- fitxer.txt

Eliminar una ACL:

<img width="595" height="222" alt="Captura de pantalla de 2026-06-01 23-37-25" src="https://github.com/user-attachments/assets/5405a42e-727b-48a6-80a7-0458e24c73e2" />



> ACL per defecte

També es poden definir ACL heredades per als fitxers nous creats dins d'un directori.

<img width="651" height="307" alt="Captura de pantalla de 2026-06-01 23-38-20" src="https://github.com/user-attachments/assets/cc4ace2e-86ef-4b11-baca-0f5339b843b4" />



**Umask**

La umask és una màscara que determina quins permisos es retiren per defecte quan es creen fitxers o directoris nous. Inicialment a ubuntu els fitxers tenen de mascara 666 i els directoris 777 i la umask per defecte es 022 per tant si restem la umask obtenim que els permisos reals dels fitxers seran 644(rw-r--r--) i dels directoris 755(rwxr-xr-x)

La umask es pot consultar desde terminal en "umask" i es pot modificar a bashrc


## 3. Copies de seguretat

Hi ha diferents tipus de còpies segons la quantitat de dades que es guarden i la relació amb còpies anteriors.

Còpia completa
Desa totes les dades seleccionades a cada execució. És l'opció més segura i senzilla de restaurar, encara que requereix més temps i espai d'emmagatzematge.

Còpia incremental
Només desa els canvis realitzats des de la darrera copia (completa o incremental). És ràpida i ocupa poc espai, però la restauració requereix còpia completa i totes les incrementals posteriors.

Còpia diferencial
Desa tots els canvis realitzats des de la darrera còpia completa. Ocupa més espai que la incremental, però és més senzilla de restaurar, ja que només en necessita la còpia completa i l'última diferencial.

En sistemes Linux hi ha diferents ordres de terminal per copiar informació, cadascun orientat a un nivell diferent de còpia i ús. 

	'cp' Copia fitxers i directoris a nivell de sistema de fitxers. És senzill i adequat per a còpies puntuals, però no està pensat per a còpies de seguretat ni per clonar discos.

	'rsync' Sincronitza fitxers i directoris copiant només els canvis realitzats. És eficient, conserva permisos i es fa servir habitualment per a còpies de seguretat i replicació de dades.

	'dd' Realitza còpies a nivell de bloc, clonant discos o particions de forma exacta. Inclou tot el contingut, fins i tot l'espai buit, i cal utilitzar-lo amb precaució.

Tambe existeixen opcions grafiques com deja-dup que podem instalar

<img width="714" height="147" alt="Captura de pantalla de 2025-12-18 09-28-57" src="https://github.com/user-attachments/assets/17a7defb-6388-45c1-a0a5-5cea2dfc252d" />

<img width="766" height="447" alt="Captura de pantalla de 2025-12-18 09-32-06" src="https://github.com/user-attachments/assets/9cc272c1-e95a-42a6-a6f3-b286573b2704" />



### Automatizacio amb scripts de les copies de seguretat

Podem automatizar el proces de crear una copia de seguretat amb scripts i eines com cron o anacron

Cron
Es fa servir per programar tasques en una data i hora concretes. Funciona únicament si el sistema està encès al moment programat, per la qual cosa és ideal per a tasques específiques i recurrents d'usuaris, com ara còpies de seguretat o execucions programades.

Les tasques de cron poden configurar-se de forma global al fitxer /etc/crontab, que afecta tots els usuaris, o de forma individual mitjançant l'ordre crontab per a cada usuari.

A més, al directori /etc/ hi ha carpetes com cron.daily, cron.weekly i cron.monthly, que faciliten l'execució automàtica de scripts segons la seva periodicitat.


Anacron
Permet executar tasques periòdiques (diàries, setmanals, mensuals), encara que el sistema estigui apagat en el moment previst. És especialment útil per a tasques de manteniment del sistema.


Prova practica

Primer creem un petit script indicant el bash, un timestamp de la data actual i un tar de la carpeta descarges

<img width="842" height="188" alt="Captura de pantalla de 2025-12-18 09-55-53" src="https://github.com/user-attachments/assets/f7da5dd7-dc41-4c21-a29f-a7993b792665" />


Si volem que l'script s'executi en un moment concret utilitzant crontab editem /etc/crontab i indiquem com es veu el minut i la hora, l'usuari que executa i la comanda que sera l'execucio de l'script

CAMBIARCAP

<img width="991" height="422" alt="Captura de pantalla de 2025-12-18 09-54-03" src="https://github.com/user-attachments/assets/908802b0-ce38-4e3a-abca-4a0d4f6d5183" />


Per automatitzar l'execucio diaria amb anacron copiarem l'script al directori /etc/cron.dialy sense l'extensio .sh i modificarem l'arxiu /etc/anacrontab per a que els cron diaris s'executin un minut despres d'enjegar la maquina

<img width="585" height="31" alt="Captura de pantalla de 2025-12-18 10-04-48" src="https://github.com/user-attachments/assets/bf3e269c-c0cc-4781-8ad3-d5f258380ec8" />

<img width="533" height="219" alt="Captura de pantalla de 2025-12-18 10-05-12" src="https://github.com/user-attachments/assets/87df67b6-d933-4641-a51b-cea5990e40a3" />

<img width="750" height="318" alt="Captura de pantalla de 2025-12-18 14-21-25" src="https://github.com/user-attachments/assets/1a0d5baf-c216-4b4d-a54d-c54aa1070555" />



## 4. Quotes de disc i d'usuari

A Ubuntu, les quotes de disc permeten limitar lespai demmagatzematge que pot utilitzar cada usuari o grup. Això ajuda a controlar lús del disc i evitar que un sol usuari ocupi tots els recursos disponibles del sistema.

Per configurar quotes en un disc primer amb la mv tancada afegirem un disc

<img width="422" height="282" alt="Captura de pantalla de 2026-06-01 16-24-38" src="https://github.com/user-attachments/assets/5f334bf1-ba06-4d8e-879e-0b39b77f0d7d" />

Despres instalarem el paquet quota en apt

<img width="742" height="275" alt="Captura de pantalla de 2026-06-01 04-26-57" src="https://github.com/user-attachments/assets/68fd3de8-c909-4b71-a403-63ed3a056147" />

Crearem una particio de tot el disc i la formatarem en ext4

<img width="567" height="223" alt="Captura de pantalla de 2026-06-01 16-33-51" src="https://github.com/user-attachments/assets/6de80e0b-f2b0-47b9-a463-96dde896c71b" />

<img width="589" height="220" alt="Captura de pantalla de 2026-06-01 04-38-38" src="https://github.com/user-attachments/assets/218c9690-dec0-4afa-8d21-f8693b79fb89" />

Creem una carpeta de proves

<img width="390" height="44" alt="Captura de pantalla de 2026-06-01 16-33-22" src="https://github.com/user-attachments/assets/93974fe4-87ab-476b-b4be-90835e10fd22" />

Montem la particio a la carpeta que acabem de crear en fstab, donantli tambe permisos de quotes

<img width="718" height="279" alt="Captura de pantalla de 2026-06-01 16-35-40" src="https://github.com/user-attachments/assets/9123716b-1afc-4112-933b-ef45913f605a" />

Reiniciem la maquina i a la carpeta de proves esta montat correctament

<img width="371" height="71" alt="Captura de pantalla de 2026-06-01 16-40-49" src="https://github.com/user-attachments/assets/4d0a1fdc-f2f0-454c-a195-45969e32b7dd" />

Pasem a activar els fitxers de quota en quotacheck i activarles en quotaon

<img width="596" height="93" alt="Captura de pantalla de 2026-06-01 16-42-23" src="https://github.com/user-attachments/assets/ebbd3446-088d-4b56-b101-2b25d3ca73b9" />

Crearem un user de prova 

<img width="505" height="332" alt="Captura de pantalla de 2026-06-01 16-43-28" src="https://github.com/user-attachments/assets/04e3fa2b-a071-4ebb-ba2c-2a26734e67e4" />

Definim la quota soft i la hard (explicar diferencia?)

En edquota -u li asignem les quotes al usuari (-u user1)(s'obri learxiu este)

<img width="590" height="87" alt="Captura de pantalla de 2026-06-01 16-55-59" src="https://github.com/user-attachments/assets/8337c2e7-025c-4737-96c8-18b627264303" />

En repquota comprovem les cuotes de tots els usuaris al disc (repquota /dev/sdc1)

<img width="653" height="170" alt="Captura de pantalla de 2026-06-01 17-32-42" src="https://github.com/user-attachments/assets/751e1256-863e-41e5-9286-56030fe75091" />

En quota -u comprovem les quotes del usuari

<img width="746" height="89" alt="Captura de pantalla de 2026-06-01 17-30-59" src="https://github.com/user-attachments/assets/352f8ad6-5d73-41b9-a234-27b930c6f893" />


Podem provar que la quota funciona afegint fitxers i comprovem que mentres no superem el limit es creen sense problemes, pero que cuan el superem es creen buits

Creem el primer fitxer que pesa tota la mida que li hem assignat

<img width="745" height="104" alt="Captura de pantalla de 2026-06-01 17-30-51" src="https://github.com/user-attachments/assets/b9d95259-42e0-45b0-b2a9-a30ce0ee325f" />

En canvi cuan ja superem el soft i despres arribem al limit podem veure com es redueix la mida i finalment es crea buit

<img width="746" height="269" alt="Captura de pantalla de 2026-06-01 17-32-08" src="https://github.com/user-attachments/assets/3fa89377-96d8-41f2-99e5-8682014496da" />



