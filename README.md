# Project Name

> Courte description en une phrase du dashboard/projet BI : quel problème il résout, pour qui, à partir de quelles données.

![status](https://img.shields.io/badge/status-active-brightgreen)
![license](https://img.shields.io/badge/license-MIT-blue)

## Aperçu

- **Objectif :** ...
- **Public cible :** ...
- **Outil de dashboard :** Power BI / Tableau / Streamlit
- **Fréquence de mise à jour :** ...

## Structure du repo

```
project-name/
├── data/
│   ├── raw/            # source brute — gitignored si volumineux/sensible
│   ├── processed/      # données nettoyées, prêtes pour le dashboard
│   └── sample/         # échantillon anonymisé pour démo publique
├── sql/
│   ├── extraction/      # requêtes source → staging
│   ├── transformation/  # CTEs, vues, logique métier
│   └── views/           # vues finales consommées par le dashboard
├── src/                 # code applicatif réutilisable (fonctions, modules Python)
├── scripts/             # scripts d'automatisation (refresh, ETL scheduled, exports)
├── notebooks/           # exploration ponctuelle (EDA, validation)
├── dashboard/
│   ├── powerbi/          # projet Power BI au format PBIP (JSON/TMDL, versionnable)
│   │   ├── <Project>.pbip
│   │   ├── <Project>.Report/        # définition du rapport (pages, visuels)
│   │   └── <Project>.SemanticModel/ # modèle sémantique (TMDL, Power Query M)
│   ├── tableau/           # classeur Tableau (.twbx / .twb) — à supprimer si non utilisé
│   └── assets/            # ressources runtime importées dans le dashboard
├── docs/                # data dictionary, méthodologie
└── reports/
    └── screenshots/     # captures du résultat final
```

## Démarrage rapide

1. Cloner le repo :
   ```bash
   git clone <repo-url>
   cd project-name
   ```
2. Placer les données brutes dans `data/raw/` (voir [docs/data-dictionary.md](docs/data-dictionary.md)).
3. Exécuter les scripts d'extraction/transformation :
   ```bash
   sql/extraction/...
   sql/transformation/...
   ```
4. Ouvrir `dashboard/powerbi/<Project>.pbip` dans Power BI Desktop (ou lancer l'app Streamlit) et rafraîchir les données.

## Données

| Dossier | Contenu | Suivi Git |
|---|---|---|
| `data/raw/` | Extraction brute depuis la source | Non (gitignored par défaut) |
| `data/processed/` | Données nettoyées, prêtes à l'emploi | Selon volumétrie |
| `data/sample/` | Échantillon anonymisé pour démo | Oui |

## SQL

- `sql/extraction/` : requêtes source → staging.
- `sql/transformation/` : CTEs, logique métier, vues intermédiaires.
- `sql/views/` : vues finales consommées directement par le dashboard.

## Dashboard

Décrire ici les pages principales, les KPI clés et comment naviguer dans le dashboard.

## Documentation

- [Dictionnaire de données](docs/data-dictionary.md)
- [Méthodologie](docs/methodology.md)

## Captures d'écran

Voir [reports/screenshots/](reports/screenshots/).

## Licence

Ce projet est sous licence MIT — voir [LICENSE](LICENSE).
