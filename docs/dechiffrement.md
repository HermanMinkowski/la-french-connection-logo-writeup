Déchiffrement
=============

Il y a très peu de répétitions dans le message codé, 78 57 68 96 53 99
59 25 36 85 98 58 46 79 86 66 79 45 33 63 98 28 38 60 95, ce qui indique
que la clé de surchiffrement n'est probablement par trivialement courte
(1, 2 ou 3 caractères).

Longueur de la clé
------------------

La première étape est de déterminer la longueur de la clé de
surchiffrement ce qui nous donnera la période du chiffre. Un chiffre
aura une période de 4 si une clé de 4 caractères est répétée pour le
chiffrement puisque chaque bloc de 4 lettres utilisera la même clé.

Pour déterminer la longueur de la clé, on va créer des tableaux avec un
nombre de colonnes correspondant à la longueur de clé que l'on désir
tester. Par exemple, si on veut vérifier si une clé de 6 caractères est
possible, on doit créer la Table 7 de 6 colonnes et y placer le message chiffré
dans l'ordre.

Table 7 : Tableau pour tester si une clé de 6 caractères est possible.
  
     78   57   68   96   53   99
     59   25   36   85   98   58
     46   79   86   66   79   45
     33   63   98   28   38   60
     95                      

On doit créer un tableau de ce genre pour toutes les longueurs de clés
de surchiffrement qu'on veut tester. Dans notre cas, entre 1 et 25
colonnes.

Pour chaque colonne d'un tableau, on applique l'algorithme ci-dessous.
D'abord au chiffre des dizaines, puis au chiffre des unités. Si pour une
colonne, cet algorithme retourne faux soit pour le chiffre des dizaines
ou des unités, c'est qu'aucune addition n'est possible pour les
combinaisons de nombres dans la colonne. La clé de surchiffrement ne
peut donc avoir la longueur supposée.

Essentiellement, on vérifie que la différence entre le chiffre maximum
et minimum est plus petite que 5. Si ce n'est pas le cas, c'est
impossible qu'un même chiffre (entre 1 et 5) ait pu surencoder le
chiffre des unités ou dizaines. Par exemple, si les chiffres des unités
pour une colonne sont 2, 4, 7, 3, 4, la différence entre 7 et 2 est de
5. Or il est impossible de trouver deux chiffres tels que $x_1 + y = 7$
et $x_2 + y = 2$ où $1\leq x_i \leq 5$ et $1\leq y \leq 5$

-----
array $A \gets$ chiffres des unités ou dizaines

for all 𝑛 ∈ {0, . . . , 𝑎𝑟𝑟𝑎𝑦𝑙𝑒𝑛𝑔𝑡ℎ − 1} do

if 𝐴[𝑖] == 0 then

$A[i] \gets 10$

end if

end for

return max(A) - min(A) \< 5

-----

Si on revient à la Table 7, on constate que les chiffres des dizaines pour la
première colonne sont 7, 5, 4, 3, 9. On a une différence de 6 entre les
chiffres maximum et minimum, donc aucune clé de 6 caractères n'aurait pu
être utilisée.

