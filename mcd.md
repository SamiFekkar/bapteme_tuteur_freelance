## Retour sur le MCD

Tu as bien identifié les différentes tables au vu de l'énoncé et tu as vu les associations qui les lient.
Les cardinalités sont globalement bonnes, mais certaines relations sont fausses :
* Entre la table USER(1, 1) et PRODUCT(1, 1), si on se pose la question "_Combien d'utilisateurs peuvent __like__ un produit au minimum et au maximum ?_", on trouve USER(0, N) : un utilisateur peut au minimum choisir de ne __like__ aucun produit, ou bien au maximum N produits.  
La même question pour les PRODUCT : "_Combien de produits peuvent être __like__ au minimum par un utilisateur ?_", on trouve PRODUCT(0, N): un produit peut être __like__ par aucun utilisateur, ou bien par N utilisateurs.
Les cardinalités pour USER et PRODUCT sont donc : __USER(0, N) - PRODUCT(0, N)__.  
Donc, comme tu l'avais noté, il y a bien une relation _many to many_.  
Dans ce cas-là, il faudrait créer une table de liaison avec comme clé primaire (primary key) les clés étrangères (foreign key) de chacune des tables (USER et PRODUCT).

* Entre la table ORDER(1, N) et PRODUCT(0, N), les cardinalités sont bonnes, il y a donc une relation _many to many_. Ainsi, comme pour les tables que nous venons de voir sur le point précédent, il faudrait créer une table de liaison entre ORDER et PRODUCT.

* Pour les autres relations ADRESS(1, 1) - USER(0, N) et ORDER(1, 1)- USER(0, N), il est nécessaire de mettre le _userId_ comme clé étrangère (foreign key) puisque dans une relation de type (1, N) la clé primaire de la table (0, N) _ici USER_ migre vers la table (0, 1) ou (1, 1) et devient une clef étrangère.