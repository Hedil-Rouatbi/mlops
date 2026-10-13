# TP1 MLOps — Prédiction du churn client

Projet d'initiation au MLOps : génération d'un jeu de données fictif de clients,
exploration rapide des données, puis entraînement d'un modèle de classification
qui prédit si un client va quitter le service (*churn*).

## Structure du projet

| Fichier | Rôle |
|---|---|
| `generate_data.py` | Génère 500 clients fictifs et les enregistre dans `churn_data.csv` |
| `churn_data.csv` | Jeu de données généré (500 lignes, 6 colonnes) |
| `churn_model.ipynb` | Exploration des données et entraînement du modèle |
| `model.pkl` | Modèle entraîné, sauvegardé avec `joblib` |
| `requirements.txt` | Liste des bibliothèques Python nécessaires |

## Données

| Colonne | Description |
|---|---|
| `age` | Âge du client (18 à 70 ans) |
| `salaire` | Salaire mensuel simulé |
| `abonnement` | Type d'offre : Basique, Standard ou Premium |
| `anciennete` | Ancienneté en années |
| `consommation` | Score d'usage du service, sur 100 |
| `churn` | Cible : 1 = le client part, 0 = il reste |

Règle de génération du churn : un client est considéré comme partant s'il est
peu actif (consommation < 30) **et** récent (ancienneté < 2 ans).

## Installation

```powershell
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
```

## Utilisation

1. Générer les données :

```powershell
   python generate_data.py
```

2. Ouvrir `churn_model.ipynb` dans VS Code, sélectionner le kernel du `venv`,
   puis exécuter toutes les cellules (**Run All**).

## Limites constatées

Chaque nouvel entraînement écrase `model.pkl`, et `churn_data.csv` n'est pas
versionné. Il est donc impossible de savoir avec certitude quel essai, quelles
données et quels paramètres ont produit le modèle enregistré. C'est ce problème
que les outils MLOps (MLflow, DVC…) permettent de résoudre.

## Auteur

Hedil Rouatbi