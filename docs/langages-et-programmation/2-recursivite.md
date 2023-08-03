# Récursivité

##	Récursivité simple

Une fonction peut être appelée n’importe où dans un programme (après sa définition), y compris par elle-même.

!!! abstract "Cours" 
        Une fonction **récursive** est une fonction qui s'appelle elle-même[^2.1].

[^2.1]: Le mot "récursivité" en informatique a la même racine que "récurrence" utilisée pour les suites mathématiques.

Prenons pour exemple une fonction qui renvoie le produit de tous les nombres entiers entre 1 et $n$. Ce produit est appelé factorielle de $n$ et noté $n!$.

$n!  =  1  \times 2  \times 3  \times 4  \times ...  \times (n-1)  \times n$ 

Un programme itératif[^2.2]: peut s'écrire simplement avec un boucle `for` qui multiplie tous les entiers allant de `1` à `n` entre eux :

[^2.2]: Une structure de contrôle est dite "itérative" qaund elle exécute plusieurs fois une séquence d’instructions (boucles `for`, `while`).

``` py 
def fact(n):
    f = 1
    for i in range(1, n + 1):
        f = f * i
    return f
```

Mais il est aussi possible de remarquer que $n!  =  (n - 1)!  \times n$ et que $1!  =  1$, ce qui permet d'écrire un programme récursif suivant : 
 
``` py 
def fact(n):
    if n == 1:
        return 1
    return  fact(n-1) * n
```

On peut toujours transformer une fonction récursive en itérative et vice versa.


##	Importance de la clause d’arrêt

!!! abstract "Cours" 
        Une fonction récursive doit toujours comporter **une clause d’arrêt**, pour ne pas « boucler ». 

La fonction suivante :

``` py 
def fact(n):
    return fact(n-1) * n
```
ne s’arrêtera jamais car il manque une clause d’arrêt `if n == 1 : …` !

: warning: Il faut toujours prendre soin de bien définir la clause d’arrêt.  Ici que se passe-t-il si on appelle  `fact(5.1)` ou `fact(-1)`  ? On préfèrera peut-être  `if n <= 1: …` ou utiliser des assertions pour éviter ces cas.

En pratique un appel récursif doit obligatoirement comporter une **instruction conditionnelle** et une **variable de contrôle** : par exemple un entier naturel qui décroît strictement à chaque appel récursif jusqu'à atteindre la valeur d'un cas de base.


## Récursivité croisée, multiple

!!! abstract "Cours" 
        Dans certains cas, une fonction appelle une autre fonction qui elle-même appelle la première. C'est une **récursivité croisée**.

Par exemple pour tester si un nombre est pair ou impair (sans utiliser l'opérateur `%2`)

``` py
def pair(n):
    if n == 0: return True
    else: return impair(n-1)
def impair(n):
    if n == 0: return False
    else: return pair(n-1)
```

!!! abstract "Cours" 
        Il arrive aussi qu’une fonction s’appelle plusieurs fois, c'est une **récursivité multiple**.

Par exemple la suite de Fibonacci est définie par  u_0=0 , u_1=1 et pour n > 1 : u_n=u_(n-1)+ u_(n-2) .

``` py
def fib(n):
    if n < 2:return n
    return fib(n – 1) + fib(n - 2)
```

Si la récursivité est **plus élégante et facile** à lire qu’un programme itératif, on atteint très vite ses limites en complexités[^2.3] spatiale et temporelle[^2.4].

[^2.3]: Les mots "complexité" ou "coût" sont employés indifféremment.
[^2.4]: Attention à ne pas confondre les deux complexités : la complexité temporelle (ou en temps) mesure l’ordre de grandeur du nombre d’opérations élémentaires, la complexité spatiale (ou en espace) mesure l'espace mémoire requis par un programme.
