#	Conception physique : SGBD relationnel


!!! abstract "Cours"
    L’implémentation physique d'une base de données se fait dans un logiciel informatique appelé Système de Gestion de Bases de Données ou SGBD.

Un SGBD doit répondre aux objectifs suivants :
•	Indépendance physique
•	Indépendance logique
•	Accès aux données
•	Administration centralisée des données
•	Non redondance des données
•	Cohérence des données
•	Partage des données
•	Sécurité des données
•	Résistance aux pannes

Les SGBD les plus connus : MySQL, PostegreSQL, SQLite, Oracle, Microsoft SQL Server, MS Access

Dans un SGBD :
- 	les relations sont implémentées par des tables ;
- 	un tuple devient une **ligne** de la table ;
- 	un attribut devient une **colonne** de la table.

Il existe quelques différences entre relations et tables, par exemple :
- L’ordre des attributs dans une relation n’a pas d’importance alors que dans un SGBD les attributs d’une table ont un ordre.
- Une table dans un SGBD peut ne pas avoir de clé, alors qu’une relation a forcément une clé.

Dans la suite de ce chapitre nous utilisons le SGBD SQLite avec l’interface DB Browse. 