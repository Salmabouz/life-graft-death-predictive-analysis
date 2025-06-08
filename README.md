# life-graft-death-predictive-analysis
Predictive modeling of liver patient outcomes using logistic regression and XGBoost to classify survival, transplantation, or death

Prédiction du Pronostic Vital des Patients atteints de Maladies Hépatiques
Objectif du projet
L’objectif de ce projet est de développer un modèle de classification multiclasses capable de prédire le statut vital d’un patient atteint de maladie hépatique. Le modèle doit estimer la probabilité que le patient appartienne à l’une des trois classes suivantes :

Status_C : patient vivant

Status_CL : patient vivant ayant reçu une greffe

Status_D : patient décédé

L’évaluation des performances repose sur la log loss, une métrique qui pénalise les probabilités mal calibrées. L’objectif est donc de minimiser cette valeur.

Données
Le jeu de données est composé de 15 000 patients et 20 variables (dont 7 catégorielles et 13 numériques), avec une colonne id pour l’identification. Une particularité importante du jeu de données est la forte présence de valeurs manquantes, certaines variables ayant entre 42% et 55% de valeurs nulles.

Analyse exploratoire
Une analyse initiale a mis en évidence :

De nombreuses valeurs manquantes nécessitant une stratégie adaptée

Une faible corrélation globale entre les variables numériques

Des distributions loin de la normalité, confirmées par des tests statistiques

Des tests de Kruskal-Wallis ont été utilisés pour comparer les distributions des variables numériques entre les classes. Ces tests ont révélé que plusieurs variables sont significativement différentes selon le statut du patient, ce qui confirme leur potentiel informatif pour la classification.

Prétraitement des données
Imputation des valeurs manquantes selon le type de variable et sa corrélation avec d’autres.

Encodage des variables catégorielles via One-Hot Encoding ou Label Encoding selon le modèle utilisé.

Détection et traitement des valeurs aberrantes pour éviter les biais dans la modélisation.

Modélisation
Trois modèles principaux ont été testés :

1. Régression logistique multinomiale
Utilisée comme modèle de base

Donne des prédictions probabilistes interprétables

Score en validation croisée : log loss de 0,3286

Bonne calibration sans nécessité d’ajustement

Moins performant sur le jeu de test Kaggle (dégradation du score)

2. XGBoost
Meilleure capacité à gérer les non-linéarités et les interactions

Résistant aux valeurs manquantes

Score public Kaggle amélioré : log loss de 0,3479

3. Réseau de neurones (MLP)
Expérimenté en fin de projet

Mauvais résultat sur Kaggle (log loss ≈ 0,84)

Non adapté à ce jeu de données (taille modérée, bruit, peu de redondance)

Conclusion
Ce travail avait pour objectif de développer un modèle de classification capable de prédire le statut clinique de patients atteints d’une maladie hépatique, à partir de données cliniques et biologiques. Après une phase d’analyse exploratoire approfondie, nous avons traité les valeurs manquantes et les valeurs aberrantes afin d’assurer la qualité des données utilisées pour la modélisation.

Nous avons d’abord construit un modèle de régression logistique multinomiale, qui s’est révélé performant avec un log loss de 0,3286 lors de la validation croisée. L’analyse de calibration a montré que ce modèle était déjà bien calibré, sans nécessiter d’ajustements supplémentaires. Cependant, lors de l’évaluation sur le dataset externe de Kaggle, le score s’est dégradé, révélant des limites dans la généralisation.

Dans un souci d’amélioration, nous avons expérimenté d’autres approches, notamment un modèle XGBoost, qui a permis de légèrement améliorer le score public sur Kaggle, atteignant 0,3479, confirmant une meilleure robustesse face aux spécificités du dataset externe. Enfin, l’utilisation d’un réseau de neurones (MLP) n’a pas été concluante, le score public ayant fortement chuté à 0,84, ce qui confirme que ce type de modèle n’est pas adapté au contexte et aux caractéristiques de nos données.

En conclusion, bien que plusieurs approches aient été testées, la régression logistique multinomiale et XGBoost apparaissent comme les solutions les plus appropriées pour ce problème multiclasses, avec des performances stables et interprétables. Des pistes d’amélioration restent possibles, notamment en travaillant sur l’équilibre des classes, l’ingénierie des variables ou encore des techniques avancées de calibration pour affiner les probabilités prédites.
