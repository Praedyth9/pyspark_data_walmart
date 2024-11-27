# Outils Big Data - PySpark pour la Data Science

Ce répertoire contient les livrables sous notebook Jupyter dans le cadre de la découverte du module PySpark. Nous traiterons ainsi des concepts fondamentaux et avancés de PySpark à travers une base de donneés relatif à Walmart qui sera détaillé ci-dessous. 

## 📋 **Table des matières**

- [Structure du répertoire](#structure-du-répertoire)
- [Bases de données fournies par Walmart](#bases-de-données-fournies-par-walmart-)
- [Objectifs du projet](#objectifs-du-projet-)
- [Démarches réalisées](#démarches-réalisées-)
- [Dataframe après manipulations](#dataframe-après-manipulations-)
- [Contact](#contact)

## **Structure du répertoire**
```
.
    pyspark-data-science/
    ├── livrables/      # Notebooks des différentes étapes pour l'analyse de données
    └── README.md       # Ce fichier
```

## **Bases de données fournies par Walmart** 🖥

Nous basons notre étude sur trois [bases de données fournies par Walmart relatifs](https://github.com/ettouilebouael/pyspark_for_datascience/raw/refs/heads/main/data/walmart_data.zip) aux ventes des produits dans dix de leur magasins entre janvier 2011 et avril 2016. Ces trois bases sont les suivantes :

- `sell_prices` : contient la liste des produits de chaque magasin ainsi que leur prix associé de manière hebdomadaire sous le format suivant :    
```
store_id | item_id | wm_yr_wk | sell_price
```
où `wm_yr_wk`correspond à un numéro attribué à une semaine en particulier.

- `calendar` : Pour chaque jour de la période à laquelle on s'interesse, indique si un évènement spécial se produit ou non (superbowl, période de Noêl, ...). Permet également de lier une semaine donnée au numéro `wm_yr_wk` et est organisé comme suit :    
```
date | wm_yr_wk | weekday | wday | month | year | event...
```
- `walmart_sales` : Répertorie les ventes journaliaires de chaque produit dans chaque magasin sous le format décrit ci-dessous :    
```
item_id | dept_id | cat_id | store_id | state_id | id | date | sales
```

## **Objectifs du projet** 🎯

L'objectif du projet est d'utiliser les bases de données fournies par Walmart afin de développer un modèle prédictif en PySpark afin d'estimer les ventes mensuelles dans chacun des 10 magasins faisant parti de la cohorte étudiée. Pour ce faire, nous effectuerons des démarches de préparation de données puis de manipulation de celles-ci afin d'établir le modèle le plus performant possible.



## **Démarches réalisées** 📓

### Préparation des données 

Il s'agit ici de parcourir chaque base de données à la recherche de valeurs manquantes mais également d'imputer la série temporelle si des données manquent au cours d'une année. La base de données fournie ne possédait aucune valeur manquante et aucune imputation était nécessaire. Les données présentées étaient également cohérentes, avec absence de valeurs de ventes négatives par exemple, rendant conforme la base de données sur laquelle nous nous basons.

### Manipulation de la base pour ajouts de features

L'ajout de feature permet au futur modèle prédictif d'avoir plus de variables sur lequels se baser afin de prédire les ventes futures au cours des prochains mois. On calcule donc les `lag` et `lead` du nombre de ventes mensuelles pour chaque produit dans chaque magasin.

L'extraction des caractéristiques temporelles est également importante, d'où le fait d'effectuer un parsing des dates en mois et année. Pour que la périodicité des mois soient plus saisis par le futur modèle, nous effectuons un encodage cyclique des mois.

Le calcul des coordonnées \( X \) et \( Y \) de chaque mois sur un cercle unité, les formules sont les suivantes :

- Soit \( m \) le numéro du mois (variant de 1 à 12).
- La coordonnée \( X \) est donnée par :

  $$ X = \cos\left( \cfrac{2 \pi \times m}{12} \right) $$

- La coordonnée \( Y \) est donnée par :

  $$ Y = \sin\left( \cfrac{2 \pi \times m }{12} \right) $$

Le chiffre d'affaire mensuel est quant à lui calculé à l'aide du prix moyen d'un produit sur un mois multiplié par son nombre de ventes, respectivement donné par les dataframes `sell_prices` et `walmart_sales`. 

Ce chiffre d'affaire est ensuite utilisé pour le calcul de quotas de marché, et également réalisé la segmentation ABC des produits.

### Modélisation 

A VENIR

## **Dataframe après manipulations** 🖥

Le dataframe permettant le développement du modèle prédictif en PySpark contient, pour chaque mois, produit et magasins les informations suivantes :

- La catégorie auquel le produit appartient `cat_id`
- La région dans laquelle le magasin se trouve `state_id`
- Le nombre de ventes du produit réalisé pendant ce mois `sales` ainsi que les lag `sales_lag` et lead `sales_lead` de ceux-ci, allant d'une différence d'un mois à un an
- Les chiffres d'affaires cumulées par produit et catégorie `ca_sum_item`, `ca_sum_category`
- Date de première commercialisation du produit `first_date`
- Part de marché d'un produit `marquet_quota`
- La segmentation ABC dans laquelle appartient le produit `perf_category`
  
## **Contact**

- Discord : @praae
- Mail : victor.juille@etudiant.univ-reims.fr
