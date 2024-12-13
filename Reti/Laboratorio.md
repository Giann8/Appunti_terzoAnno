# Lezione_2

(consiglia di non usare apparati di rete cisco)
cge - Gigabit ethernet

---
# Lezione_3
Se ho apparati di livello uguale utilizzo la tipologia cross, altrimenti straight.

![[../Images/Lab_reti2.png]]

---
# Lezione_4
`?`-> Svela i comandi eseguibili
`show` -> utile come utente.
in caso di errori per mac ctrl+shift+^
stare in privilegiato solo per il comando da fare in privilegiato.

per configurare da cli:
config -> scelgo cosa (interface) -> scelgo il tipo di porta (ff,fr)->0/1
quando farò do show non si autocompleterà
per mettere una nuova vlan andrò in config e utilizzerò `vlan {id_vlan}` per settare il nome (all'interno di vlan) farò `name {nome_vlan}` check con ? in caso dovessi aggiungere altro (ma ci sarà carriage return)

con `switchport` configuro il canale:
- `switchport access vlan {id}`
- `switchport trunk allowed vlan add 120`

---
# Lezione_5
### Class-based addressing
- Primo ottetto serve per capire il continente
I router non possono avere due interfacce sulla stessa rete, tutte le loro interfacce si trovano su reti diverse.

Ricordarsi nei router di settare l'indirizzo ip dello switch e accendere sempre le porte
Gli indirizzi di base sono sempre pari.
L'indirizzo di Broadcast è sempre dispari.


---
# Lezione_6

## Subnetting
### Dimensionamento_sottoreti
rete 192.168.20.96/27

- VERDE: 4 host + 1 router +broadcast + base = 7 indirizzi -> 3 bit 
	01100111
	- Netmask: 255.255.255.248
	- Base: 192.168.20.96/29
	- Broadcast: 192.168.20.103(01100111)
	- Range:192.168.20.97-192.168.20.102
- ARANCIO: 2 host + router +broadcast + base = 5 indirizzi -> 3 bit
	01101000
	- Netmask:255.255.255.248
	- Base: 192.168.20.104/29
	- Broadcast: 192.168.20.111
	- Range: 192.168.20.105 - 192.168.20.110


---

# Lezione_7
## PMI con euristica
- R reparto produzione 58 host (+gw,bcast,base) -> 61 -> 64(6 bit)
	- Base:10.11.160.0/26 (subnetID 00);
	- Netmask: 255.255.255.192;
	- Bcast: 10.11.160.63; 
	- Range :10.11.160.1 - 10.11.160.62;

- K marketing 28 host (+3) = 31 -> 32 (5 bit)
	- Base: 10.11.160.64/27(subnetID 010); 
	- Netmask: 255.255.255.224;
	- Bcast:10.11.160.95; 
	- Range: 10.11.160.65 - 10.11.160.94;

- A amministrazione 25 host(+3) = 28 ->32 (5 bit)
	- Base:10.11.160.96/27 (subnetID 011); 
	- Netmask: 255.255.255.224;
	- Bcast:10.11.160.127; 
	- Range: 10.11.160.97-10.11.160.126;

- G gestione ordine 14 host (+3) = 17 -> 32 (5 bit)
	- Base:10.11.160.128/27 (subnetID 100);
	- Netmask: 255.255.255.224;
	- Bcast:10.11.160.159;
	- Range:10.11.160.129-10.11.160.158;

- M magazzino 9 host (+3) = 12 -> 16 (4 bit)
	- Base:10.11.160.160/28 (subnetID 1010);
	- Netmask: 255.255.255.240;
	- Bcast: 10.11.160.175(1010|1111);
	- Range: 10.11.160.161 - 10.11.160.174;

## PMI (con regola)

- A amministrazione 25 host (+3) = 28 -> 32 (5 bit)
	- Base: 10.11.160.0/27 (subnet 000);
	- Netmask: 255.255.255.224;
	- Bcast: 10.11.160.31;
	- Range (GW): 10.11.160.1 - 10.11.160.30; 

- G gestione ordine 14 host (+3) = 17 -> 32 (5 bit) ( 32 multiplo di 32, va bene)
	- Base: 10.11.160.32/27 (subnet 001);
	- Netmask: 255.255.255.224;
	- Bcast: 10.11.160.63;
	- Range (GW): 10.11.160.33 - 10.11.160.62;

- K marketing 28 host (+3) = 31 -> 32 (5 bit) (64 multiplo di 32, va bene)
	- Base: 10.11.160.64/27 (subnet 010);
	- Netmask: 255.255.255.224;
	- Bcast: 10.11.160.95;
	- Range: 10.11.160.65 - 10.11.160.94;

- M magazzino 9 host (+3) = 12 -> 16 (4 bit) (96 multiplo di 16)
	- Base: 10.11.160.96/28 (subnet 0110);
	- Netmask: 255.255.255.240;
	- Bcast: 10.11.160.111;
	- Range: 10.11.160.97 - 10.11.160.110;

- R reparto produzione 58 host (+gw,bcast,base) -> 61 -> 64(6 bit) (112 non va bene quindi vado fino a 128)
	- Base: 10.11.160.128/26 (subnet 10);
	- Netmask: 255.255.255.192;
	- Bcast: 10.11.160.191;
	- Range: 10.11.160.129 - 10.11.160.190;

## Cisco-Router (cli)
fare no all'inizio
conf t
? -> elenca i vari comandi
show interfaces
show ip protocol

ip address 192.168.0.1 255.255.255.0
accendere interfaccia

se vogliamo avere due vlan su una sola interfaccia (router cfe) possiamo creare delle sotto interfacce.
Mettere in trunk il cavo

```
interface fastEthernet 0/0.10
encapsulation dot1q vlanId
ip address 192.168.0.1 255.255.255.0
no shutdown
```
Infine andiamo a ad accendere l'intera interfaccia.

# Lezione_8
## Configurazione server DHCP
Iniziamo aggiungendo un server nella VLAN

# Lezione_9
Le sottoreti tra i router possono contenere solo 4 indirizzi ip che permettono ovvero quelli che servono per i due router, il bcast e l'indirizzo base.
L'admin deve istruire l'apparato riguardo il passaggio delle sottoreti, definendo eventuali output interface in modo da istruire alcuni apparati riguardo apparati lontani.

`passive-interface` serve a non far mandare le informazioni verso un certo route


# Lezione_11
## ACL extended
possiamo utilizzare diversi quantificatori nella port number

```
access-list 110 permit TCp any host 192.168.200.200 eq 80
access-list 110 deny Icmp any any (blocca qualsiasi segnale, anche di errore)
```

# Lezione_12

## Java socket
I server devono dare l'illusione all'utente di lavorare solo per lui

## User Agent
Qualunque browser è uno user agent, è un processo software che si interfaccia con l'utente sopra e con la rete sotto

Le socket sono affidabili, portabili e permettono collegamento double direction.
Numeri di porta sono unsigned short su 16 bit ( se unsigned long)

# Lezione_13
## Socket
La socket del server è la socket passiva che non si 

Il client crea la socket, recupera l'indirizzo e 

```java
public class Client{
public static void main(String[] args){
Socket sClient;
InetAddress ia;
InetSocketAddress isa;

sClient = new Socket();
try {
ia= InetAddress.getLocalHost();
isa = new InetSocketAddress(ia,50000); //porta però che potrebbe essere giù in uso;
} catch(UnknownHostException uhe){
uhe.printstackTrace();
}
}
}
```
la porta da mettere deve essere oltre a 49900 (peschiamo tra le effimere)
no porta 80 per il server

# Esercizi
### Lezione_5
1. Conversioni
	- 127.128.129.192 -> 01111111.10000000.10000001.11000000
	- 218.160.179.60 -> 11010000.10100000.10110011.00111100
	- 01011011.01110110.00101111.10011111->91.118.47.159
	- 00001100.10001000.01110010.00110111->12.136.114.55

2. Indirizzo broadcast, netmask e 2 indirizzi validi per
	- 15.0.0.0 (A)
		- Bcast: 15.255.255.255; 
		- netmask: 255.0.0.0;
		- 2 indirizzi: 15.10.211.57, 15.0.0.1,15.255.255.254
	- 137.149.0.0 (B)
		- Bcast:137.149.255.255; 
		- netmask: 255.255.0.0;
		- 2 indirizzi: 137.149.0.1, 137.149.255.254
	- 215.151.59.0 (C)
		- Bcast:215.151.59.255; 
		- netmask: 255.255.255.0;
		- 2 indirizzi: 215.151.59.1 - 215.151.59.254;

3. Indirizzi di host (n) -> indirizzo base, netmask, indirizzo broadcast, numero apparati indirizzabili:
	(_networkID_)
	
	- 111.162.136.87 (12) -> _01101111.1010_|0010.01010111
		- Base: 01101111.1010|0000.00000000 -> 111.160.0.0/12
		- Netmask: 11111111.11110000.00000000.00000000 ->255.240.0.0
		- Bcast: 01101111.10101111.11111111.11111111 -> 111.175.255.255
		- numero apparati: 2^20 (numero bit rimanenti) - 2 (impegnati in broadcast)
	- 206.191.1.207 (25) -> _10001110.10111111.00000001.1_|1001111
		- Base: 10001110.10111111.00000001.1|00000000 -> 206.191.1.128/25
		- Netmask: 11111111.11111111.11111111.1|0000000 -> 255.255.255.128
		- Bcast: 10001110.10111111.00000001.1|1111111 -> 206.191.1.255
		- numero apparati: 2^7 - 2

---
### Lezione_6
1. Indirizzamento a livello 3
	- Indirizzo base rete 192.168.20.96/27
	- Subnet s1 con 5 apparati; subnet s2 con 14 apparati (estendo con switch)
		- s1:
			- Netmask: 255.255.255.248;
			- Base: 192.168.20.96/29;
			- Broadcast: 192.168.20.103;
			- Range: 192.168.20.97 - .102;
		- S2:
			- Netmask:  255.255.255.248;
			- Base: 192.168.20.104/28;
			- Broadcast: 192.168.20.119;
			- Range: 192.168.20.105-.118;