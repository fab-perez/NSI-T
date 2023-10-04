# Structures linéaires : Listes

!!! abstract "Cours"
    Une **liste**[^3.1] est une structure abstraite de données constituée d’éléments d’un même type, chacun possédant une position (ou rang). 

    Une liste peut être **éventuellement vide**. Une liste est évolutive: on peut  **ajouter** ou **supprimer** n’importe lequel de ses éléments. 
    
    Une liste non vide comprend de 2 parties :

    -	La **tête** (notée *car*[^3.2]), qui est le **dernier élément ajouté** à la liste;
    -   La **queue** (note *cdr*[^3.3] ), qui contient le reste de la liste, elle-même une liste .

    La **longueur** de la liste est le nombre d’éléments composant la liste. Une liste de longueur zéro est une liste vide.


À noter le caractère récursif de la définition où la queue d'une liste est une liste.


[^3.1]: Le langage de programmation Lisp (inventé par John McCarthy en 1958) a été un des premiers langages de programmation à introduire cette notion de liste (Lisp signifie "list processing").

[^3.2]: *contents of address register*
[^3.3]: *contents of decrement register*



## Interface 
Les principales primitives  sur les listes :

-	`creer() → liste` : constructeur d’une liste vide.
-	`est_vide() → bool` : vérification si une liste est vide ou non.
-	`inserer_tete(element)` : insertion d'un élément en tête.
-	`supprimer_tete() →  element` : suppression de l’élément de tête
-	`taille() → int` : nombre d'éléments dans la pile.
-	`tete() →  element` : lire le premier élément de la liste
-	`queue() → liste` : accès au reste de la liste

Eventuellement on trouve aussi :

-   `insérer(element, i)` : insertion d'un élément en ième position.
-   `lire(i) → element` : accès au ième élément de la liste (get)


##	Implémentation

La liste est un type abstrait, son implémentation peut se faire sous différentes formes, en particulier les tableaux et les listes chaînées.

:warning: **Ne pas confondre type abstrait de données liste avec le type `list` de Python**. Le type `list` Python est en réalité un **tableau dynamique**, ce n’est qu’une forme d’implémentation particulière de la structure de données abstraite liste mais ce n’est pas la seule.

###	Implémentation récursive avec des tuples imbriqués

Une liste peut être définie comme :

-	soit un tuple vide : () si la liste est vide ;
-	soit un couple  formé de la tête de la liste et de sa queue : (car, cdr)

Exemple : une liste avec les éléments 'd', 'c', 'b', 'a'  s’écrit en Python `('d', ('c',( 'b',( 'a', ()))))`. `'d'` est la tête et `(('c', ('b', ('a', ())))` est la queue, c’est-à-dire la liste 'c', 'b', 'a'.

Commençons par les primitives pour créer une liste vide et insérer des éléments en tête de liste :

``` py
def creer(): return ()  # renvoie une tuple vide
def est_vide(L): return L == ()
def inserer_tete(L, e): return (e, L)  

L = creer()
L = inserer_tete(L, 'a')
L = inserer_tete(L, 'b')
L = inserer_tete(L, 'c')
L = inserer_tete(L, 'd')
```

Ajoutons quelques primitives supplémentaires :

``` py
def tete(L): return L[0]
def queue(L): return L[1]
```

La taille est calculée de façon récursive :
``` py
def taille(L):
    if est_vide(L): return 0
    else: return 1 + taille(queue(L))
```

l'affichage est aussi récursif :
``` py
def afficher(L):
    if est_vide(L): print('')     
    else:
        print(tete(L), end=' - ' ) 
        afficher(queue(L))
```

ainsi que la recherche calculéé de façon récursive :

``` py
def chercher(L, e):
    if est_vide(L): return False 
    elif tete(L) == e: return True 
    else: return chercher(queue(L) , e) 
```

###	Implémentation avec un tableau de taille fixe

