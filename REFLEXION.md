## TP3

**1. Quel est le meilleur modèle ? Peux-tu le prouver ?**
Oui. Dans MLflow, je trie les runs par f1. Essai 1 et Essai 3 sont à égalité (f1 = 0.889),
Essai 2 est le plus faible (f1 = 0.333). Je choisis l'Essai 3, plus simple (sans salaire).
Le résultat est daté et conservé.

**2. Peux-tu redonner exactement le modèle de l'Essai 1 ?**
Oui. Chaque run garde son modèle. On le recharge avec
mlflow.sklearn.load_model("runs:/<run_id>/model").

**3. Un camarade peut-il reproduire ton travail ?**
En partie. Le code est sur GitHub, et les paramètres et versions des bibliothèques sont
notés dans le run (requirements.txt). Mais mlruns/ et mlflow.db restent sur ma machine,
et l'environnement n'est pas garanti identique



## TP4 — Model Registry et API

**1. Comment désigner officiellement le modèle à utiliser ?**

On utilise le Model Registry de MLflow et l’alias `champion` pour identifier la version du modèle choisie. Si on veut utiliser une autre version, il suffit de modifier l’alias.

**2. Comment une application peut-elle utiliser le modèle ?**

Une application peut envoyer les informations d’un client à l’API avec une requête HTTP `POST /predict`, au format JSON. L’API utilise le modèle pour effectuer la prédiction et renvoie le résultat.

**3. Que se passe-t-il quand on change de champion ?**

On déplace l’alias `champion` vers la nouvelle version du modèle. L’API doit ensuite être redémarrée pour charger cette version, mais le code de l’application cliente reste inchangé.