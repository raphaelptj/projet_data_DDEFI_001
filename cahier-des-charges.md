# Cahier des charges : Prédire le temps de course sur semi-marathon et marathon

- **Projet** : prédiction du temps d'un coureur sur semi-marathon et marathon à partir des données de ses séances Strava.
- **Équipe** : Petitjean Raphael, Semet Tristan, Le Bras Tom


---

## 1. La décision

Un coach ou une application d’entraînement doit attribuer un niveau et un plan d’entraînement à un coureur amateur, à partir du temps que nous prédisons pour son semi-marathon et son marathon. Il choisit entre un plan plus exigeant et un plan plus prudent. Si notre prédiction est trop optimiste, le coureur risque la surcharge et la blessure : c’est l’erreur la plus grave pour un amateur. Si elle est trop prudente, il s’entraîne en dessous de son niveau et progresse moins.

## 2. La problématique

À partir de ses X dernières courses, peut-on prédire le temps d’un coureur amateur sur semi-marathon et marathon à ± 3 minutes (semi) et ± 6 minutes (marathon) près, pour que son coach ou son application d’entraînement lui attribue le bon niveau ? Le nombre X est un paramètre que nous testerons.



## 3. La cible

Le modèle doit determiner le temps qu’un coureur met sur une distance donnée, à partir de ses courses précédentes. Nous l’entraînons et l’évaluons sur les distances disponibles dans nos données, puis nous l’extrapolons au semi-marathon et au marathon. 

Cette approche présente deux limites principales. D’abord, elle ne prend pas en compte les conditions extérieures ni l'état physique du coureur le jour de la séance (météo, fatigue, sommeil ou blessure). Ensuite, il est difficile d'évaluer la précision de la prédiction en la confrontant à un véritable chrono officiel, car les temps réels sur semi-marathon ou marathon ne sont pas disponibles pour l'ensemble des profils de notre jeu de données. Faute de ces courses de référence pour tous les coureurs, le résultat obtenu reste une estimation indicative et non une mesure exacte.

## 4. Les deux métriques

our évaluer notre modèle, nous utilisons deux critères :

- La métrique technique : l’erreur relative moyenne (en %), calculée sur des courses inconnues du modèle.
- La métrique terrain : la part de prédictions précises, fixée à ± 3 minutes près sur semi-marathon et ± 6 minutes sur marathon (seuils à confirmer).



## 5. Le garde-fou

En l’absence de données fiables (manque de courses récentes, sorties trop courtes ou fréquence cardiaque non renseignée), le modèle ne doit pas donner de chrono fixe. Il doit plutôt proposer une fourchette assortie d'un indice de confiance faible, voire refuser d'émettre une prédiction si les informations sont insuffisantes.

## 6. Qui sommes nous ?

**PETITJEAN Raphael**
- Parcours : DDEFI DATA
- Métier visé : Project Manager Aéronautique
- Centres d'intérêt : Sport (course à pied, basket, musculation)


**SEMET Tristan**
- Parcours : DDEFI FINANCE
- Métier visé : Analyste TS
- Centres d'intérêt : Sport (course à pied, foot)


**LE BRAS TOM** 
- Parcours : DDEFI FINANCE
- Métier visé : Analyste M&A
- Centres d'intérêt : Sport (course à pied, musculation, JJB)

**Pourquoi ce choix** 
- Nous réalisons déjà plusieurs projet en lien avec nos aspirations futures et nous voulions faire ce projet en lien avec nos passion commune qu'est la course à pied.
---

## Données

- **Source** : Nos données sont issues de Strava et concernent 6 utilisateurs, soit 600 activités, dont environ 360 courses à pied exploitables. Elles sont réparties dans deux fichiers : un fichier de résumés, avec une ligne par activité (distance, durée, fréquence cardiaque moyenne, etc.), et un fichier de streams, qui enregistre les mesures seconde par seconde (environ 1,5 million de lignes). Les deux fichiers sont reliés par l’identifiant activity_key.

- **Limites connues** : Nos données comportent plusieurs lacunes. La fréquence cardiaque est absente sur environ 12 % des activités et la puissance sur environ 61 %, ce qui limite les variables utilisables. Le fichier contient aussi des activités qui ne sont pas des courses (vélo, randonnée, natation, etc.), que nous écartons. Enfin, nous excluons les allures supérieures à 10 min/km, qui correspondent à de la marche ou à des arrêts et qui fausseraient les prédictions.

