À la recherche du chiffre perdu
===============================

Avec les quelques informations obtenues, il est possible d'explorer
plusieurs pistes pour tenter d'identifier le chiffrement utilisé. Les
nombres du chiffre ont très certainement été créés à l'aide de règles
mathématiques simples qui leurs confèrent les caractéristiques
observées. Un bon endroit pour débuter la recherche pour identifier le
chiffre est [dCode](https://www.dcode.fr/). Ce site une ressource
précieuse pour en apprendre plus sur les codes et le chiffrement. Il
offre non seulement des descriptions très détaillées de plusieurs
dizaines de chiffremements classiques, mais aussi des outils pour
encoder, décoder et briser certains d'entre eux.

Polybe
------

Nous avons probablement affaire à un chiffre de substitution ou de
transposition qui inclu des éléments additionnels pour rendre le
déchiffrage plus difficile. La méthode la plus amusante pour identifier
le chiffrement utilisé est de passer de longues heures à explorer les
différents chiffres classiques, à lire leurs descriptions et à chiffrer
et déchiffrer différents messages. C'est aussi la méthode demandant le
plus de temps. Si vous l'utilisez, vous finirez probablement par tomber
sur le chiffre de Polybe qui utilise le carré de Polybe, une grille de
5x5 associant chacune des lettres de l'alphabet à un nombre entre 11 et
55. La Table 4 montre un carré possible. Comme il y a 26 lettres à l'alphabet,
il faut en sacrifier une. Dans ce cas-ci on sacrifie le Z mais le J, V
ou W sont aussi fréquemment rejetés.

 Table 4 : Carré de Polybe.

               1       2       3       4       5
     1         A       B       C       D       E
     2         F       G       H       I       J
     3         K       L       M       N       O
     4         P       Q       R       S       T
     5         U       V       W       X       Y


Pour chiffrer un message à l'aide d'un carré de Polybe, il suffit de
trouver la lettre dans le tableau et de la remplacer par le nombre formé
par le numéro de ligne suivit par le numéro de colonne. Par exemple, la
lettre Q sera remplacée par le nombre 42.

Polybe sur les stéroïdes
------------------------

Afin de rendre la tâche plus difficile aux curieux, il est possible
d'utiliser une clé pour changer l'ordre des lettres de la grille. Le mot
utilisé doit avoir des lettres distinctes. On écrit les lettres de ce
mot secret au haut de la grille et on continue avec les lettres
restantes. Par exemple, avec la clé HACK on aurait le carré présenté en Table 5.

Table 5: Carré de Polybe avec la clé HACK.

             1       2       3       4       5  
     1       H       A       C       K       B
     2       D       E       F       G       I
     3       J       L       M       N       O
     4       P       Q       R       S       T
     5       U       V       W       X       Y


Le chiffre de Polybe présente une régularité dans les nombres utilisés,
ce qui le rend facilement identifiable puisque seuls les nombre 11, 12,
13, 14, 15, 21, 22, 23, 24, 25, 31, 32, 33, 34, 35, 41, 42, 43, 44, 45,
51, 52, 53, 54, 55 sont utilisables.

Polybe ou pas Polybe? Là est la question!
-----------------------------------------

Bien que le chiffre de Polybe présente des similitudes avec les
caractéristiques de notre message, les nombres possibles ne
correspondent pas. Nous avons donc affaire à un autre chiffre ou à une
variation du chiffre de Polybe avec une grille différente.

En s'éduquant un peu plus sur le chiffre de Polybe, on constate qu'il
est souvent associé au chiffre des Nihilistes qui est un surchiffrement
du carré de Polybe. On peut reconnaitre le chiffre des Nihilistes grâce
aux indices suivants:

-   Contient uniquement des nombres entre 22 et 110.

-   Ne contient aucun des nombres suivants:
    21, 31, 41, 51, 61, 71, 81, 91, 101.

-   Le chiffre est associé à une quelconque référence à la Russie.

Mini OSINT
----------

Les deux premières caractéristiques correspondent parfaitement au
message secret au bas du logo, mais une mention quelconque de la Russie
dans un épisode confirmerait le tout. Un peu de Google Fu ceinture
blanche (*logo site:securite.fm*) nous révèle qu'on mentionne le message
encodé dans le logo à l'épisode 0x017 (aux environs de la minute 40),
tel qu'illustré à la Figure 3. Lors de cet épisode Damien, toujours gourmand,
nous donne un indice: "Poutine"\... À moins qu'il fasse référence à un
autre type de "Putin", beaucoup moins digeste.

![L'épisode 0x017 mentionne le mystère du logo.](img/googlefu.png)

Figure 3 : L'épisode 0x017 mentionne le mystère du logo.

