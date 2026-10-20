1. Schema remationnel
* categorie(**id**,libelle)
* plat(**id**,nom,prix,#id_categorie)
* commande(**id**,date_commande,numero_table)
* commande_ligne(**id**,**#id_commande**,**#id_plat**,quantite,prix_unitaire)

