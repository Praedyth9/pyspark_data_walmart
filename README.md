# Outils Big Data - PySpark pour la Data Science

Ce répertoire contient les livrables sous notebook Jupyter dans le cadre de la découverte du module PySpark. Nous traiterons ainsi des concepts fondamentaux et avancés de PySpark à travers une base de donneés relatif à Walmart qui sera détaillé ci-dessous. L'objectif ici est d'effectuer des manipulations sur les bases de données founrnies afin de visualiser les prédictions sur les ventes des magasins Walmart.

## 📋 **Table des matières**

- [Structure du répertoire](#structure-du-répertoire)
- [Documentation de la base de données](#documentation-de-la-base-de-données)
- [Contact](#contact)

## **Structure du répertoire**
```
.
    pyspark-data-science/
    ├── data/           # Données utilisées fournies par Walmart
    ├── livrables/      # Notebooks des différentes étapes pour l'analyse de données
    └── README.md       # Ce fichier
```

## **Documentation de la base de données**

### **Bases de données fournies par Walmart**

Nous basons notre étude sur trois bases de données fournies par Walmart relatifs aux ventes des produits dans dix de leur magasins entre janvier 2011 et avril 2016. Ces trois bases sont les suivantes :

- `sell_prices` : contient la liste des produits de chaque magasin ainsi que leur prix associé de manière hebdomadaire
- `calendar` : Pour chaque jour de la période à laquelle on s'interesse, indique si un évènement spécial se produit ou non (superbowl, période de Noêl, ...)
- `walmart_sales` : Répertorie les ventes journaliaires de chaque produit dans chaque magasin

### **Dataframe après manipulations**

Le dataframe permettant le développement du modèle prédictif en PySpark contient, pour chaque mois, produit et magasins les informations suivantes :

- La catégorie auquel le produit appartient `cat_id`
- La région dans laquelle le magasin se trouve `state_id`
- Le nombre de ventes du produit réalisé pendant ce mois `sales` ainsi que les lag et lead de ceux-ci, allant d'une différence d'un mois à un an
- Les chiffres d'affaires cumulées par produit et catégorie `ca_sum_item`, `ca_sum_category`
- Date de première commercialisation du produit `first_date`
- Part de marché d'un produit `marquet_quota`
- La segmentation ABC dans laquelle appartient le produit `perf_category`

  
## **Contact**

