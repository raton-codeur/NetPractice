# petit guide de NetPractice 

## sommaire

<!-- no toc -->
  - [rappels sur le binaire](#rappels-sur-le-binaire)
  - [la base sur les réseaux](#la-base-sur-les-réseaux)
  - [division d'un octet par plages de valeurs selon le masque](#division-dun-octet-par-plages-de-valeurs-selon-le-masque)
  - [les équipements réseau](#les-équipements-réseau)
  - [niveau 1](#niveau-1)
  - [niveau 2](#niveau-2)
  - [niveau 3](#niveau-3)
  - [niveau 4](#niveau-4)
  - [niveau 5](#niveau-5)
  - [niveau 6](#niveau-6)
  - [niveau 7](#niveau-7)
  - [niveau 8](#niveau-8)
  - [niveau 9](#niveau-9)
  - [niveau 10](#niveau-10)

## rappels sur le binaire

tous les nombres décimaux (= écrits en base 10) peuvent s'écrire en binaire (= base 2).

un nombre binaire est composé de bits.  
1 bit = `0` ou `1`

sur n bits, on peut coder 2<sup>n</sup> valeurs différentes.

<details open>
<summary>quelques conversions</summary>
<table style="font-family: monospace;">
  <thead>
    <tr>
      <th>décimal</th>
      <th>binaire</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>0</td><td><code>00000000</code></td></tr>
    <tr><td>1</td><td><code>00000001</code></td></tr>
    <tr><td>2</td><td><code>00000010</code></td></tr>
    <tr><td>3</td><td><code>00000011</code></td></tr>
    <tr><td>4</td><td><code>00000100</code></td></tr>
    <tr><td>5</td><td><code>00000101</code></td></tr>
    <tr><td>6</td><td><code>00000110</code></td></tr>
    <tr><td>7</td><td><code>00000111</code></td></tr>
    <tr><td>8</td><td><code>00001000</code></td></tr>
    <tr><td>9</td><td><code>00001001</code></td></tr>
    <tr><td>10</td><td><code>00001010</code></td></tr>
    <tr><td>11</td><td><code>00001011</code></td></tr>
    <tr><td>12</td><td><code>00001100</code></td></tr>
    <tr><td>13</td><td><code>00001101</code></td></tr>
    <tr><td>14</td><td><code>00001110</code></td></tr>
    <tr><td>15</td><td><code>00001111</code></td></tr>
    <tr><td>16</td><td><code>00010000</code></td></tr>
    <tr><td>17</td><td><code>00010001</code></td></tr>
    <tr><td>30</td><td><code>00011110</code></td></tr>
    <tr><td>31</td><td><code>00011111</code></td></tr>
    <tr><td>32</td><td><code>00100000</code></td></tr>
    <tr><td>33</td><td><code>00100001</code></td></tr>
    <tr><td>34</td><td><code>00100010</code></td></tr>
    <tr><td>63</td><td><code>00111111</code></td></tr>
    <tr><td>64</td><td><code>01000000</code></td></tr>
    <tr><td>65</td><td><code>01000001</code></td></tr>
    <tr><td>126</td><td><code>01111110</code></td></tr>
    <tr><td>127</td><td><code>01111111</code></td></tr>
    <tr><td>128</td><td><code>10000000</code></td></tr>
    <tr><td>129</td><td><code>10000001</code></td></tr>
    <tr><td>130</td><td><code>10000010</code></td></tr>
    <tr><td>191</td><td><code>10111111</code></td></tr>
    <tr><td>192</td><td><code>11000000</code></td></tr>
    <tr><td>193</td><td><code>11000001</code></td></tr>
    <tr><td>223</td><td><code>11011111</code></td></tr>
    <tr><td>224</td><td><code>11100000</code></td></tr>
    <tr><td>225</td><td><code>11100001</code></td></tr>
    <tr><td>239</td><td><code>11101111</code></td></tr>
    <tr><td>240</td><td><code>11110000</code></td></tr>
    <tr><td>241</td><td><code>11110001</code></td></tr>
    <tr><td>247</td><td><code>11110111</code></td></tr>
    <tr><td>248</td><td><code>11111000</code></td></tr>
    <tr><td>249</td><td><code>11111001</code></td></tr>
    <tr><td>251</td><td><code>11111011</code></td></tr>
    <tr><td>252</td><td><code>11111100</code></td></tr>
    <tr><td>253</td><td><code>11111101</code></td></tr>
    <tr><td>254</td><td><code>11111110</code></td></tr>
    <tr><td>255</td><td><code>11111111</code></td></tr>
    <tr><td>256</td><td><code>100000000</code></td></tr>
  </tbody>
</table>
</details> 

1 octet = 8 bits

on peut coder 2<sup>8</sup> = 256 valeurs différentes sur un octet.  
ces valeurs vont de 
```
0 (décimal) = 0 (binaire)
```
à
```
255 (décimal) = 11111111 (binaire)
```

la table de vérité de l'opérateur binaire ET est la suivante :
```
0 ET 0 = 0
0 ET 1 = 0
1 ET 0 = 0
1 ET 1 = 1
```

on peut effectuer l'opération ET entre deux nombres en appliquant cette table de vérité bit à bit.  
par exemple :
```
9 ET 3 = 1
```
car 
``` 
9 (en décimal) = 1011 (en binaire)
3 (en décimal) = 0011 (en binaire)
1 (en décimal) = 0001 (en binaire)
```

[&uarr; retour au sommaire &uarr;](#sommaire)

## la base sur les réseaux

lorsque plusieurs appareils (ordinateurs, téléphones, imprimantes, ...) veulent communiquer entre eux, ils doivent utiliser des **protocoles de communication**.  
parmi ces protocoles, on retrouve **TCP/IP** (aussi appelé "la suite des protocoles Internet").

chaque appareil connecté est appelé un **hôte**.  

les données à envoyer sont divisées en **paquets**.  

**IP** (Internet Protocol) est le protocole d'adressage (&rarr; couche réseau dans le modèle OSI).  
il utilise les adresses des hôtes du réseau (les fameuses **adresses IP**) pour adresser correctement chaque paquet transmis.  
IP assure que les paquets arrivent à la bonne destination, mais il ne garantit ni leur ordre ni leur fiabilité.

**TCP** (Transmission Control Protocol) est le protocole de contrôle des transmissions (&rarr; couche transport dans le modèle OSI).  
il établit une connexion fiable entre chaque expéditeur et récepteur, vérifie que les paquets sont bien reçus (sinon, il les retransmet) et qu'ils arrivent dans le bon ordre (sinon, il les reclasse).

chaque hôte doit avoir une **adresse IP** unique ainsi qu'un **masque de sous-réseau**.  
dans les exercices, ça ressemble à ça : 

<img src="img/23.png" height="300px" />

ici, les adresses IP et les masques sont codées sur 4 octets (c'est de l'IPv4).  
donner une adresse IP ou un masque, c'est donc donner les valeurs de ces 4 octets. par exemple :
adresse IP en décimal | adresse IP en binaire
-- | --
`128.255.0.5` | `10000000.11111111.00000000.00000101`

plusieurs hôtes forment localement un **sous-réseau**.  

dans un sous-réseau, tous les hôtes partagent la même **adresse de sous-réseau** et (pour rester simple) le même masque de sous-réseau.  
l'adresse du sous-réseau peut s'obtenir à partir de l'adresse IP d'un hôte en binaire, en lui appliquant son masque de sous-réseau (en binaire aussi). cela consiste à ne garder que les bits de l'adresse IP où le masque est à 1.  
exemple :
* adresse IP : `104.198.241.245` (en décimal)  
= `01101000.11000110.11110001.11110101` (en binaire)
* masque de sous-réseau : `255.255.255.128` (en décimal)  
= `11111111.11111111.11111111.10000000` (en binaire)

    &rarr; adresse du sous-réseau : `01101000.11000110.11110001.10000000` (en binaire)  
    = `104.198.241.128` (en décimal)

> c'est équivalent de dire que l'adresse du sous-réseau s'obtient en faisant l'opération binaire ET entre l'adresse IP et le masque de sous-réseau.

un masque de sous-réseau (en binaire) est toujours de la forme : "un certain nombre de 1" suivi de "un certain nombre de 0".  
on peut le donner sous forme binaire, décimale ou CIDR.  
la notation CIDR (Classless Inter-Domain Routing) consiste à écrire `/` + le nombre de 1 au début du masque. elle est pratique car elle permet de préciser un masque directement à la fin d'une adresse IP (voir plus bas).  
par exemple :
masque de sous-réseau en décimal | masque de sous-réseau en binaire | masque de sous-réseau en notation CIDR
-- | -- | --
`255.255.240.0` | `11111111.11111111.11110000.00000000` | `/20`

le masque de sous-réseau sépare donc une adresse IP entre les bits qui servent à coder le sous-réseau (à gauche) de ceux qui servent à coder l'hôte au sein du sous-réseau (à droite). il suffit de préciser le nombre de bits qui servent à coder le sous-réseau pour en déduire le nombre de bits qui servent à coder l'hôte au sein du sous-réseau.  
par exemple, avec un masque /26, on sait que les 26 premiers bits de l'adresse IP codent l'adresse du sous-réseau et, sachant que l'adresse IP d'un hôte est codée sur 4 octets (= 32 bits), on sait que les 6 derniers bits (= 32 - 26) codent l'adresse de l'hôte au sein du sous-réseau.  
par exemple :  

`01101111.11110010.11000001.00101101/25`  
(= `01101111.11110010.11000001.00101101` avec le masque `/25`)  
&rarr; `01101111.11110010.11000001.0` (les 25 premiers bits) + `0101101` (le reste)  
&rarr; adresse du sous-réseau : `01101111.11110010.11000001.00000000`  
&rarr; adresse de l'hôte au sein du sous-réseau : `00000000.00000000.00000000.0101101`

on observe que choisir un gros masque (`11111111.11111111.11111111.11111100` par exemple), c'est augmenter le nombre de sous-réseaux possibles dans le réseau au détriment du nombre d'hôtes par sous-réseau.  
en effet, en augmentant le masque, on augmente le nombre de bits permettant de coder le sous-réseau et on diminue le nombre de bits permettant de coder l'hôte en lui-même.

par ailleurs, comme tous les hôtes d'un sous-réseau doivent avoir la même adresse de sous-réseau, il faut que, dans un sous-réseau, toutes les adresses soient dans la même plage de valeurs.  
petit exemple sur 4 bits :
* si le masque est `0000`, tous les hôtes du réseau ne peuvent qu'être dans le même sous-réseau. dans ce sous-réseau, les adresses IP peuvent être entre 0 (= 0000 en binaire) et 15 (= 1111 en binaire).
* si le masque est `1000`, il peut y avoir 2 sous-réseaux dans le réseau. dans un de ces sous-réseaux, les adresses IP sont soit toutes entre 0 et 7 (elles sont de la forme 0xxx en binaire), soit toutes entre 8 et 15 (elles sont de la forme 1xxx en binaire).
* si le masque est `1100`, il peut y avoir 4 sous-réseaux. les plages d'adresses IP sont :
  * entre 0 et 3 (= de la forme 00xx en binaire)
  * entre 4 et 7 (= de la forme 01xx en binaire)
  * entre 8 et 11 (= de la forme 10xx en binaire)
  * entre 12 et 15 (= de la forme 11xx en binaire)

on observe qu'augmenter le masque d'un bit revient à chaque fois à :
* multiplier le nombre de plages d'adresses IP par 2 (c'est-à-dire multiplier le nombre maximal de sous-réseau dans le réseau par 2)
* diviser le nombre maximal d'hôtes par sous-réseau par 2.

attention, il faut faire la différence entre la plage des adresses possibles et les valeurs effectivement possibles. lorsque je dis que, dans un sous-réseau, l'adresse IP d'un hôte doit être dans la plage de valeurs entre `min` et `max`, je sous-entends qu'elle n'est ni à `min` ni à `max`. en effet, l'adresse `min` fait déjà référence à l'adresse du sous-réseau en lui-même et ne peut pas être prise telle quelle par l'un de ses hôtes. l'adresse `max` quant à elle est l'adresse de diffusion (= broadcast) de ce sous-réseau. elle sert à envoyer des paquets à tous les hôtes du sous-réseau à la fois et ne peut pas non plus être prise telle quelle par l'un des hôtes du sous-réseau.

[&uarr; retour au sommaire &uarr;](#sommaire)

## division d'un octet par plages de valeurs selon le masque

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

[&uarr; retour au sommaire &uarr;](#sommaire)

## les équipements réseau

on a déjà vu les hôtes. voici les autres équipements qui composent les réseaux de NetPractice.

### le switch

un **switch** permet de connecter plusieurs hôtes dans un même sous-réseau.  
dans les exercices, il ressemble à ça :  

<img src="img/20.png" height="300px" />

### le routeur

un **routeur** permet de connecter plusieurs sous-réseaux entre eux.  
dans les exercices, il ressemble à ça :  

<img src="img/21.png" height="300px" />

il possède, lui-aussi, des **interfaces réseau** (une par sous-réseau connecté).  
pour faire simple, une interface réseau est un point de connexion dans le réseau, identifié par une adresse IP (qui doit être unique) et un masque de sous-réseau. 

lorsque plusieurs sous-réseaux sont connectés, la plage d'adresses IP de chaque sous-réseau ne doit pas chevaucher celle des autres !

### la table de routage

une **table de routage** est utilisée à un endroit précis du réseau (hôte, routeur, ...) pour définir la prochaine adresse à laquelle il faut envoyer un paquet lorsque l'adresse de destination de celui-ci est trop éloignée (on comprendra mieux en faisant les exercices).  

c'est une liste d'associations :  

* adresse de sous-réseau de destination &rarr; adresse IP suivante  
* adresse de sous-réseau de destination &rarr; adresse IP suivante  
* ...

dans les exercices, ça ressemble à ça :  

<img src="img/22.png" height="200px" />

dans cet exemple, on voit notamment que lorsqu'un paquet veut rejoindre le sous-réseau `78.149.0.0` (= `78.149.0.2` avec le masque `/18`) alors il est envoyé à `163.172.250.12`.

lorsque l'adresse de destination de la table est à `default` (ou `0.0.0.0/0`) alors les paquets sont toujours (?) envoyés à l'adresse IP correspondante.

### Internet

le fameux réseau mondial de l'Internet est représenté ainsi :

<img src="img/24.png" height="250px" />

il est forcément associé à une table de routage.  

on peut voir Internet comme un hôte qui n'a pas d'adresse IP en particulier.

lorsqu'un sous-réseau est connecté à Internet, les adresses IP suivantes ne peuvent pas être utilisées. en effet, elles sont réservées aux réseaux privés (ou réseaux locaux) déconnectés d'Internet :
* 192.168.x.x (en /16)
* de 172.16.x.x à 172.31.x.x (en /12)
* 10.x.x.x (/8)

[&uarr; retour au sommaire &uarr;](#sommaire)

## niveau 1

<img src="solution/1.png" width="100%" />

### premier réseau

le réseau est un unique sous-réseau.

le masque indique que le sous-réseau est codé sur les 3 premiers octets des adresses IP.

il suffit d'utiliser une adresse identique sur les 3 premiers octets.

### deuxième réseau

c'est la même chose sauf que le sous-réseau est codé sur les 2 premiers octets.

[&uarr; retour au sommaire &uarr;](#sommaire)

## niveau 2

<img src="solution/2.png" width="100%" />

[&uarr; retour au sommaire &uarr;](#sommaire)

## niveau 3

<img src="solution/3.png" width="100%" />

[&uarr; retour au sommaire &uarr;](#sommaire)

## niveau 4

<img src="solution/4.png" width="100%" />

[&uarr; retour au sommaire &uarr;](#sommaire)

## niveau 5

<img src="solution/5.png" width="100%" />

[&uarr; retour au sommaire &uarr;](#sommaire)

## niveau 6

<img src="solution/6.png" width="100%" />

[&uarr; retour au sommaire &uarr;](#sommaire)

## niveau 7

<img src="solution/7.png" width="100%" />

[&uarr; retour au sommaire &uarr;](#sommaire)

## niveau 8

<img src="solution/8.png" width="100%" />

[&uarr; retour au sommaire &uarr;](#sommaire)

## niveau 9

<img src="solution/9.png" width="100%" />

[&uarr; retour au sommaire &uarr;](#sommaire)

## niveau 10 
<span style="text-align: right;"></span>

<img src="solution/10.png" width="100%" />

[&uarr; retour au sommaire &uarr;](#sommaire)
