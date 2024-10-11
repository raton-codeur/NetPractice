# rappels sur le binaire

1 bit = 0 ou 1

1 octet = 8 bits

tous les nombres décimaux (= écrits en base 10) peuvent s'écrire en binaire (= base 2).  

<details>
<summary>tableau de conversion basique</summary>
<table style="font-family: monospace;">
  <thead>
    <tr>
      <th>Décimal</th>
      <th>Binaire</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>0</td><td>00000000</td></tr>
    <tr><td>1</td><td>00000001</td></tr>
    <tr><td>2</td><td>00000010</td></tr>
    <tr><td>3</td><td>00000011</td></tr>
    <tr><td>4</td><td>00000100</td></tr>
    <tr><td>5</td><td>00000101</td></tr>
    <tr><td>6</td><td>00000110</td></tr>
    <tr><td>7</td><td>00000111</td></tr>
    <tr><td>8</td><td>00001000</td></tr>
    <tr><td>9</td><td>00001001</td></tr>
    <tr><td>10</td><td>00001010</td></tr>
    <tr><td>11</td><td>00001011</td></tr>
    <tr><td>12</td><td>00001100</td></tr>
    <tr><td>13</td><td>00001101</td></tr>
    <tr><td>14</td><td>00001110</td></tr>
    <tr><td>15</td><td>00001111</td></tr>
    <tr><td>16</td><td>00010000</td></tr>
    <tr><td>17</td><td>00010001</td></tr>
    <tr><td>30</td><td>00011110</td></tr>
    <tr><td>31</td><td>00011111</td></tr>
    <tr><td>32</td><td>00100000</td></tr>
    <tr><td>33</td><td>00100001</td></tr>
    <tr><td>34</td><td>00100010</td></tr>
    <tr><td>63</td><td>00111111</td></tr>
    <tr><td>64</td><td>01000000</td></tr>
    <tr><td>65</td><td>01000001</td></tr>
    <tr><td>126</td><td>01111110</td></tr>
    <tr><td>127</td><td>01111111</td></tr>
    <tr><td>128</td><td>10000000</td></tr>
    <tr><td>129</td><td>10000001</td></tr>
    <tr><td>130</td><td>10000010</td></tr>
    <tr><td>191</td><td>10111111</td></tr>
    <tr><td>192</td><td>11000000</td></tr>
    <tr><td>193</td><td>11000001</td></tr>
    <tr><td>223</td><td>11011111</td></tr>
    <tr><td>224</td><td>11100000</td></tr>
    <tr><td>225</td><td>11100001</td></tr>
    <tr><td>239</td><td>11101111</td></tr>
    <tr><td>240</td><td>11110000</td></tr>
    <tr><td>241</td><td>11110001</td></tr>
    <tr><td>247</td><td>11110111</td></tr>
    <tr><td>248</td><td>11111000</td></tr>
    <tr><td>249</td><td>11111001</td></tr>
    <tr><td>251</td><td>11111011</td></tr>
    <tr><td>252</td><td>11111100</td></tr>
    <tr><td>253</td><td>11111101</td></tr>
    <tr><td>254</td><td>11111110</td></tr>
    <tr><td>255</td><td>11111111</td></tr>
    <tr><td>256</td><td>100000000</td></tr>
  </tbody>
</table>
</details> 

on peut coder 2<sup>8</sup> = 256 valeurs différentes sur un octet.  
ces valeurs vont de
```
0 (en décimal) = 00000000 (en binaire)
255 (en décimal) = 11111111 (en binaire)
```

la table de vérité de l'opérateur binaire ET est la suivante :
```
0 ET 0 = 0
0 ET 1 = 0
1 ET 0 = 0
1 ET 1 = 1
```

par exemple :
```
9 ET 3 = 1, car :
6 = 1001
3 = 0011
1 = 0001
```

# la base sur les réseaux

lorsque plusieurs appareils (ordinateurs, téléphones, imprimantes, ...) veulent communiquer entre eux, ils doivent utiliser des **protocoles de communication**.  
parmi ces protocoles, on retrouve **TCP/IP** (aussi appelé "la suite des protocoles Internet").

chaque appareil connecté est appelé un **hôte**.  

les données à envoyer sont divisées en **paquets**.  

**IP** est le protocole d'adressage (&rarr; c'est la couche réseau dans le modèle de la communication).  
il utilise les adresses des hôtes du réseau (les fameuses **adresses IP**) pour adresser correctement chaque paquet transmis.  
IP assure que les paquets arrivent à la bonne destination, mais il ne garantit ni leur ordre ni leur fiabilité.