Un **tableau** en informatique est en général représenté par une suite de "cases mémoire" de mêmes tailles contenant les différents éléments du tableau.  Une plage d'adresses mémoire est réservée afin de stocker tous les éléments.

![Cases memoire d'un tableau](assets/3-liste-tableau-cases-memoire-light-mode.png#only-light){width="50%"}
![Cases memoire d'un tableau](assets/3-liste-tableau-cases-memoire-dark-mode.png#only-dark){width="50%"}

Cette représentation présente 2 avantages :

-	pour un tableau sans case vide, elle est très compacte, puisqu'elle se contente de stocker les données ;
-	l'accès un élément du tableau par son $indice$ s'effectue relativement rapidement en temps constant. Son  adresse se calcule facilement:
    $adresseElement = adresseTableau + indice \times  tailleCase$

On peut créer en Python une liste sous forme d’un tableau de taille fixe n+1 en utilisant une variable de type `list`:
•	la première case du tableau contient le nombre d’éléments de la liste ;
•	les cases suivantes (d’indice `1` à `n`) contiennent les éléments de la liste ou `None`.

Exemple : une liste de taille 5 avec les éléments `'c'`, `'b'`, `'a'`  se présentera sous la forme  `[3, 'c', 'b', 'a', None, None]`.

Créons l’interface d’une telle liste :

``` py
def creer_liste(longueur):
    '''(int) - > list
    Cree une liste sous forme de tableau de taille fixe
    La première case du tableau contient le nombre d’éléments de la liste
    Les cases suivantes (d’indice 1 à n) contiennent les éléments de la liste ou None
    '''
    L = [None] * (longueur + 1)
    L[0] = 0
    return L
```

On peut définir une fonction pour insérer un élément en tête de liste (***U**pdate*) :

``` py
def inserer_tete(L, elem):
    ''' Ajoute elem en tete de la liste L
    - L est une liste implémentée sous forme de tableau de taille fixe
    - elem est un element ajouté à la liste (de n'importe quel type)
    la fonction ne renvoie rien car L est modifé (le type list est muable)
    '''
    # verifions si la liste est pleine
    if L[0] == len(L) - 1: raise IndexError('La liste est déjà pleine')
    else:
        for i in range(L[0], 0, -1):
            L[i+1]= L[i]
        L[1] = elem
        L[0] += 1
```

A noter qu’il est inutile de renvoyer la valeur de `L` car c’est une variable de type `list`, donc muable.

``` py
inserer_tete(L, 'a')
inserer_tete(L, 'b')
inserer_tete(L, 'c')
```

Une fonction pour afficher la liste s'écrit :

``` py
def afficher(L):
    ''' affiche la liste L
    '''
    for i in range(1, L[0] + 1):
        print(L[i], end = "-")
    print("")
```

On peut rajouter une fonction pour supprimer la tête de la liste :

``` py
def supprimer_tete(L):
    ''' supprime la tete de la liste L
    la fonction ne renvoie rien car L est modifé (le type list est muable)
    '''
    # verifions si la liste est vide
    if L[0] == 0: raise IndexError('La liste est déjà vide')
    else:
        for i in range(1, L[0] ):
            L[i]= L[i+1]
        L[L[0]] = None
        L[0] -= 1
```
Testons le résultat :

``` py
L = creer_liste(5)
inserer_tete(L, 'a')
inserer_tete(L, 'b')
inserer_tete(L, 'c')
inserer_tete(L, 'd')
inserer_tete(L, 'e')
afficher(L)
supprimer_tete(L)
supprimer_tete(L)
supprimer_tete(L)
afficher(L)
```

On peut aussi ajouter des méthodes pour :

-	accéder au ième élément de la liste (get) ; 
-	insérer un élément en tête d’une liste ;
- 	insére un élément en ième position ;
-	etc.

Pour aller plus loin,  on peut écrire une classe d’objet Liste avec des méthodes similaire.
