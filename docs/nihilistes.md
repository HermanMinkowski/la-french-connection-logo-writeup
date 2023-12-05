Chiffre des Nihilistes
======================

Rendu célèbre par son utilisation par les nihilistes russes du 19ième
siècle. Ce chiffre est simple à mémoriser et permet de transmettre un
message de plusieurs façons. Par exemple, les prisonniers russes
transmettaient des messages de ce type en cognant sur les murs de leurs
cellules un nombre de fois qui correspondait à la rangée puis à la
colonne de chaque lettre.

Fonctionnement
--------------

Le fonctionnement du chiffre des Nihilistes est simple:

1.  On choisit un carré de Polybe, avec les lettres potentiellement dans
    le désordre grâce à une clé convenue d'avance. Par exemple, le carré
    de la Table 5.

2.  On encode le message avec la grille. Chaque lettre se voit attribuée
    un chiffre correspondant à une ligne et une colonne. Le message
    "MESSAGESECRET" deviendrait par exemple: 33 22 44 44 12 24 22 44
    22 13 43 22 45.

3.  On choisit une clé de surchiffrement et on l'encode avec le carré de
    Polybe. Si on choisit "PLANET" comme clé, on aura 41 32 12 34
    22 45.

4.  On réécrit la clé encodée autant de fois que nécessaire sous le
    message encodé et on additionne les deux nombres comme dans la Table 6.

Table 6 : Surchiffrement.

       M    E    S    S    A    G    E    S    E    C    R    E    T
      ---- ---- ---- ---- ---- ---- ---- ---- ---- ---- ---- ---- ----
       33   22   44   44   12   24   22   44   22   13   43   22   45
       41   32   12   34   22   45   41   32   12   34   22   45   41
       74   54   56   78   34   69   63   76   34   47   65   67   86


On obtient alors un chiffrement par substitution auquel on additionne
une clé de façon répétée. Au final, on aura un chiffrement
polyalphabétique fractionné puisque deux lettres identiques peuvent être
encodées de façon différente selon leur position dans le message.

Vulnérabilités
--------------

Le chiffre des Nihilistes comporte de multiples vulnérabilités dont
celles ci-dessous:

-   La clé de surchiffrement est répétée. Quand le message chiffré est
    plus long que cette clé, on peut observer des similitudes entre les
    blocs de texte de même longueur que la clé.

-   Il y a un nombre limité de combinaisons pour les additions. Par
    exemple, le chiffre 80 ne peut être obtenu qu'avec les additions
    $25+55$ ou $35+45$.

-   Plus les nombres sont grands ou petits, plus les possibilités sont
    limitées. Par exemple, 22 ou 110 ne peuvent être obtenus que si la
    lettre encodée est la même que celle de la clé de surchiffrement et
    que cette lettre est soit dans le coin supérieur gauche ou le coin
    inférieur droit de la grille, respectivement.

-   Un nombre ayant un 0 à la position des unités indique que les
    nombres additionnés proviennent de la dernière colonne.

-   Similairement, un nombre ayant un 2 à la position des unités
    provient d'une addition de nombres de la première colonne.

-   Une fois la longueur de la clé identifiée et un espace de clé
    réduit, on peut trouver la clé (si c'est un mot), par déduction ou
    avec un dictionnaire.

-   Une fois la clé de surchiffrement trouvée, le problème se réduit à
    un simple chiffre de substitution, un chiffre de Polybe.

La cryptanalyse du chiffre des Nihilistes sera grandement facilitée si
le message codé est long et/ou si on possède un autre message décodé qui
aurait été chiffré avec la même grille et la même clé de surchiffrement.
Malheureusement, dans le cas présent, on n'a aucun de ces deux éléments
facilitateurs.
