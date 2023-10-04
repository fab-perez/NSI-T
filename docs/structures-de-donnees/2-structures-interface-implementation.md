# Structures de données, interface et implémentation 

!!! abstract "Cours"
    Une **structure de données** ou type abstrait de données (TAD ) est un ensemble de données organisées et d’opérations sur ces données.

On parle de type abstrait car c’est une  "vue de l'esprit" permettant la manipulation de ces données par un algorithme sans rentrer dans les détails d'implémentation.  

Par exemple, on connait déjà les structures de données : 
- des entiers relatifs, munis des opérations: +, *, /, etc. ;
- des booléens, munis des opérations:  AND, OR ;
- des chaînes de caractères, munies des opérations: insertion, concaténation, etc.

!!! abstract "Cours"
    L'**interface** d'une structure de données abstraite est l'ensemble des opérateurs nécessaires à la manipulation de cette structure. 



L’utilisateur d’une structure de données n’a besoin de connaître que son interface, comme la partie visible d'un iceberg, qui lui offre toutes les opérations qu’il lui est possible de faire sur ces données, sans en connaître l'ensemble du fonctionnement interne qui lui est caché.


![L'interface comme partie emergée d'un iceberg](assets/2-interface-iceberg.png){width="50%"}
 
!!! abstract "Cours"
    L’interface d’une structure de données comporte un ensemble de fonctions de bases (appelées **primitives**) qui permettent entre autres de créer (***C**reate* ), lire (***R**ead*), écrire (***U**pdate*) ou supprimer (***D**elete*) (***CRUD*** en abrégé) une donnée. 

Pour une même interface, on peut avoir diverses implémentations de la structure de données, qui peuvent par exemple dépendre des choix ou du langage de programmation. 

!!! abstract "Cours"
    L’**implémentation** d’une  structure de données consiste à le "traduire"  dans un langage informatique (Python, Java). 

Certains types abstraits ne sont pas forcément implémentés dans un langage donné, si le programmeur veut utiliser ce type abstrait, il faudra qu'il le programme par lui-même en utilisant les "outils" fournis par son langage de programmation.
