# Quantification d'Incertitude (UQ) pour la Prédiction de Séries Temporelles

Ce repository propose une exploration et une implémentation pratique de différentes méthodes de **quantification d'incertitude (UQ)** appliquées à la prédiction de séries temporelles multivariées. 
L'objectif est de comparer plusieurs approches classiques pour estimer l'incertitude **aléatorique** (liée aux données) des prédictions d'un modèle de Deep Learning.

Le code est principalement contenu dans le notebook `UQ.ipynb`.
***

### Méthodes Explorées

Ce projet implémente et compare plusieurs méthodes de référence pour la quantification d'incertitude, notamment :

* **Méthodes Basées sur l'Historique** : Utilisation de la distribution des données passées pour estimer les intervalles futurs.
* **Deep Ensembles** : Entraînement de plusieurs modèles identiques avec des initialisations différentes pour capturer l'incertitude.
* **Monte Carlo Dropout (MC Dropout)** : Une technique bayésienne approchée qui utilise le dropout en phase d'inférence pour simuler un ensemble de modèles.
* **Deep Quantile Regression (DQR)** : Entraînement d'un modèle à prédire directement les quantiles de la distribution de sortie.
* **Conformal Prediction** : Génération d'un PI à partir du quantile des résidual des erreurs de prédictions. Garantie une couverture statistique.
* **Conformalized Quantile Prediction** : Combinaison de la conformal prediction et de la DQR

D'autres approches sont également discutées et référencées dans le notebook.

***

### Structure du Repository

* `UQ.ipynb`: Notebook Jupyter principal. Il contient les explications, le code et les visualisations pour chaque méthode.
* `CNN.py`: Définit principalement un modèle **CNN** simple capable de gérer des séries temporelles multivariées sans structure de graphe explicite.
* `trainer.py`: Contient principalement la classe `Trainer` pour gérer l'entraînement et l'évaluation du modèle PyTorch.
* `PI.py`: Fournit des fonctions utilitaires pour la gestion des intervalles de prédiction (PI).
* `plotting.py`: Centralise les fonctions utilisées pour générer les figures et graphiques.
* `load_data.py`: Gère le chargement, le prétraitement et la génération des séquences de données.

***

### Mise en Route

Ouvrez et exécutez le notebook `UQ.ipynb`. Il est conçu pour être auto-suffisant.

***

### Métriques d'Évaluation

Pour évaluer la qualité des intervalles de prédiction générés, nous utilisons deux métriques principales :

* **PICP (Prediction Interval Coverage Probability)** : Le pourcentage de fois où la valeur réelle se trouve à l'intérieur de l'intervalle de prédiction. On vise un PICP proche du niveau de confiance désiré (ex: 95%).
* **MPIW (Mean Prediction Interval Width)** : La largeur moyenne des intervalles de prédiction. Pour un même PICP, un intervalle plus étroit est préférable car il représente une prédiction plus précise.
