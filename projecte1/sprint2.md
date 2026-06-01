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
		
		Crear usuaris o grups:
		
		'adduser' per crear un usuari de manera automatica, unicament introduim el nom de l'usuari i la password al moment i ens crea la carpeta home i els permisos automaticament.

		`useradd` s'utilitza tambe per crear usuaris pero de manera manual, despres de crearlo hem de configurarli la contrasenya, la home i si volem tambe el shell ja que no ve en bash per defecte.

		'addgroup' serveix per crear un grup. 


		Modificar usuaris, grups o contraseñes:

		'usermod' permet modifcar usuaris per exemple per bloquejarlos

		'groupmod' permet modificar un grup, per exemple canviarli el nom

		'change' permet afegir una caducitat a les contrasenyes
		

		Eliminar usuaris o grups:

		'userdel'

		'deluser'

		'groupdel'


		Afegir un usuari a un grup:

		'adduser usuari grup'

		'gpasswd -a usuari grup' (afegig user grup com secundari tipo apend) (-A hace al user admin de ese grupo)
		
		'usermod -a -G grup usuari' (-a lo mismo i la -G es para modif el grupo principal del user q de primeras es el q se crea auto igual q el nombre del usu)

		Modifiquem el nom d'usuari funcionalment:
		
		'usermod -l' (nounom anticnom) per canviar l'user
		canviar nom de carpeta home mv /home/ant ''/nou
		usermod -d /home/nou per a q la home del user sigui la nova 
		id user com per info del user
		groupmod -n nounom anti canvia el nom del grup del user
		comprov rapid de id, cat passwd, group que estan correct 
		iniciar grafico con el user (deveria func)
		abrir term i poner whoaim para la cap


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
# Habilitar colores en el prompt
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


### Automatizacio amb scripts de les copies de seguretat

Podem automatizar el proces de crear una copia de seguretat amb scripts i eines com cron o anacron

Cron
Es fa servir per programar tasques en una data i hora concretes. Funciona únicament si el sistema està encès al moment programat, per la qual cosa és ideal per a tasques específiques i recurrents d'usuaris, com ara còpies de seguretat o execucions programades.

Les tasques de cron poden configurar-se de forma global al fitxer /etc/crontab, que afecta tots els usuaris, o de forma individual mitjançant l'ordre crontab per a cada usuari.

A més, al directori /etc/ hi ha carpetes com cron.daily, cron.weekly i cron.monthly, que faciliten l'execució automàtica de scripts segons la seva periodicitat.


Anacron
Permet executar tasques periòdiques (diàries, setmanals, mensuals), encara que el sistema estigui apagat en el moment previst. És especialment útil per a tasques de manteniment del sistema.

Primer creem un petit script indicant el bash, un timestamp de la data actual i un tar de la carpeta descarges

Si volem que l'script s'executi en un moment concret utilitzant crontab editem /etc/crontab i indiquem com es veu el minut i la hora, l'usuari que executa i la comanda que sera l'execucio de l'script

Per automatitzar l'execucio diaria amb anacron copiarem l'script al directori /etc/cron.dialy sense l'extensio .sh i modificarem l'arxiu /etc/anacrontab per a que els cron diaris s'executin un minut despres d'enjegar la maquina


## 4. Quotes de disc i d'usuari

A Ubuntu, les quotes de disc permeten limitar lespai demmagatzematge que pot utilitzar cada usuari o grup. Això ajuda a controlar lús del disc i evitar que un sol usuari ocupi tots els recursos disponibles del sistema.

Per configurar quotes en un disc primer amb la mv tancada afegirem un disc

Despres instalarem el paquet quota en apt

Crearem una particio de tot el disc i la formatarem en ext4

Creem una carpeta de proves

Montem la particio a la carpeta que acabem de crear en fstab, donantli tambe permisos de quotes

Reiniciem la maquina i a la carpeta de proves esta montat correctament

Pasem a activar els fitxers de quota en quotacheck i activarles en quotaon

Crearem un user de prova 

Definim la quota soft i la hard (explicar diferencia?)

En edquota -u li asignem les quotes al usuari (-u user1)(s'obri learxiu este)

En repquota comprovem les cuotes de tots els usuaris al disc (repquota /dev/sdc1)

En quota -u comprovem les quotes del usuari

Podem provar que la quota funciona afegint fitxers i comprovem que mentres no superem el limit es creen sense problemes, pero que cuan el superem es creen buits (dd if...)



