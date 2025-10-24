---
title: "Sprint 1.Inst. i Config inicial"
---

## 1. SO ubuntu (virtualitzacio i instalacio)

Creem una nova maquina virtual per una instal·lació dual de ubuntu 22 amb windows 10 on començarem instal·lant l’ubuntu

<img width="866" height="487" alt="captura16" src="https://github.com/user-attachments/assets/702c25df-1614-4afc-945f-2987186b70cc" />

li asignem la ram necesaria

<img width="866" height="487" alt="captura17" src="https://github.com/user-attachments/assets/bf3ad434-2549-41a4-aee3-643586fcfb38" />

i un disc de 80gb

<img width="866" height="487" alt="captura18" src="https://github.com/user-attachments/assets/f26b9481-90e1-44f6-84f3-cf21b2bdeeb6" />

instalem ubuntu

<img width="885" height="685" alt="captura19" src="https://github.com/user-attachments/assets/bbb1060e-f769-4380-a05e-69624e755bc7" />

al moment de seleccionar el tipus d'instal·lació triem “més opcions” per poder particionar el disc manualment

<img width="885" height="685" alt="captura21" src="https://github.com/user-attachments/assets/d215c898-2d48-4223-aded-5db145daf18c" />

utilitzem la meitat del disc per ubuntu, creant una particio efi, una swap, un boot, una arrel i la home i deixem 40gb per la instal·lació dual amb windows 

<img width="845" height="637" alt="captura31" src="https://github.com/user-attachments/assets/eb376751-1080-4e7f-a475-b5f5e56292dc" />

despres acabem de configurar l’usuari i contrasenyes i s’instalara

<img width="845" height="637" alt="captura34" src="https://github.com/user-attachments/assets/b10ee831-3345-4edb-8b0d-e9e620360750" />

podem comprovar que accedim

<img width="1276" height="885" alt="captura36" src="https://github.com/user-attachments/assets/1e6db8be-e29e-4d61-ae64-bd09be2ec0a7" />

## 2. Llicenciament





## 3. Gestors d'arrencada duals
ara suposem que volem instalar windows a l’espai de disc lliure
des de la configuracio d’emagatzematge de virtualbox afegim la iso 

<img width="275" height="232" alt="captura1" src="https://github.com/user-attachments/assets/4ec7a7d4-cda2-4886-af0c-6b4056be3841" />


activem la efi per SO especials si no estava activa

<img width="883" height="582" alt="captura26" src="https://github.com/user-attachments/assets/ed7e476f-224b-4065-a21a-942e30bffac1" />


al iniciar amb F12 selecionem iniciar per dvd i podem instalar windows 

<img width="1027" height="749" alt="captura2" src="https://github.com/user-attachments/assets/56a489e8-07a1-4e5e-9b32-a2392550215f" />


triem la opcio personalitzada per poder utilitzar les particions

i triem la particio lliure

<img width="1027" height="749" alt="captura3" src="https://github.com/user-attachments/assets/e21e1ae4-afe2-48e5-a026-2c60218effac" />
<img width="1026" height="728" alt="captura5" src="https://github.com/user-attachments/assets/44b13e12-3d2e-4765-99a6-c4050fb2c7ca" />


es comença a instalar

<img width="1026" height="728" alt="captura6" src="https://github.com/user-attachments/assets/e9801cee-9911-408b-a6dd-16f622f3f07f" />


instalat correcte

<img width="1026" height="728" alt="captura7" src="https://github.com/user-attachments/assets/4eb54738-3b81-4d43-8f41-a91ecab5bb9a" />



una vegada instalat ja no podem accedir a ubuntu, tot i que segueix existint, ja que al haber instalat windows despres d’ubuntu, s’ha sobreescrit el grub per el MBR de windows i per recuperarlo i poder usar els dos SO utilitzarem la iso de supergrub2

des de la configuracio de la vm em eliminat la iso de windows i ara afegim la del supergrub

<img width="277" height="252" alt="captura8" src="https://github.com/user-attachments/assets/4816934e-3879-45e3-a54a-ec13d6cfbca3" />


entrem dins windows i anem a configuracio, recuperacio, i reiniciem desde inici avançat

<img width="1025" height="598" alt="captura10" src="https://github.com/user-attachments/assets/7b717179-451f-4d8f-99e2-9a0622340858" />


selecionem el disc-dvd que correspon al supergrub i este s’inicia

<img width="1025" height="598" alt="captura9" src="https://github.com/user-attachments/assets/f047eb1d-a0cf-4c20-a193-0d792776f24b" />


triem la opcio “detecta boot method”

<img width="645" height="412" alt="captura11" src="https://github.com/user-attachments/assets/8f4312f8-35c6-4682-9927-4092d9d50520" />


en el nostre cas triem ubuntu

<img width="645" height="412" alt="captura12" src="https://github.com/user-attachments/assets/c7cd236a-8857-400f-a12a-621831a8abf2" />


tornarem a entrar a ubuntu i obrirem una terminal

<img width="882" height="379" alt="captura13" src="https://github.com/user-attachments/assets/45af3518-a605-4949-9cdc-4d0338e3f264" />


grub-install /dev/sda

<img width="882" height="379" alt="captura15" src="https://github.com/user-attachments/assets/9cf288c8-a34e-44f0-a180-fda2ae644f21" />


modifiquem el fitxer /etc/default/grub i comentem les linies de TIMEOUT

