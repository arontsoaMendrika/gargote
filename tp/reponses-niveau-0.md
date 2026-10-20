1. Schema remationnel
* categorie(**id**,libelle)
* plat(**id**,nom,prix,#id_categorie)
* commande(**id**,date_commande,numero_table)
* commande_ligne(**id**,**#id_commande**,**#id_plat**,quantite,prix_unitaire)

2. commande_ligne contient-elle une colonne prix_unitaire, alors que le prix est déjà dans plat car au cas ou les prix changent on changera directement dans la table commande_ligne au lieu de passer dans la table plat à chaque fois
exemple prenons 'Café' avec son prix 1000Ar dans la table plat si on change le prix du café en 1200Ar on le changera juste dans la table commande_ligne colonne prix_unitaire