**TCP** est le protocole de contrôle des transmissions (&rarr; c'est la couche transport dans le modèle de la communication).  
il établit une connexion entre chaque expéditeur et récepteur puis il vérifie que les paquets sont bien reçus (sinon, il les retransmet) et qu'ils sont dans le bon ordre (sinon, il les reclasse).

chaque hôte doit avoir une adresse IP unique.  

ici, les adresses IP sont toutes codées sur 4 octets (c'est de l'IPv4).  
donner une adresse IP, c'est donner la valeur de ses 4 octets en décimal. (par exemple : 128.255.0.1)

plusieurs hôtes forment localement un **sous-réseau**.  

dans un sous-réseau, tous les hôtes partagent la même **adresse de sous-réseau** et, généralement, le même **masque de sous-réseau**.  
l'adresse de sous-réseau peut s'obtenir à partir de l'adresse IP d'un hôte en binaire, en lui appliquant son **masque de sous-réseau** (en binaire aussi). cela consiste à ne garder que les bits de l'adresse IP où le masque est à 1.  
exemple :
* adresse IP : `104.198.241.125` (en décimal)  
= `01101000.11000110.11110001.01111101` (en binaire)
* masque de sous-réseau : `255.255.255.128` (en décimal)  
= `11111111.11111111.11111111.10000000` (en binaire)

    &rarr; adresse du sous-réseau : `01101000.11000110.11110001.00000000`

c'est équivalent de dire que l'adresse du sous-réseau s'obtient en faisant l'opération binaire ET pour chaque entre l'adresse IP et le masque de sous-réseau. on a :

un masque est toujours de la forme : "un certain nombre de 1" suivi de "un certain nombre de 0". par exemple : 111111100000.  
on peut le donner sous forme binaire, décimale ou CIDR (`/` + le nombre de 1 au début du masque). par exemple, sur 8 bits :
* en décimal : 192
* en binaire : 11000000
* en CIDR : /2

autre exemple, avec un masque /26, on sait que les 26 premiers bits de l'adresse IP indiquent l'adresse du sous-réseau. sachant que l'adresse IP d'un hôte est codée sur 4 octets (= 32 bits), on sait donc que les 6 derniers bits (= 32 - 26) indiquent l'adresse de cet hôte au sein de ce sous-réseau.  

on observe que choisir un gros masque (111111111111111111100 par exemple), c'est augmenter le nombre de sous-réseaux possibles au détriment du nombre d'hôtes par sous-réseau.

dans un sous-réseau, il faut que toutes les adresses soient dans la même plage de valeurs. par exemple, sur 4 bits :
* si le masque est 0000, il n'y a qu'un sous-réseau possible. les adresses IP peuvent être entre 0 et 15.
* si le masque est 1000, il peut y avoir 2 sous-réseaux. dans un de ces sous-réseaux, les adresses IP sont soit toutes entre 0 et 7 (elles sont de la forme 0xxx en binaire), soit toutes entre 8 et 15 (elles sont de la forme 1xxx en binaire).
* si le masque est 1100, il peut y avoir 4 sous-réseaux. les plages d'adresses IP sont :
  * entre 0 et 3 (de la forme 00xx en binaire)
  * entre 4 et 7 (de la forme 01xx en binaire)
  * entre 8 et 11 (de la forme 10xx en binaire)
  * entre 12 et 15 (de la forme 11xx en binaire)

on observe qu'augmenter le masque d'un bit revient à chaque fois à :
* multiplier le nombre de plages d'adresses IP par 2 (c'est-à-dire multiplier le nombre maximal de sous-réseau par 2)
* diviser le nombre maximal d'hôtes par sous-réseau par 2.

attention, il faut faire la différence entre la plage des adresses possible et les valeurs effectivement possibles. lorsque je dis qu'une adresse IP doit être dans la plage de valeurs entre `min` et `max`, je sous-entends qu'elle n'est ni à `min` ni à `max`. en effet, l'adresse `min` fait déjà référence à l'adresse du sous-réseau et l'adresse `max` est l'adresse de diffusion dans ce sous-réseau.

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

masque : 192 = 1100 0000
plages : 0 → 63, 64 -> 127, 128 -> 191, 192 -> 255
adresse IP : 0100 0010 = 66
adresse du sous réseau : 0100 0000 = 64

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