Si on applique cette règle pour des tableaux de 2 à 25 rangées (à l'aide
d'un script Python maison), on obtient des longueurs de clés possibles
de 10, 20, 22, 23, 24 ou 25. Comme le message a 25 caractères, les clés
de longueur entre 20 et 25 sont considérées comme possibles puisque dans
ces cas la majorité des colonnes ne contiendront qu'un nombre. Par
contre, elles sont peu probables puisque si la longueur de la clé est
près de la longueur du message, on aura presque un chiffre de Vernam
(one-time pad) ce qui serait pratiquement impossible à décoder sans
connaitre la clé.

Dans ces circonstances, la longueur de la clé est fort probablement de
10.

Espace de clé
-------------

Une fois la longueur de la clé établie, on peut tenter de réduire
l'espace de clé. En effet, avec le chiffre des Nihilistes, ce ne sont
pas toutes les clés de 10 caractères qui sont possibles, mais seulement
un nombre réduit de celles-ci. Pour limiter le nombre de clés possibles
on a besoin de la Table 8 avec autant de colonnes que la longueur de la clé.

Table 8 : Tableau de 10 colonnes.


     78   57   68   96   53   99   59   25   36   85
     98   58   46   79   86   66   79   45   33   63
     98   28   38   60   95                      



Pour chacune des colonnes de ce tableau, on doit appliquer l'algorithme
suivant qui produira la liste des nombres possiblement utilisés pour
surchiffrer une colonne. Encore une fois, c'est une conséquence directe
de l'utilisation du carré de Polybe qui limite le nombre des unité ou
dizaines à un chiffre entre 1 et 5.

-----
array $col \gets$ une colonne du tableau

$dizaineMin \gets 1$

$dizaineMax \gets 5$

$uniteMin \gets 1$ 

$uniteMax \gets 5$

for all 𝑛 ∈ 𝑐𝑜𝑙 do

$unite \gets n \mod 10$

if $unite == 0$ then

$uniteMin \gets 5$

$uniteMax \gets 5$

else if $unite < 7$ then

$uniteMin \gets 1$

$uniteMax \gets unite - 1$

else

$uniteMin \gets unite - 5$

$uniteMax \gets 5$

end if

array $unitesPossibles \gets \{uniteMin, \dots, uniteMax\}$

$dizaine \gets floor(n/10) \mod 10$

if $dizaine == 0$ then

$dizaineMin \gets 5$

$dizaineMax \gets 5$

else if $dizaine < 7$ then

$dizaineMin \gets 1$

$dizaineMax \gets dizaine - 1$

else

$dizaineMin \gets dizaine - 5$

$dizaineMax \gets 5$

end if

array $dizainesPossibles \gets \{dizaineMin, \dots, dizaineMax\}$

end for

return $combinaisons(dizainesPossibles, unitesPossibles)$

-----

Si on applique cet algorithme à chaque colonne de la Table 8 , on obtient les
possibilités de la Table 9 pour chacun des caractères de la clé de
surchiffrement.

Table 9  : Espace de clé.

    Position      Possibilités

        1         43, 44, 45, 53, 54, 55
        2               13, 14, 15
        3         13, 14, 15, 23, 24, 25
        4                   45
        5                 41, 42
        6             44, 45, 54, 55
        7         24, 25, 34, 35, 44, 45
        8             11, 12, 13, 14
        9             11, 12, 21, 22
        10        31, 32, 41, 42, 51, 52


Même si tous ces calculs sont faisables à la main, un script Python peut
être une aide importante tant au point de vue temps, que santé mentale.

Des chiffres
------------

Pour ce chiffre, on a donc une clé de 10 caractères chaque caractère
ayant respectivement 6, 3, 6, 1, 2, 4, 6, 4, 4, et 6 possibilités. Le
nombre de combinaisons possibles est de
$6 \times 3 \times 6 \times 1 \times 2 \times 4 \times 6 \times 4 \times 4 \times 6 = 497664$.
Parmi ces combinaisons, beaucoup ne sont pas des mots. On pourrait
commencer par les exclure mais, au final, si la clé est aléatoire nous
avons 497664 clés à tester.

De plus, si on ne veut pas devoir valider manuellement chaque test de
déchiffrage, il faudrait automatiser le tout en comparant chaque bloc de
4 caractères d'une tentative de décodage aux
[quadrigrammes](https://github.com/torognes/enigma/blob/master/)
français et anglais (on présume que le message est dans une de ces deux
langues) qui sont au nombre d'environ 400000 chacun. Notons qu'il y a 22
blocs de 4 caractères possibles dans une séquence de 25 caractères.

Finalement, rien ne nous certifie qu'un carré de Polybe totalement
aléatoire n'a pas été utilisé pour la substitution initiale. Pour 26
lettres on a $26! \approx 4 \times 10^{26}$ carrés possibles.

On aura approximativement
$497644 \times 400000 \times 400000 \times 22 \times 4 \times 10^{26} \approx 7 \times 10^{44}$
tests à faire.

Ça fait beaucoup de chemins à explorer, il faut donc réduire encore plus
cet espace d'exploration en faisant plusieurs suppositions.

Suppositions
------------

Pour débuter, on fera les suppositions suivantes:

1.  La clé de surchiffrement est un mot. Probablement relié au podcast.

2.  Le carré de Polybe utilisé est un des quelques carrés les plus
    connus (avec les lettres de l'alphabet pratiquement dans l'ordre).

3.  La langue utilisée pour la clé et le message original est soit le
    français ou l'anglais.

4.  L'algorithme des Nihilistes utilisé pour chiffer le message n'a pas
    été modifié pour compliquer le déchiffrement.

Trouver la clé de surchiffrement
--------------------------------

Fort de ces suppositions, on peut enfin s'attaquer à la clé de
surchiffrement. On présume que le carré de Polybe le plus commun, où on
omet la lettre "J", a été utilisé (Table 10). Encoder le message avec ce carré
impliquerait l'utilisation des lettres de la Table 11 pour chiffrer la clé.

Table 10 : Carré de Polybe présumément utilisé.

             1       2       3       4       5
     1       A       B       C       D       E
     2       F       G       H       I       K
     3       L       M       N       O       P
     4       Q       R       S       T       U
     5       V       W       X       Y       Z


Table 11 : Lettres possibles pour la clé.
  
     1       2       3       4       5       6       7       8       9      10
     S       C       C       U       Q       T       I       A       A       L
     T       D       D               R       U       K       B       B       M
     U       E       E                       Y       O       C       F       Q
     X               H                       Z       P       D       G       R
     Y               I                               T                       V
     Z               K                               U                       W


Les 10 lettres les plus communes dans les mots français sont e, a, i, s,
n, r, t, o, l, u alors qu'en anglais il s'agit de e, t, a, o, i, n, s,
h, r, d. Ne conservons pour l'instant que les lettres les plus communes
pour les deux langues. En faisant ceci, on se rend presque immédiatement
compte, si on a déjà joué au scrabble ou fait des mots cachés, qu'on a
presque le mot SECURITÉ ou encore SECURITY (Table 12). Ce n'est très
certainement pas un hasard.

Table 12 : Lettres possibles épurées.

     1       2       3       4       5       6       7       8       9       10
     S               C       U               T       I       A       A       L
     T       D       D               R       U                            
     U       E       E                               O                    
                     H                                       D               R
                     I                               T                    
                                                     U                    


Une bonne façon de vérifier si on est sur la bonne voie est d'utiliser
cette clé de surchiffrement partielle pour décoder le message.
L'utilisation de [dCode](https://www.dcode.fr/) accélère grandement ce
genre de test puisqu'il permet de modifier rapidement soit le carré de
Polybe, soit la clé. Comme il nous manque quelques lettres à la clé pour
former un mot, on va les remplacer arbitrairement par la première lettre
de chaque colonne. On obtient la clé *SECURTTAAL*. En utilisant celle-ci
et la Table 10 pour tenter de déchiffrer le message on obtient
*PRZVAZEDKYZSNOTGPOGMZCKEX*.

On remarque un petit mot anglais et quelques bigrammes communs en
anglais dans le message partiellement décodé:\
**PR**Z**VA**ZEDKYZS**NOT**GPOGMZC**KE**X.

C'est un grand pas puisqu'on a identifié la langue du message original.
De plus, il y a plus de lettres "Z" qu'il ne faudrait dans ce message,
ce qui laisse croire qu'il y a un problème avec le carré de Polybe
utilisé. En consultant la liste des 10 lettres les plus communes en
anglais on remarque que le "I", la cinquième lettre la plus utilisée
dans cette langue, n'apparait jamais alors que le "Z" apparait à
quatre reprises. Si on inverse les positions du "I" et du "Z" dans
le carré de Polybe et qu'on tente à nouveau de décoder le message on
obtient un message partiellement décodé avec encore plus de mots et mots
partiels **PRIVA**I**E**DKY**ISNOT**GPOGMIC**KE**X.

À ce point, il est beaucoup plus facile d'essayer quelques autres clés
que de tenter de modifier le carré de Polybe. En essayant avec les clés
SECURITEAL et SECURITYAL on obtient:\

     SECURITEAL: PRIVATE?KYISNOTAP?GMICKEX
     SECURITYAL: PRIVATE?BIUYNNTQC?BHKVMVI?

La première tentative de clé, avec le mot en français, est clairement
mieux même si deux lettres sont impossibles à décoder avec le carré de
Polybe utilisé. Pour les deux dernières lettres de la clé, on peut soit
utiliser la force brute et tester toutes les combinaisons possibles ou
se souvenir (grâce à notre mini OSINT) que le site internet du podcast
est [securite.fm](https://securite.fm/).

Avec la clé de surchiffrement "SECURITEFM", on décode le message
*PRIVATE?EXISNOTAP?BLICKEX* qu'on peut deviner être
"PRIVATEKEXISNOTAPUBLICKEY". Cependant, le message n'est pas
totalement décodable avec cette clé. On peut facilement améliorer la
situation en inversant les lettres "X" et "Y" dans le carré de
Polybe pour obtenir la Table 13.

 Table 13 : Carré de Polybe final.

             1       2       3       4       5
     1       A       B       C       D       E
     2       F       G       H       Z       K
     3       L       M       N       O       P
     4       Q       R       S       T       U
     5       V       W       Y       X       I


Avec cette clé et ce carré de Polybe, deux nombres dans notre séquence
de chiffres initiale ne peuvent être décodés 78 57 68 96 53 99 59 **25**
36 85 98 58 46 79 86 66 79 **45** 33 63 98 28 38 60 95. Ils
correspondent aux lettres aux positions 8 et 18 du message. Avec la clé
de surchiffrement actuelle, le nombre 25 devrait être 10 puisqu'on
devrait soustraire 15 (à cause du "E") et le nombre 45 devrait être
30, pour la même raison.

Or 10 et 30 ne peuvent être obtenus avec la clé et le carré de Polybe
trouvés. Cependant, les nombres 25 et 45 correspondent aux lettres
manquantes "K" et "U". Ces deux lettres n'ont tout simplement pas
été surchiffrées avec la clé! Il s'agit soit d'une erreur involontaire
ou d'une tentative de rendre le déchiffrement du message plus difficile.
Au final, tous seront d'accord avec le message secret: "private key is
not a public key".
