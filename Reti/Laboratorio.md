        ## Lezione_1

(consiglia di non usare apparati di rete cisco)
cge - Gigabit ethernet

## Lezione_2
Se ho apparati di livello uguale utilizzo la tipologia cross, altrimenti straight.

![[../Images/Lab_reti2.png]]

## Lezione_4
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

## Lezione_5
### Class-based addressing
- Primo ottetto serve per capire il continente
I router non possono avere due interfacce sulla stessa rete, tutte le loro interfacce si trovano su reti diverse.

Ricordarsi nei router di settare l'indirizzo ip dello switch e accendere sempre le porte
Gli indirizzi di base sono sempre pari.
L'indirizzo di Broadcast è sempre dispari.
## Esercizi
### Lezione_5
1. 
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

1. Indirizzi di host (n) -> indirizzo base, netmask, indirizzo broadcast, numero apparati indirizzabili:
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