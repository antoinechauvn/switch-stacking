# switch-stacking
Mise en place de switch stacking

![image](https://user-images.githubusercontent.com/83721477/171123852-54ca0956-2b26-4449-bf6c-cfed03e33fe7.png)

## Qu’est ce que la mise en pile ?
L’idée consiste à raccorder plusieurs switches ensemble pour former une unité logique unique: virtuellement, tout se passe comme s’il y avait un seul « gros » switch.<br> Donc, il n’y a qu’une seule adresse IP affectée à la pile pour administrer et superviser l’ensemble. Lorsque plusieurs commutateurs sont mis en pile, ils deviennent un seul nouveau système…

Cela présente l’avantage d’être efficace (et financièrement pertinent) puisqu’on peut utiliser la pile pour augmenter la capacité en termes de nombres de ports uniquement lorsqu’on en a besoin. La technologie Cisco permet de regrouper en pile jusqu’à 9 commutateurs.

Cela est possible grâce au raccordement spécifique (les connecteurs sont sur la face arrière des commutateurs) qui crée une topologie en anneau entre les commutateurs: le trafic peut donc être véhiculé entre les commutateurs par deux chemins distincts. Cet anneau apporte donc une fiabilité à la pile.

Pour afficher le numéro d'un swith dans la pile, il faut presser le bouton mode pour selectionner l'item stack, le numéro du port qui clignote correspond au numéro du switch.

![image](https://user-images.githubusercontent.com/83721477/171122595-85e042b6-8529-40f0-961e-8cb0105acadc.png)


![image](https://user-images.githubusercontent.com/83721477/170940684-e04d918f-9893-4a68-9d1f-ea11c9fc81c0.png)

## Différents types de topologies de stack
### Topologie Chain

Celle-ci est la moins coûteuse, car dans cette topologie chaque commutateur est connecté à son voisin, de cette manière :

![image](https://user-images.githubusercontent.com/83721477/171124429-b6c22e32-b1fe-461e-bc89-f375f62307c6.png)

### Topologie Ring

Identitique à la topologie Chain, sauf qu’ici nous connectons simplement le premier membre de la stack avec le dernier. De cette manière, une redondance accrue est mise en place :

![image](https://user-images.githubusercontent.com/83721477/171124554-b81208e9-c465-40c8-8609-a4b74ce119b6.png)

## Principe de fonctionnement
### Notion de commutateur maître ou actif
Dans une pile de plusieurs commutateurs, un des commutateurs va avoir un rôle important puisqu’il va dicter le comportement pour tous les commutateurs de la pile. 

En environnement Stackwise et Stackwise Plus, le commutateur principal est appelé le maitre de la pile (Master). En cas de panne ou de problème avec le commutateur Maitre, un autre commutateur se verra attribué ce rôle pour la pile.
En environnement Stackwise-480, donc notamment pour les commutateurs Cisco Catalyst 3850, ce commutateur est appelé le commutateur actif (Active). En cas de panne sur cet équipement, celui qui aura été élu commutateur de secours (Standby) prendra le relais.

### Election du commutateur Maitre ou Actif
* Le commutateur qui a été allumé le plus tôt sera élu le maitre de la pile.
* Il est possible d’avoir un contrôle déterministe du commutateur Maitre par configuration du paramètre « Priorité pour être maître » (Switch Priority).  La priorité la plus haute (valeur configurable entre 1 et 15 – 1 étant la valeur par défaut) sera choisie pour déterminer le commutateur Maitre.

![image](https://user-images.githubusercontent.com/83721477/170941173-c8d383d1-3967-494c-9952-36e9738b5660.png)

### Redémarrer un switch d'un stack?
La commande suivante redémarre le switch numéro 4:
```
sw-2960x#reload slot 4
```

### Renuméroter le switch d'un stack?
La commande suivante renumérote le switch numéro 3 en switch numéro 2. Il faut ensuite redémarrer le switch.
```
sw-2960x(config)#switch 3 renumber 2
```

### Changer la priorité d'un switch dans le stack
Le switch qui a la priorité la plus haute devient le master. Le niveau de priorité va de 1 à 15. Le niveau le plus haut étant prioritaire.
Commande pour modifier le niveau d'un switch puis vérification:
```
sw-2960x(config)#switch 2 priority 15
Changing the Switch Priority of Switch Number 2 to 15
Do you want to continue?[confirm]

sw-2960x#sh switch
Switch/Stack Mac Address : 0024.d96d.e800
H/W Current
Switch# Role Mac Address Priority Version State
----------------------------------------------------------
*1 Master 0024.d96d.e800 1 0 Ready
2 Member 0024.5e23.a290 15 0 Ready
3 Member 0024.6256.0300 1 0 Ready
4 Member 0024.2b25.4520 1 0 Ready
```
