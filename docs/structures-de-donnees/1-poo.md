#	Programmation orientée objet

!!! abstract "Cours" 
    La **programmation orientée objet**, ou **POO**, consiste en la définition et l’interaction de briques logicielles appelées objets ; un objet représente un concept, une idée ou toute entité du monde physique (une voiture, une personne, etc.).

Chaque objet possède une structure interne et un comportement, et il sait interagir avec ses pairs. Il s'agit donc de représenter ces objets et leurs relations.
Exemple de langages orientés objets : Java, Javascript C++, Python, PHP

Quelques définitions :
!!! abstract "Cours" 
    La classe est le "moule" à partir duquel des objets d’un même type peuvent être créés en mémoire, comprenant:

    - les données communes aux objets de cette classe : les **attributs**. Les valeurs des attributs seront contenues dans les objets issus de la classe.
    - les actions qui s’appliquent à ces objets : les **méthodes**.

    Une fois la classe définie (le moule), on peut fabriquer autant d’exemplaires similaires : les objets, par un processus appelé l'instanciation. Tout objet est une instance d'une classe. 

Exemple :
Imaginons un collectionneur de vielle voiture qui possède une Citroen 2CV avec 152 856 km (`voiture_1`), une Peugeot Dauphine avec 75 254 km (`voiture_2`), etc.

