#	Structures linéaires : Files 


!!! abstract "Cours"
    
    En informatique, une **file** (en anglais ***queue***) est un type abstrait de données sur le principe « dernier arrivé, premier sorti » (ou **FIFO** pour ***First In, First Out***).

    Les premiers élément ajoutés à la file, ou **enfilés**, seront les premiers sortis, ou **défilés**.


Le fonctionnement est celui d'une **file d'attente** : les premières personnes qui arrivent dans la file sont ensuite les premières qui en sortiront. 


Ici aussi, les files trouvent de nombreuses applications en informatique, par exemple :

-	En général, on utilise des files pour mémoriser temporairement des transactions qui doivent attendre pour être traitées.

-	Les imprimantes qui traitent les demandes dans l'ordre dans lequel elles arrivent, et les insèrent dans une file d'attente.

-	L'ordonnanceur d'un système d'exploitation qui accorde du temps machine à chaque processus dans l'ordre où il arrive, sans en privilégier aucun.



## Interface

Les principales primitives constitant l'interface d'une file sont :

- `creer() → file` : construire d'une file vide.
- `est_vide() → bool` : vérifier si une file est vide ou non.
- `enfiler(element)` : ajouter un élément sur la file (*enqueue* en anglais).
- `défiler() → element` : enlèver un élément de la file et le renvoier (*dequeue* en anglais).
- `taille() → int` : renvoyer le nombre d'éléments dans la file.

Exemples :

Soit une file `F` composée des éléments suivants : 12, 14, 8, 7, 19 et 22 (le premier élément rentré dans la file est 22 ; le dernier élément rentré dans la file est 12). Pour chaque exemple ci-dessous on repart de la file d'origine :
•	`enfiler(F,42)` la file `F` est maintenant composée des éléments suivants : 42, 12, 14, 8, 7, 19 et 22 (le premier élément rentré dans la file est 22 ; le dernier élément rentré dans la file est 42)
•	`défiler(F)` la file F est maintenant composée des éléments suivants : 12, 14, 8, 7, et 19 (le premier élément rentré dans la file est 19 ; le dernier élément rentré dans la file est 12)
•	si on applique `défiler(F)` 6 fois de suite, `est_vide(F)` renvoie vrai.
•	après avoir appliqué `défiler(F)` une fois, `taille(F)` renvoie 5.


## Implémentation

###	avec le type `list` de Python

La liste est un type abstrait, son implémentation peut se faire sous différentes formes, par exemple en reprenant l'implémentation d'une Pile avec une variable de type `list` il suffit de modifier `pop()` en `pop(0)` pour écrire la méthode `defiler()`.

``` py
    def defiler(self):
        if self.est_vide(): raise IndexError("la file est vide")
        return self.pile.pop(0)
```

###	avec deux piles

Ici on propose une autre approche, en utilisant deux piles.
