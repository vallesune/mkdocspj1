---
title: "Sprint 2. Instal·lació, Configuració de Programari de Base i Gestió de Fitxers"
---

## 1. Sistemes de fitxers i particions

kkkkkk
1. Sistemes de fitxers i particions
  Mida de sector
    
    Unitat mínima física del disc per guardar dades.
    
   Normalment: 512 bytes.

  Mida de bloc
  
    Unitat mínima lògica que utilitza el sistema operatiu per gestionar les dades.
    
    Per defecte: 4 KB (4096 bytes), però es pot modificar durant la formatació.
    
    Cada partició pot tenir una mida de bloc diferent segons el sistema de fitxers.

  Fragmentació

    Interna (lògica): pèrdua d’espai per blocs massa grans o petits.
    
    Externa (física): fitxers separats en diferents blocs del disc, reduint el rendiment.

  Tipus de formatació
    
    Formatació d’alt nivell: crea o reinicia el sistema de fitxers però manté el contingut.
    
    Formatació de baix nivell: esborra completament el contingut, repara errors físics i crea de nou la estructura de sectors. Es fa amb eines especialitzades.
    
    Formatació de nivell mitjà: recrea el sistema de fitxers però només marca els blocs defectuosos, no els repara.

  Gestió de particions

    Eines com GParted o línies d’ordres (fdisk, parted) permeten:
    
    Crear, esborrar i redimensionar particions.
    
    Assignar sistemes de fitxers diferents.
    
    Comprovar l’estat dels blocs i sectors.

  Particions i volums

    Partició: fragment físic d’un disc.

    Volum: agrupació lògica de particions o discos, que permet unificar espai de diversos discos sota una sola unitat virtual.



## 2. Gestio d'usuaris, grups i permisos

kkkkkk