<img width="990" height="626" alt="captura22" src="https://github.com/user-attachments/assets/11926344-7285-4694-a6a3-5bc9447778f1" />


i al final afegim ‘GRUB_DISABLE_OS_PROBER=false’

<img width="990" height="626" alt="captura21" src="https://github.com/user-attachments/assets/490bea63-f7a8-48e9-9e88-7a5b1f8bdb7e" />


guardem i actualitzem el grub en ‘update-grub2’

<img width="990" height="626" alt="captura23" src="https://github.com/user-attachments/assets/a59e1f15-671f-4bf6-9713-6fad48d840c1" />


ja podem accedir!

<img width="990" height="626" alt="captura24" src="https://github.com/user-attachments/assets/6d6e7dbc-2320-41af-b38b-a467cd2b0753" />



## 4. punts de restauracio
Per fer proves de restauracio de discos utilitzarem l'eina grafica timeshift
Primer afegim a la maquina virtual un disc extra per proves

<img width="574" height="332" alt="image" src="https://github.com/user-attachments/assets/a7818c5a-b646-4c6d-8532-1ffbed64b352" />


Dins de la maquina comprovem que esta amb "fdisk -l" i es el disc sdb

<img width="741" height="516" alt="captura3" src="https://github.com/user-attachments/assets/6cf5a553-de0f-4217-ad6e-286a83af0c92" />


El formatejem per que tot el disc ocupi una sola particio de tipus ext4

<img width="875" height="517" alt="captura5" src="https://github.com/user-attachments/assets/fe83ddb7-e22b-478c-aeaf-1e9ff8863767" />

<img width="870" height="530" alt="captura6" src="https://github.com/user-attachments/assets/2c089b3c-d97a-4f66-b8ac-b7592a26992c" />

Podem instalar timeshift per terminal amb apt "sudo apt install timeshift"

<img width="1343" height="576" alt="captura2" src="https://github.com/user-attachments/assets/7efdc5e8-f307-4202-a746-569666440759" />

Obrim el programa i seleccionem tipus rsync 

<img width="622" height="671" alt="captura9" src="https://github.com/user-attachments/assets/c9f6f211-06b1-429c-bdc1-8c198dd6b819" />


Triem la particio creada del disc afegit

<img width="622" height="671" alt="captura11" src="https://github.com/user-attachments/assets/e831c7d0-6b81-43fc-9648-2cce9747ef1d" />


Per fer proves mes rapidament seleccionem que faigui copies de seguretat al arrencar la maquina

<img width="622" height="671" alt="captura13" src="https://github.com/user-attachments/assets/00aeb1a6-d7d1-4aaa-ba42-85ae4fa5fb4a" />


Nomes farem copies dels continguts del usuari

<img width="797" height="671" alt="captura14" src="https://github.com/user-attachments/assets/6c419894-0285-466a-87de-e1b221e66b53" />


Es comença a creea

<img width="797" height="671" alt="captura15" src="https://github.com/user-attachments/assets/34cb5036-de76-4d83-a1a0-e7f6b9489c6a" />


Un cop acabada la copia podem eliminar alguns archius del usuari per provar de restaurarlos

<img width="1018" height="729" alt="captura17" src="https://github.com/user-attachments/assets/14d53db6-a899-44a0-a164-b30d26dfb139" />


Restaurem la copia

<img width="1018" height="729" alt="captura18" src="https://github.com/user-attachments/assets/e7c12f57-403c-4180-b756-e86f744fe53d" />

<img width="1187" height="849" alt="captura20" src="https://github.com/user-attachments/assets/85adbf18-00f0-4cab-915c-01fada935a1f" />


I comprovem que hem recuperat els fitxers

<img width="1187" height="849" alt="captura21" src="https://github.com/user-attachments/assets/a6bb61af-9a87-4f5a-af7d-987bcb92b9b3" />


## 5. Config xarxa
Podem comprovar les nostres xarxes i ips amb ip a

<img width="724" height="483" alt="captura24" src="https://github.com/user-attachments/assets/d59c4b87-9d27-43e1-971e-0419d629be37" />


Podem modificar els parametres de xarxa al fitxer .yaml que es troba a /etc/netplan/


Per defecte ve indicat unicament el renderer que ens permet tenir interficie grafica, el NetworkManager, si volem un renderer sense interficie podem utilitzar networkd

<img width="735" height="483" alt="captura26" src="https://github.com/user-attachments/assets/1a3f6f97-8c88-489b-9849-9ff939186a8f" />

Podem modificar i afegir la configuracio directament a l'archiu


Exemple de configuracio ethernet sense dchp, fixa

Indiquem parametres com l'adreça amb la mascara, la porta d'enllaç, i algun dns

<img width="735" height="483" alt="captura28" src="https://github.com/user-attachments/assets/c50d5a18-8ad2-49c3-8d86-f510f73629fb" />

Per aplicar les configuracions fetes al fitxer el guardem, tornem a terminal i utilitzem la comanda 'netplan apply'

<img width="735" height="483" alt="captura29" src="https://github.com/user-attachments/assets/2a22b823-0f11-42ae-8686-13444aa28d66" />

comprovem en un 'ip a'

<img width="724" height="483" alt="captura23" src="https://github.com/user-attachments/assets/d5472f2c-91db-4385-9c11-d5e90caca184" />



## 6. Comandes generals (instalacio)