![Instanciation d'une classe d'objets Voiture](assets/1-instanciation-classe-voiture-light-mode.png#only-light){width="80%"}
![Instanciation d'une classe d'objets Voiture](assets/1-instanciation-classe-voiture-dark-mode.png#only-dark){width="80%"}

##	Les classes et objets

Créons la classe Voiture :   
!!! tip "PEP 8" 
    Les noms de classes s’écrivent en CamelCase [https://www.python.org/dev/peps/pep-0008/#class-names(https://www.python.org/dev/peps/pep-0008/#class-names)
  
``` py
class Voiture:
    pass
```


Notre classe `Voiture` est une sorte « d'usine à créer des voitures ». Il est maintenant possible de créer autant d'objets que l'on désire avec cette classe, créons nos deux premières voitures, c'est-à-dire deux instances de la classe `Voiture` :

``` py
voiture_1 = Voiture()
voiture_2 = Voiture()
```

##	Les attributs

Pour l’instant notre classe est juste une coquille vide. Il est possible de rajouter des caractéristiques à une instance en définissant ses attributs, par exemple : 

``` py
>>> voiture_1 = Voiture()
>>> voiture_1.marque = "Citroen"
>>> voiture_1.modele = "2 CV"
>>> voiture_1.km = 55000
```

et ensuite de les lire ainsi :

``` py
>>> voiture_1.marque
'Citroen'
```

Mais l’attribut `marque` n’existe pas pour `voiture_2` : 

``` py
>>> voiture_2.marque
Traceback (most recent call last):
  File "<interactive input>", line 1, in <module>
AttributeError: 'Voiture' object has no attribute 'marque'
```

##	Constructeur

La création d’un nouvel objet avec l’instruction `voiture_1 = Voiture()` appelle une méthode particulière nommée `__init__`. C’est le **constructeur** de la classe. Il est possible de le modifier pour définir des attributs pour toutes les instances de `Voiture` dès leur instanciation :


``` py
class Voiture:
    def __init__(self):
        self.marque = ""
        self.modele = ""
        self.km = 0
```

Le paramètre `self` représente l’objet qui est instancié.

Toutes les instances de Voiture possèderont ces attributs, mais les valeurs seront différentes pour chaque instance qui pourra évoluer de façon indépendante.

``` py
>>> voiture_1 = Voiture()
>>> voiture_1.modele
''
>>> voiture_1.modele = "2 CV"
>>> voiture_1.modele 
```

Avec ce constructeur, tous les objets sont créés avec les attributs initiés à la même valeur (`""` ou `0`). Ce n’est pas toujours pratique. 
La méthode `__init__` est une méthode comme les autres, elle peut avoir des paramètres,  par exemple la marque et le modèle et mettre km par défaut à 0 si ce n’est pas renseigné.

``` py
class Voiture:
    """ 
    Classe d’objets représentants des voitures de collection 

    Attributs:
    marque (str): la nom de la marque de la voiture
    modele (str): le modèle de la voiture
    km (int): les km parcourus par la voiture
    """

    def __init__(self, ma, mo, k=0):
        self.marque = ma
        self.modele = mo
        self.km = k
```

L’instruction `Voiture('Citroen', '2 CV')` appelle le constructeur  `__init__`  créant ainsi un nouvel objet `Voiture` en lui donnat les valeurs de ses attributs `'Citroen'` et `'2 CV'`.

``` py
>>> voiture_1 = Voiture('Citroen', '2 CV')
>>> voiture_1.modele
'2 CV'
>>> voiture_1.km
0
```

##	Les méthodes

Définir une classe c’est aussi définir les comportements communs aux objets de la classe : ce sont les **méthodes**. Les méthodes sont des fonctions définies dans une classe. Nous avons déjà vu la méthode `__init__` appelée à l’instanciation. On peut ajouter d’autres méthodes dans la classe `Voiture`.

!!! abstract "Cours" 
    Les méthodes prennent toujours comme **premier paramètre le mot réservé `self`** de façon à désigner l’objet sur lequel va s’appliquer la méthode.

Par exemple, on veut définir la fonction roule(k) qui ajoute des k kilomètres quand la voiture roule :

``` py
class Voiture:
    """ 
    Classe d’objets représentants des voitures de collection 

    Attributs:
    marque (str): la nom de la marque de la voiture
    modele (str): le modèle de la voiture
    km (int): les km parcourus par la voiture
    """

    def __init__(self,ma, mo, k=0):
        self.marque = ma
        self.modele = mo
        self.km = k

    def roule(self, k):
        self.km = self.km + k
```

Pour utiliser une méthode de la forme `nom_methode(self, param1, param2..)` sur un objet `nom_objet`, il faut écrire : `nom_objet.nom_methode(param1, param2 ,…)`. 

!!! abstract "Cours" 
    `self` est toujours le premier paramètre d’une méthode mais il n’est pas présent entre les paramètres lors de l’appel.

Utilisons la méthode `roule(self, k)` :

``` py
>>> voiture_1 = Voiture('Citroen', '2 CV')
>>> voiture_1.km
0
>>> voiture_1.roule(10000)
>>> voiture_1.km
10000
```

Ici `voiture_1.methode roule(self, k)` est exécuté avec `voiture_1` à la place de `self` et `10000` à la place de `k`.

Notons aussi qu’une méthode peut renvoyer une valeur. Par exemple : 

```
class Voiture:
    """ 
    Classe d’objets représentants des voitures de collection 

    Attributs:
    marque (str): la nom de la marque de la voiture
    modele (str): le modèle de la voiture
    km (int): les km parcourus par la voiture

    Méthodes:
    roule(km): ajoute des km parcourus
    revision(): renvoie le nombre de km restant avant la prochaine revision des 15000
    """

    def __init__(self,ma, mo , k=0):
        self.marque = ma
        self.modele = mo
        self.km = k

    def roule(self, km):
        self.km = self.km + km

    def revision(self):
        return 15000 - self.km % 15000

>>> voiture_1 = Voiture('Citroen', '2 CV')
>>> voiture_1.roule(20000)
>>> voiture_1.revision()
10000
```

Il existe en Python quelques méthodes particulières. Comme `__init__()`, leur nom est entouré de deux paires de blancs soulignés. Par exemple on peut tester `dir(list)` dans la console pour observer les méthodes du type `list`.

Les paires de blancs soulignés indiquent que ces méthodes ne sont pas appelées directement  (on dit qu’elles sont privées) mais plutôt par le biais de fonctions particulières.
-	`__init__(self)` est appelée à l’instanciation par `nom_objet = nom_classe()`.
-	`__str__(self)` est appelée par la fonction `print()`. La valeur renvoyée par `__str__()` sera affichée quand on fera `print(nom_objet)` ou bien la chaîne de caractère renvoyée par `str(nom_objet)`.
    ```
    def __str__(self):
        return self.modele + ' '+ self.marque
    ```
    Noter l’utilisation de `return` et non de `print()` dans la définition de la méthode `__str__(self)`.

    ``` py
    >>> print(voiture_1)
    2 CV Citroen
    ```

-   `__len__(self)` est appelée par `len(nom_objet)`.
-   `__add__(self, other)` pour ajouter deux objet avec le signe « `+` »; `__mul__(self, other)` pour les multiplier avec « `*` »; `__lt__(self, other)` pour comparer avec « `<` », etc. 

##	Alias

Lorsqu’on lie une variable comme `voiture_1` à un objet par `voiture_1 = Voiture('Citroen', '2 CV')`, la variable ne contient pas l’objet, mais une référence à l’objet, c’est-à-dire l’adresse mémoire de l’objet. Dès lors, deux noms de variables peuvent faire référence au même objet (des alias). On peut accéder ou modifier l’objet par l’un ou l’autre. Cette possibilité mène à de nombreuses erreurs de programmation.

``` py
>>> voiture_2 = Voiture('Peugeot','Dauphine')
>>> v = voiture_2
```

On peut constater tout simplement que les deux variables pointent sur le même objet :
```
>>> voiture_2
<__main__.Voiture object at 0x02E102C8>
>>> v
<__main__.Voiture object at 0x02E102C8>
>>>
```

Et par conséquent : 
```
>>> voiture_2.km
0
>>> v.roule(50000)
>>> voiture_2.km
50000
```

##	Variable de classe

Nous avons défini une classe comportant des attributs et des méthodes. Les attributs sont déclarés à l’intérieur du constructeur et sont donc propres à chaque objet instancié de la classe. Ils sont sur le même moule mais ont des états différents. On appelle cela des **variables d’instance**. 

Dans certains cas, on veut qu’une variable soit commune à toutes les instances. Elles sont appelée **variables de classe** et permettent de définir des attributs valables pour toutes les instances de la classe.

Dans ce cas-là on déclare la variable en dehors du constructeur et on y accède sous la forme `NomClasse.NomVariable` :

``` py
class Voiture:
    total_voiture = 0

    def __init__(self,ma, mo, k=0):
        self.marque = ma
        self.modele = mo
        self.km = k
        Voiture.total_voiture += 1
```
puis :

``` py
>>> Voiture.total_voiture
0
>>> v=Voiture('PEUGEOT','DAUPHINE')
>>> Voiture.total_voiture
1
>>> w= Voiture('Citroen', '2 CV')
>>> Voiture.total_voiture
2
>>>
```

##	Encapsulation 

Admettons qu’on veuille garder en mémoire le total des km parcourus par toutes les instances de Voiture. On ferait :

``` py
class Voiture:
    total_voiture = 0
    total_km = 0

    def __init__(self,ma, mo, k=0):
        self.marque = ma
        self.modele = mo
        self.km = k
        Voiture.total_voiture += 1
        Voiture.total_km += k

    def roule(self, k):
        self.km=self.km + k
        Voiture.total_km += k
```

puis :

``` py
>>> Voiture.total_km
0
>>> v = Voiture('Peugeot','Dauphine', 20000)
>>> w = Voiture('Citroen', '2 CV')
>>> w.roule(30000)
>>> Voiture.total_km
50000
```

Jusqu’ici tout va bien. Mais que se passe-t-il si on change les km d’une instance de Voiture directement ?

``` py
>>> v.km = 30000
>>> Voiture.total_km
50000
```

La variable de classe `total_km` n’est plus correcte ! Pour éviter ce problème, un objet ne devrait jamais permettre à ses utilisateurs de modifier son état (ses attributs) autrement que par des méthodes. 


!!! abstract "Cours" 
    Avec ses attributs et ses méthodes, toutes valeurs des variables et fonctionnalités d’un objet sont « enfermées » à l’intérieur d’un objet. On appelle cela l’**encapsulation**. 
    **L'encapsulation** crée une sorte de boîte noire contenant en interne un mécanisme protégé (les attributs et méthodes sont dit **privés**) et en externe un ensemble de commandes qui vont permettre de la manipuler (dit **publics**), de telle sorte qu'il sera impossible d'altérer le mécanisme protégé en cas de mauvaise utilisation. 

En Python, un **simple blanc souligné** au début de nom de variable indique qu’un attribut est privé. Ici on écrirait `self._km`..

``` py
class Voiture:
    ...
    def __init__(self,ma, mo, k=0):
        self.marque = ma
        self.modele = mo
        self._km = k
        Voiture.total_voiture += 1
        Voiture.total_km += k

    def roule(self, k):
        self._km = self._km + k
        Voiture.total_km += k
    ...
```

Pour respecter le principe de l’encapsulation, on ne devrait plus lire ou écrire la valeur de l’attribut _km d’un objet Voiture directement hors de cet objet. 

!!! abstract "Cours" 
    Une classe doit fournir des méthodes (publiques) dédiées qui font l’interface avec l’extérieur :
    -	**accesseurs** (ou **getters** par convention leur nom commence par ***get**) les méthodes permettant d’obtenir la valeur d’un attribut, et
    -	**mutateurs** (ou **setters**, par convention leur nom commence par **set**) pour en modifier la valeur.

``` py 
class Voiture:
    total_voiture = 0
    total_km = 0

    def __init__(self, ma, mo, k=0):
        self.marque = ma
        self.modele = mo
        self._km = k
        Voiture.total_voiture += 1
        Voiture.total_km += k

    def get_km(self):
        return self._km

    def set_km(self, k):
        Voiture.total_km -= self.km        # on soustrait l’ancienne valeur de km
        self._km = k
        Voiture.total_km += k               # on rajoute la nouvelle valeur

    def roule(self, k):
        self._km = self._km + k
        Voiture.total_km += k
```

Noter que ce **simple blanc souligné** au début de nom de variable n’est une convention d’écriture entre programmeurs, elle n’est pas prise en compte par l’interpréteur et on peut toujours lire et modifier l’attribut. 

```
>>> v._km = 30000
```
Certains utilisent un **double blanc souligné** au début de nom de variable.  

``` py
class Voiture:
    def __init__(self, ma, mo, k=0):
        #...
        self.__km = k
        #...
```

Mais cette variable pourra toujours être lue ou modifiée par `nomobjet.__nomvariable` et a des effets indésirables[^1.1] :

[^1.1]: Il faudrait utiliser `v._Voiture__km` au lieu de `v.__km`. Cette utilisation est contestée (règle du « name mangling »).
 Voir PEP 8 « Generally, double leading underscores should be used only to avoid name conflicts with attributes in classes designed to be subclassed. Note: there is some controversy about the use of __names (see below). »


```
>>> v = Voiture('Peugeot','Dauphine', 20000)
>>> v.get_km())
20000
>>> v.__km = 30000
>>> v.__km
30000
>>> v.get_km())
20000
```

Pour aller encore plus loin (hors programme) une autre manière « Pythonesque » de respecter le principe d’encapsulation est d’utiliser des décorateurs pour transformer les attributs en propriétés (hors programme)[^1.2] .

[^1.2]: Une classe Voiture en utilisant des décorateurs Python :
        ``` py
        class Voiture:

            total_voiture = 0
            total_km = 0

            def __init__(self, ma, mo, k=0):
                self.marque = ma
                self.modele = mo
                self._km = k
                Voiture.total_voiture += 1
                Voiture.total_km += k

            # propriété km. Permet d'utiliser nom_objet.km
            @property     
            def km(self):
                return self._km	

            # setter de l'attribut km. Pour utiliser nom_objet.km = ….
            @km.setter         
            def km(self, k):
                Voiture.total_km -= self._km 
                self._km = k
                Voiture.total_km += k

            def roule(self, k):
                self._km=self._km + k
                Voiture.total_km += k

        v = Voiture('Peugeot','Dauphine', 20000)
        v.km = 30000
        ```




  
##	Héritage et polymorphisme (hors programme)

!!! abstract "Cours"
    L'**héritage** consiste à créer une **nouvelle classe (la classe fille) à partir d'une classe existante** (super classe ou classe mère).


Cela permet de définir de nouveaux attributs et de nouvelles méthodes pour la classe fille, qui s'ajoutent à ceux et celles héritées de la classe mère sans avoir à les réécrire.

Admettons que l’on veille créer un classe de voiture électrique qui a les propriétés de la classe `Voiture` plus un certain nombre de kWh pour 100 kms.

La définition de la classe fille mentionne la mère. La méthode `__init__` appelle le constructeur de la mère et permet d’ajouter des attributs. On pourrait aussi ajouter des méthodes propres à la classe fille.

``` py
class VoitureElectrique(Voiture):

    def __init__(self, ma, mo, k=0, kwh=0):
        Voiture.__init__(self, ma, mo, k)     # ou super().__init__()
        self.kwh = kwh
```

Créons une instance de `VoitureElectrique` : 

``` py
>>> t = VoitureElectrique('TESLA', 'S', kwh=18)
```

Toutes les méthodes de la classe mère s’appliquent à la fille :

``` py
>>> t.roule(1000)
>>> t.getKm()
1000
```

!!! abstract "Cours"
    Le **polymorphisme** permet de modifier le comportement d’une classe fille par rapport à sa classe mère.

Cela permet d’adapter le comportement des objets. Par exemple, créons une classe fille pour des voitures qui ne roulent plus, appelée `Epave` : 

``` py
class Epave(Voiture):

     # inutile de redéfinir __init__ on utilise le constructeur de la classe mère

    def roule(self, k):
        pass


>>> e = Epave('Trabant','601', 150000)
>>> e.roule(10000)
>>> e.get_km()
150000
>>>
```

