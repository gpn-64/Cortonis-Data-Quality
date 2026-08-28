# Méthodologie

## Sources de données

- Décrire chaque source (base de données, API, fichiers plats), son propriétaire et sa fiabilité.

## Pipeline

1. **Extraction** (`sql/extraction/`) : requêtes source → staging.
2. **Transformation** (`sql/transformation/`) : nettoyage, jointures, logique métier.
3. **Vues finales** (`sql/views/`) : agrégations consommées par le dashboard.
4. **Chargement dashboard** : rafraîchissement dans `dashboard/project.pbix`.

## Définitions des KPI

| KPI | Formule | Source |
|---|---|---|
| ... | ... | ... |

## Hypothèses et limites

- Lister les hypothèses de calcul, les exclusions de données, les biais connus.

## Historique des changements

| Date | Changement | Auteur |
|---|---|---|
| AAAA-MM-JJ | Création initiale | ... |
