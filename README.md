# switch-stacking
Mise en place de switch stacking

![image](https://user-images.githubusercontent.com/83721477/170940145-06d2dc47-bb2d-4707-9e1d-ea9c73182052.png) 

## Qu’est ce que la mise en pile ?
L’idée consiste à raccorder plusieurs switches ensemble pour former une unité logique unique: virtuellement, tout se passe comme s’il y avait un seul « gros » switch.<br> Donc, il n’y a qu’une seule adresse IP affectée à la pile pour administrer et superviser l’ensemble. Lorsque plusieurs commutateurs sont mis en pile, ils deviennent un seul nouveau système…

Cela présente l’avantage d’être efficace (et financièrement pertinent) puisqu’on peut utiliser la pile pour augmenter la capacité en termes de nombres de ports uniquement lorsqu’on en a besoin. La technologie Cisco permet de regrouper en pile jusqu’à 9 commutateurs.

Cela est possible grâce au raccordement spécifique (les connecteurs sont sur la face arrière des commutateurs) qui crée une topologie en anneau entre les commutateurs: le trafic peut donc être véhiculé entre les commutateurs par deux chemins distincts. Cet anneau apporte donc une fiabilité à la pile.

Pour afficher le numéro d'un swith dans la pile, il faut presser le bouton mode pour selectionner l'item stack, le numéro du port qui clignote correspond au numéro du switch.

![image](https://user-images.githubusercontent.com/83721477/171122595-85e042b6-8529-40f0-961e-8cb0105acadc.png)


![image](https://user-images.githubusercontent.com/83721477/170940684-e04d918f-9893-4a68-9d1f-ea11c9fc81c0.png)

## Principe de fonctionnement
### Notion de commutateur maître ou actif
Dans une pile de plusieurs commutateurs, un des commutateurs va avoir un rôle important puisqu’il va dicter le comportement pour tous les commutateurs de la pile. 

En environnement Stackwise et Stackwise Plus, le commutateur principal est appelé le maitre de la pile (Master). En cas de panne ou de problème avec le commutateur Maitre, un autre commutateur se verra attribué ce rôle pour la pile.
En environnement Stackwise-480, donc notamment pour les commutateurs Cisco Catalyst 3850, ce commutateur est appelé le commutateur actif (Active). En cas de panne sur cet équipement, celui qui aura été élu commutateur de secours (Standby) prendra le relais.

### Election du commutateur Maitre ou Actif
* Le commutateur qui a été allumé le plus tôt sera élu le maitre de la pile.
* Il est possible d’avoir un contrôle déterministe du commutateur Maitre par configuration du paramètre « Priorité pour être maître » (Switch Priority).  La priorité la plus haute (valeur configurable entre 1 et 15 – 1 étant la valeur par défaut) sera choisie pour déterminer le commutateur Maitre.

![image](https://user-images.githubusercontent.com/83721477/170941173-c8d383d1-3967-494c-9952-36e9738b5660.png)
