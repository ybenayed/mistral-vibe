# Edge Cases

*Fichier source: 06-edge-cases.md*

## ---

## Résumé des edge cases

| Cas limite | Comportement | Source | Test existant |
|------------|--------------|--------|---------------|
| Chemins avec ".." | Normalisés et résolus → vérification des limites workspace | `utils.py:L175-180` | ❌ Non |
| Liens symboliques | Résolus avant vérification → hors workspace si cible hors workspace | `utils.py:L175-180` | ❌ Non |
| Commandes enchaînées (&&, |, ;) | Analysées récursivement → chaque partie vérifiée | `_shell_permission_analysis.py:L1-150` | ✅ Oui |
| Substitutions $(...) | Détectées comme nœuds dynamiques → demande approval | `_shell_permission_analysis.py:L80-90` | ❌ Non |
| Commandes non analysables | Nœuds non fidèles → demande approval | `_shell_permission_analysis.py:L95-100` | ❌ Non |
| Windows vs POSIX | Géré séparément → normalisation des chemins | `shell.py:L1-50`, `permissions.py:L40-90` | ✅ Oui |
| Fichier inexistant | Permission vérifiée avant existence → ToolError après | `read_file.py:L150-200` | ✅ Oui |
| Motifs sensibles + ALWAYS | Motifs sensibles l'emportent → demande approval | `utils.py:L210-218` | ❌ Non |
| Conflits allowlist/denylist | Denylist l'emporte | `bash.py:L690-705`, `utils.py:L200-210` | ❌ Non |

---

