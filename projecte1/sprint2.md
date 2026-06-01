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
jjj
adduser i useradd utiltizen els fitxers de configuracio de /etc/skel al moment de crear un usuari, si modifiquem aquests fitxers podem fer que els usuaris que es creen despres tinguin aquesta configuracio per defecte, mes efectiu que tenir que modificar cada usuari despres de crearlo. Igualment si afegim algun fitxer o carpeta al skel es copiaran als nous usuaris sense tenir que indicarho a cap fitxer.

En cas de que vulgem modificar la configuracio d'un usuari ja creat es creen els mateixos fitxers dins la carpeta home de cada usuari, per tan els podem modificar desde alli.

Tambe podem modificar el que fan les comandes adduser i user add desde 
/etc/adduser.conf
/etc/default/useradd

fitx /etc/login.defs ??

Los tres fitxeros de etc skel son
explicar los bash i prof de skel
bash_logout tanca sesio
.bashrc interpret
.profile inici sesio


Exemplos de canvios de config: ?

Habilitar colores en el prompt
export LS_COLORS='di=1;34:ln=36:so=35:pi=33:ex=32:bd=1;33:cd=1;33:su=37:sg=30:tw=30:ow=34'
export EDITOR=nano
export HISTSIZE=2000
export HISTCONTROL=ignoredups:erasedups

Cambiar el bash por defecto(en los add), el uid(en los add), el temps contraseña(en login)

Para modificar els fitxers o contingut de la carpeta skel no podem ferho desde la terminal grafica, sino que hem d'utilitzar una tty nativa a la que podem entrar en Fn+Fx 

Modificar alguna cosa de cada fitx (bashrc,logout i prof)
al prf per exempe pdem fer que la home no es cree a /home si no a cualsevol altre dir (?) nosesiesaqui

En useradd conf podemos hacer qe se automatize
automatitzar useradd
en los fitxers q faig falta
primera vez q inicia gradficament  q te demano cambiar contra(posibilitat)
antes caldria un passwor per defecte (com 123) per evitar interaccio
q se cree la home i todo lo q haciamos manualmente
config utiles para cuando se execute el comando

practicas del sp pasado?
equivale a los ex 29 y 30
softlink hardlink
ln (-s es soft sesne es hard)
ln -s /tmp /etc/skel/enllas
nano etc login.defs (conf login i contrasenyes)

etc adduser.conf
(bash cambiat sh)
(home a /tmp)
cambiat lo de primer uid no 1000 cambiat a 2000
directori
etc skel

etc default useradd
sh per bash

etc profile
alias pwd = /var

esto es de lo q seria la act 31:
els fitxers .bash i profile no es modifiquen en pseudoterminal(la de grafica) S’han de fer ter tty
carpeta /etc/skel sense ocult no te res pero en ocult te els .prof i .bash que si es modifiquen aqui a partir del
proxim user es crearan amb la conf d’aqui i aixi no s’a de modificar indiv
si es crea algo a la carpeta skel (carpetes, archius lo q sea) es creara /copiara als nous users
pwd para saver en q carpeta estas
com que a la etc skel es per a tots els users se pot usar variables

jjj

modificaciones echas en skel bashrc bashlogout profile adduser useradd logindefs

1. carpeta skel añadimos carpeta prova per que es cree junt en la resta de fitxers al crear l'user
2.bashrc creem un alias per q el pugen usar los nous users
3.bash_logout borrar el contingut d'una carpeta temporal i missatge de sortida i/o log de tancat sessio
4.profile afegir missatge de benvinguda
5.adduser modifiquem uid i canviar permisos per defecte de la carpeta creada home
6.useradd modif shell per def (de sh a bash) i alguna cosa com el uid max min
7.logins modif la caducitat de les contrasenyes


