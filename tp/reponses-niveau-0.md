1. Schema remationnel
* categorie(**id**,libelle)
* plat(**id**,nom,prix,#id_categorie)
* commande(**id**,date_commande,numero_table)
* commande_ligne(**id**,**#id_commande**,**#id_plat**,quantite,prix_unitaire)

2. commande_ligne contient-elle une colonne prix_unitaire, alors que le prix est déjà dans plat car au cas ou les prix changent on changera directement dans la table commande_ligne au lieu de passer dans la table plat à chaque fois
exemple prenons 'Café' avec son prix 1000Ar dans la table plat si on change le prix du café en 1200Ar on le changera juste dans la table commande_ligne colonne prix_unitaire



3. quand on supprime la commande les lignes de commandes sont effaces automatiquemnt car cela utilise id_commande et cela aussi est provoquee par l'instruction ON DELETE CASCADE qui en est responsable

4.donnees absurdes:
````
INSERT INTO commande_ligne (id_commande, id_plat, quantite, prix_unitaire) VALUES
    (1, 1, 1, -2000);
````



5. Pour la requête **b** le code est 201 pour dire que c'est crée , ce n'est pas 200 car c'est une creation avec POST

6. Pour la requête **d**, PostgreSQL bloque la suppression 
la ligne de code qui transforme ce blocage en reponse 409 est dans  App\Controllers\Api dans Plats.php dans la fonction delete($id=null)
````
catch (\Throwable $e) {
            // Le plat apparaît dans des commandes : la clé étrangère bloque la suppression.
            return $this->erreur('Ce plat figure déjà dans des commandes, il ne peut pas être supprimé.', 409);
        }
````


7. curl -i -X POST "http://localhost:8080/api/commandes" \
  -H "Content-Type: application/json" \
  -d '{
    "numero_table": 6,
    "lignes": [
      {
        "id_plat": 4,
        "quantite": 2
      },
      {
        "id_plat": 10,
        "quantite": 1
      }
    ]
  }'
