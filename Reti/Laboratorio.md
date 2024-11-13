## Lezione 1

(consiglia di non usare apparati di rete cisco)
cge - Gigabit ethernet

## Lezione 2
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