---
layout: default
title: "Sprint 2. Instal·lació, Configuració de Programari de Base i Gestió de Fitxers"
permalink: projecte1/sprint2/
---

## 1. Sistemes de fitxers i particions

intro

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
		adduser
