# Centralisation des Tableaux - Documentation Permissions

Ce dossier contient les **tableaux extraits et centralisés** des fichiers de documentation du module `permissions`.

## Structure

### Fichiers markdown centralisés
- `tous_les_tableaux.md` - Tous les tableaux extraits en un seul fichier
- `fichiers_modules.md` - Tableaux du fichier 04-fichiers-et-modules.md (22 tableaux)
- `adr.md` - Tableaux du fichier 07-adr-et-contrat-des-outils.md (4 tableaux)
- `scenarios.md` - Tableaux du fichier 02-deroulement-et-scenarios.md (2 tableaux)
- `edge_cases.md` - Tableaux du fichier 06-edge-cases.md (1 tableau)
- `comparaison.md` - Tableaux du fichier 05-securite-et-sandbox.md (1 tableau)
- `comparaison_permissions_sandbox.md` - Tableau de comparaison
- `composants_contrat.md` - Tableaux des composants et contrats
- `aspects_comportement.md` - Tableaux des aspects comportementaux
- `autres.md` - Autres tableaux

## Utilisation

### Pour ajouter/modifier un tableau

1. **Modifier le fichier YAML correspondant** dans ce dossier
2. **Exécuter le script de génération** (si disponible) :
   ```bash
   python3 generate_md_from_yaml.py
   ```
3. **Ou mettre à jour manuellement** les fichiers markdown sources dans le dossier parent

### Pour référencer un tableau centralisé

Dans vos fichiers markdown, vous pouvez maintenant faire référence aux tableaux centralisés :

```markdown
Voir [Tableau des fichiers principaux](../tables/fichiers_et_modules.yaml) pour les détails.
```

Ou inclure directement un extrait :

```markdown
## Fichiers principaux

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/permissions.py` | Bibliothèque centrale | `PathGrantScope`, `PermissionScope` | `vibe/permissions.py:L1-100` |
```

## Avantages de la centralisation

✅ **Maintenance simplifiée** : Modifier un tableau dans un seul endroit
✅ **Cohérence** : Même format et structure pour tous les tableaux
✅ **Réutilisation** : Possibilité de générer automatiquement des vues différentes
✅ **Versionnage** : Historique clair des modifications des données

## Utilisation

### Pour utiliser les tableaux centralisés

Vous pouvez maintenant référencer les tableaux depuis n'importe quel fichier markdown :

```markdown
Voir [tous les tableaux](./tables/tous_les_tableaux.md) pour une vue d'ensemble.

Ou consulter des tableaux spécifiques :
- [Fichiers et modules](./tables/fichiers_modules.md)
- [ADR et contrats](./tables/adr.md)
- [Scénarios](./tables/scenarios.md)
```

### Pour ajouter/modifier un tableau

1. Ajouter ou modifier le tableau dans le fichier markdown correspondant dans ce dossier
2. Le tableau sera automatiquement disponible pour référence

## Fichiers source originaux

Les tableaux ont été extraits des fichiers suivants :
- `01-niveaux-et-modes.md` (12 tableaux)
- `02-deroulement-et-scenarios.md` (37 tableaux) ⭐
- `03-fichiers-utilisateur.md` (1 tableau)
- `04-fichiers-et-modules.md` (68 tableaux) ⭐⭐⭐
- `05-securite-et-sandbox.md` (6 tableaux)
- `06-edge-cases.md` (10 tableaux)
- `07-adr-et-contrat-des-outils.md` (51 tableaux) ⭐⭐
- `08-tests-et-qualite.md` (25 tableaux)

**Total : 33 tableaux extraits et catégorisés**

## Prochaines étapes

1. Terminer la migration de tous les tableaux vers les fichiers YAML
2. Créer un système d'inclusion dynamique (si MkDocs ou un autre générateur de site est utilisé)
3. Mettre à jour les fichiers markdown sources pour référencer les tableaux centralisés
4. Automatiser la génération via un script ou un hook git
