# rappels sur le binaire

1 bit = 0 ou 1

1 octet = 8 bits

on peut coder 2<sup>8</sup> = 256 valeurs différentes sur un octet.  
ces valeurs vont de 0 à 255.

# la base sur les réseaux

lorsque plusieurs appareils (ordinateurs, téléphones, imprimantes, ...) veulent communiquer entre eux, ils doivent utiliser des **protocoles de communication**.  
parmi ces protocoles, on retrouve **TCP/IP** (la suite des protocoles Internet).

chaque appareil connecté est appelé un **hôte**.  

les données à envoyer sont divisées en **paquets**.  

**IP** est le protocole d'adressage (&rarr; couche réseau de la communication).  
il utilise les **adresses IP** des hôtes du réseau pour envoyer leurs paquets.  
IP assure que les paquets arrivent à la bonne destination, mais il ne garantit ni leur ordre ni leur fiabilité.

**TCP** est le protocole de contrôle des transmissions (&rarr; couche transport de la communication).  
il établit une connexion entre expéditeur et récepteur et vérifie que les paquets sont bien reçus (sinon, il les retransmet) et qu'ils sont dans le bon ordre (sinon, il les reclasse).

chaque hôte doit avoir une **adresse IP** unique.  

ici, les adresses IP sont toutes codées sur 4 octets (c'est de l'IPv4).  
donner une adresse IP, c'est donner la valeur de ses 4 octets en décimal. (par exemple : 128.255.0.1)

plusieurs hôtes forment localement un **sous-réseau**.  

dans un sous-réseau, les hôtes partagent la même **adresse de sous-réseau**.  
cette adresse peut s'obtenir à partir de l'adresse IP d'un hôte, en lui appliquant son **masque de sous-réseau**. cela consiste à ne garder que les bits de l'adresse IP où le masque est à 1.  
exemple sur 5 bits :
* adresse IP en binaire : 10110
* masque de sous-réseau : 11100
* &rarr; adresse du sous-réseau : 10100

un masque est toujours de la forme : 1...0  
(par exemple : 111111100000)  
on peut le donner sous forme binaire, décimale ou CIDR (`/` + le nombre de 1 au début du masque). par exemple, sur 8 bits :
* en décimal : 192
* en binaire : 11000000
* en CIDR : /2

par exemple, avec un masque /26, comme une adresse IP est codée sur 4 octets, on sait que ses 26 premiers bits codent le sous-réseau et que le reste des bits (les 6 les plus à droite) codent l'adresse l'hôte au sein de son sous-réseau.  
choisir un gros masque (111111111111111111100 par exemple), c'est donc augmenter le nombre de sous-réseaux possibles au détriment du nombre d'hôtes par sous-réseau.

une autre façon de le voir c'est de dire que choisir une adresse IP et un masque de sous-réseau, c'est choisir la plage des adresses IP qui peuvent composer ce sous-réseau. par exemple, sur 4 bits :
* si le masque est 0000, les adresses IP peuvent prendre toutes les valeurs entre 0 et 15
* si le masque est 1000, les adresses IP sont soit toutes entre 0 et 7 (premier bit à 0), soit toutes entre 8 et 15 (premier bit à 1).
* si le masque est 1100, les adresses IP sont soit :
  * toutes entre 0 et 3 (premiers bits : 00)
  * toutes entre 4 et 7 (premiers bits : 01)
  * toutes entre 8 et 11 (premiers bits : 10)
  * toutes entre 12 et 15 (premiers bits : 11)
* ...

on observe qu'augmenter le masque d'un bit revient à chaque fois à :
* multiplier le nombre de plages d'adresses IP par 2 (c'est-à-dire multiplier le nombre maximal de sous-réseau par 2)
* diviser le nombre maximal d'hôtes par sous-réseau par 2.

lorsque je dis qu'une adresse IP doit être dans la plage de valeurs entre `min` et `max`, je sous-entends qu'elle n'est ni à `min` ni à `max`. en effet, l'adresse `min` fait déjà référence à l'adresse du sous-réseau et l'adresse `max` est l'adresse de diffusion dans ce sous-réseau.

un **switch** connecte plusieurs hôtes dans un même sous-réseau.

un **routeur** connecte plusieurs sous-réseaux entre eux. 

lorsque plusieurs sous-réseaux sont connectés, la plage d'adresses IP de chaque sous-réseau ne doit pas chevaucher celle des autres !

une **table de routage** est utilisée pour définir à quelle adresse IP envoyer un paquet lorsque son adresse de destination n'est pas directement accessible. c'est une liste d'associations :  
adresse du sous-réseau de destination &rarr; adresse IP suivante  
adresse du sous-réseau de destination &rarr; adresse IP suivante  
...

lorsque l'adresse de destination d'une table de routage est à `default` (ou `0.0.0.0/0`) les paquets sont toujours envoyés à l'adresse IP suivante.

les adresses IP suivantes sont réservées aux réseaux privés (ou réseaux locaux), c'est-à-dire, déconnectés d'Internet :
* 192.168.x.x
* de 172.16.x.x à 172.31.x.x
* 10.x.x.x

# division d'un octet par plages selon le masque

<img src="img/1.jpg" height="150px" />

par exemple, pour 128, les adresses IP d'un sous-réseau sont :
* soit toutes entre 0 et 127 (sous-entendu : entre 1 et 126)
* soit toutes entre 128 et 255 (sous-entendu : entre 129 et 254)

--- 

pour le masque 1110 0000 = 224, il y a 3 bits pour différencier les adresses réseaux donc il y a 8 plages d'adresses possibles :

<img src="img/3.jpg" height="100px" />

---  

pour le masque 1111 0000 = 240, les plages vont de 16 en 16 :

<img src="img/13.png" height="50px" />

(ou en partant de la fin :)

<img src="img/12.png" height="50px" />

---

<img src="img/14.png" height="300px" />

c'est le plus gros masque possible. il ne laisse la place que de coder 2 hôtes par sous-réseau.

# niveau 1

<img src="solution/1.png" width="100%" />

## premier réseau

le réseau est un unique sous-réseau.

le masque indique que le sous-réseau est codé sur les 3 premiers octets des adresses IP.

il suffit d'utiliser une adresse identique sur les 3 premiers octets.

## deuxième réseau

c'est la même chose sauf que le sous-réseau est codé sur les 2 premiers octets.

# niveau 2

<img src="solution/2.png" width="100%" />

# niveau 3

<img src="solution/3.png" width="100%" />

# niveau 4

<img src="solution/4.png" width="100%" />

# niveau 5

<img src="solution/5.png" width="100%" />

# niveau 6

<img src="solution/6.png" width="100%" />

# niveau 7

<img src="solution/7.png" width="100%" />

# niveau 8

<img src="solution/8.png" width="100%" />

# niveau 9

<img src="solution/9.png" width="100%" />

# niveau 10

<img src="solution/10.png" width="100%" />
