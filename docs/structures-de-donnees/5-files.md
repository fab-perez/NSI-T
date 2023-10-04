#	Structures linéaires : Files 


!!! abstract "Cours"
    
    En informatique, une **file** (en anglais ***queue***) est un type abstrait de données sur le principe « dernier arrivé, premier sorti » (ou **FIFO** pour ***First In, First Out***).

    Les premiers éléments ajoutés à la pile, ou **enfilés**, sont les premiers qui seront sortis, ou **défilés**.


Le fonctionnement ressemble à une file d'attente : les premières personnes qui arrivent dans la file sont les premières personnes qui en sortent. 


Ici aussi, les files trouvent de nombreuses applications en informatique :

-	En général, on utilise des files pour mémoriser temporairement des transactions qui doivent attendre pour être traitées.

-	Les serveurs d'impression, qui doivent traiter les requêtes dans l'ordre dans lequel elles arrivent, et les insèrent dans une file d'attente (ou une queue).

-	Certains moteurs multitâches, dans un système d'exploitation, qui doivent accorder du temps machine à chaque tâche, sans en privilégier aucune.

-	Un algorithme de parcours en largeur utilise une file pour mémoriser les nœuds visités.

-   etc.

## Interface

Voici les opérations communément utilisées pour manipuler des files :

- `creer() → file` : constructeur d’une file vide.
- `est_vide() → bool` : vérification si une file est vide ou non.
- `enfiler(element)` : ajouter un élément sur la file (*enqueue* en anglais).
- `défiler() → element` : enlèver un élément de la file et le renvoie (*dequeue* en anglais).
- `taille() → int` : nombre d'éléments dans la file.

Exemples :

Soit une file `F` composée des éléments suivants : 12, 14, 8, 7, 19 et 22 (le premier élément rentré dans la file est 22 ; le dernier élément rentré dans la file est 12). Pour chaque exemple ci-dessous on repart de la file d'origine :
•	`enfiler(F,42)` la file `F` est maintenant composée des éléments suivants : 42, 12, 14, 8, 7, 19 et 22 (le premier élément rentré dans la file est 22 ; le dernier élément rentré dans la file est 42)
•	`défiler(F)` la file F est maintenant composée des éléments suivants : 12, 14, 8, 7, et 19 (le premier élément rentré dans la file est 19 ; le dernier élément rentré dans la file est 12)
•	si on applique `défiler(F)` 6 fois de suite, `est_vide(F)` renvoie vrai.
•	après avoir appliqué `défiler(F)` une fois, `taille(F)` renvoie 5.


## Implémentation
La liste est un type abstrait, son implémentation peut se faire sous différentes formes,  par exemple en reprenant l’implémentation d’une Pile avec une variable de type list il suffit de modifier `pop()` en `pop(0)` pour écrire la méthode `defiler()`.

``` py
    def defiler(self):
        if self.est_vide(): raise IndexError("la file est vide")
        return self.pile.pop(0)
```

###	Implémentation en utilisant deux piles

Ici on propose une autre approche, en utilisant deux piles.