2. alias ll='l -lah'
3.rm -rf "$HOME/temporal" /*  echo "Adeu!" echo "$(date) - $USER ha tancat la sessio" >> $HOME/logout.log
4.echo "Benvingut al shell"
5.canviar tal cual desde el nano (dir_mode=0700 a dir_mode=0750)
6.igual 5
7.canviar el pass_warn_age ens canvia els dies en antelacio a que caduca que ens avisa
canviar el pass_max_days canvia els dies maxims avans de tenir q canviar la pass
i el minim lo mismo
i si hi a algun parametre mes de este tipo pues canviar eso



### Gestio de permisos
ultimo dia hicimos permisos (777,rw,stiky…) hacer lo mismo q el año pasado

cosas de permisos q entran
ugo
especials
acl
mascara

permisos normals
permisos especials
llistes control access(acl)
umask

perm nomals
(en un ls -l)
3 primeres lletres sosn del user(propietari)(menos la q es realment primera q indica el tipus d per directori - per fitxer …)
los 3 despues son los q formen part del grup
i los ulktims tres son per nose los q no formen del grup ni son propiet (invitats, altres)
lo grup q apareix es sempre el principal del user propietari
chgrp per el grup
chmod per permisos
chown per propietari
r read w write x executar

permisos especials
sticky(util per 
suid(util per a scripts )
sgid(no utilitat segons profe)

s(suid)   z(guid)    t(stiky)

chmod 1(777) carpeta
777 representa los permisos q pondrias a esa carp archivo lo q sea q pueden ser 777 o lo q sea i el uno delante es para activar el sticky


apunts acl
getfacl carp/
dona un resumdls permisos
ls -l en un + indica acl defini

setfacl -m(-m per a idicar despues si es user o grup) user:nomuser:permisos a donar carp/ (captures en exemple)
setfacl -b carp/ (elimina les acl de la carp indicada)(totes de tots los users i tal)
setfacl -x user carp/ (elimina unicament les acl de un user)

apunts umask
sudo nano /etc/login.defs (umask)

directori->777 (111 111 111)
arxiu -> 666 (110 110 110)

/etc/login.devs -> umask 0022 = root
umask (num) - canvia la mascara temporalment(si reinicies se perd)

comenta utilitat mascara 

prova practica
per a les proves hem creat los de blau verd roig i groc el grup parchis i inicialment ara tenim los blau i verd al grup parchis pero lo groc i roig nop

pr al ub24 ha cambiat en lo 22 i per a coses de chown i noseq sobre un grup 
per a utilitzar chgrp i ficar un grup del q el user no forma part (parchis / groc) no se si sea por eso o q en general pero para eso necesita sudo si no no deja

per a un ch-loqsea de un directori fiquem -R per q s’aplico a tot lo d dins


CHATGPT TEORIA

Permisos en Ubuntu: fitxers i directoris

En Ubuntu (i en general en sistemes GNU/Linux), els permisos són un mecanisme de seguretat que determina quins usuaris poden llegir, modificar o executar fitxers i directoris. Cada fitxer o directori té un propietari, un grup associat i un conjunt de permisos que controlen les accions que es poden realitzar sobre ell. Aquest model permet protegir la informació i gestionar l'accés als recursos del sistema.

UGO (user,group,other)
Els permisos tradicionals es basen en tres categories d'usuaris:

User (u): propietari del fitxer o directori.
Group (g): grup propietari del fitxer o directori.
Others (o): qualsevol altre usuari del sistema.

Per a cadascuna d'aquestes categories es poden assignar tres permisos bàsics:

r (read): lectura.
w (write): escriptura.
x (execute): execució.

Per exemple, si executem:

ls -l proves/

Obtenim (sense contar que el primer valor que pot ser un - o una d indicant fitx o directori)
obtenim les tres primeres lletres son del propietari, les tres seguents del grup propietari, i els tres ultims de la resta
(explicar lo q haya salido en ese caso)


Permisos especials

A més dels permisos tradicionals, Linux disposa de tres permisos especials.

SUID (Set User ID)

Quan un executable té aquest bit activat, s'executa amb els privilegis del propietari del fitxer.

Exemple:

ls -l /usr/bin/passwd

Pot mostrar:
-rwsr-xr-x

La s substitueix la x del propietari.

El programa passwd necessita privilegis elevats per modificar /etc/shadow.

Per activar-lo:

chmod u+s programa


SGID (Set Group ID)

En fitxers executables, el programa s'executa amb el grup propietari.

En directoris, els fitxers nous hereten el grup del directori.

Exemple:

chmod g+s projecte

Visualització:

drwxrwsr-x

És molt útil en directoris compartits entre membres d'un mateix grup.


Sticky Bit

S'utilitza principalment en directoris compartits.

Permet que només el propietari d'un fitxer (o root) pugui esborrar-lo, encara que altres usuaris tinguin permisos d'escriptura sobre el directori.

Exemple clàssic:

ls -ld /tmp

Resultat:

drwxrwxrwt

La t final indica el Sticky Bit.

Per activar-lo:

chmod +t directori


ACL (Access Control Lists)

Les ACL permeten definir permisos més detallats que el model UGO tradicional.

Per exemple, podem voler donar permisos a un usuari concret sense canviar el propietari ni el grup.

Veure ACL
getfacl projecte

Exemple:

user::rwx
user:anna:rwx
group::r-x
other::---

Això indica que l'usuari anna té permisos complets encara que no sigui propietària.

Configurar ACL

Donar permisos complets a l'usuari anna:

setfacl -m u:anna:rwx projecte

Donar permisos de lectura a un grup:

setfacl -m g:professors:r-- fitxer.txt

Eliminar una ACL:

setfacl -x u:anna projecte


ACL per defecte

També es poden definir ACL heretades per als fitxers nous creats dins d'un directori.

Exemple:

setfacl -d -m u:anna:rwx projecte

A partir d'aquest moment, els fitxers nous creats a projecte heretaran aquests permisos.


Podem consultar les acl d'un directori en "getfacl"


Umask

La umask és una màscara que determina quins permisos es retiren per defecte quan es creen fitxers o directoris nous.

Valors inicials teòrics:

Fitxers: 666 (rw-rw-rw-)
Directoris: 777 (rwxrwxrwx)

La umask resta permisos d'aquests valors

Consultar la umask
umask

Exemple:

0022

Càlcul

Per a fitxers:

666 - 022 = 644
rw-r--r--

Per a directoris:

777 - 022 = 755
rwxr-xr-x


Resum

El sistema de permisos de Linux combina diversos mecanismes. Els permisos UGO proporcionen el control bàsic sobre propietari, grup i altres usuaris. Els permisos especials (SUID, SGID i Sticky Bit) afegeixen funcionalitats avançades relacionades amb l'execució de programes i els directoris compartits. Les ACL permeten definir permisos específics per a usuaris o grups concrets més enllà del model tradicional. Finalment, la umask controla els permisos inicials dels fitxers i directoris nous. La combinació d'aquests mecanismes proporciona una gestió flexible i segura dels accessos en Ubuntu.






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



