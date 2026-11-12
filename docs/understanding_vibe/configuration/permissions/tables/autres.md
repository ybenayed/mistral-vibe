# Autres

*Fichier source: 08-tests-et-qualite.md*

## ## Couverture des tests

### Tests unitaires et d'intégration

| Fichier de test | Couverture | Description | Source |
|-----------------|------------|-------------|--------|
| `tests/app_server/test_approval_permissions.py` | Permissions d'approbation | Tests des path scopes, validation des grants, intégration app-server | `tests/app_server/test_approval_permissions.py` |
| `tests/session/test_session_permissions.py` | Permissions de session | Tests de la restriction des permissions des logs de session (owner-only) | `tests/session/test_session_permissions.py` |
| `tests/agent_loop/test_agent_override_resolve_permission.py` | resolve_permission | Vérification des mécanismes de résolution des permissions par outil | `tests/agent_loop/test_agent_override_resolve_permission.py` |
| `tests/agent_loop/test_agent_tool_call.py` | Appels d'outils | Tests des appels d'outils avec vérification des permissions | `tests/agent_loop/test_agent_tool_call.py` |
| `tests/agent_loop/test_approve_always_permanent.py` | Always allow | Tests des approbations permanentes | `tests/agent_loop/test_approve_always_permanent.py` |

---

## | `tests/agent_loop/test_agent_tool_call.py` | Appels d'outils | Tests des appels d'outils avec vérification des permissions | `tests/agent_loop/test_agent_tool_call.py` |
| `tests/agent_loop/test_approve_always_permanent.py` | Always allow | Tests des approbations permanentes | `tests/agent_loop/test_approve_always_permanent.py` |

### Tests des outils builtins

| Fichier de test | Outil testé | Couverture | Source |
|-----------------|-------------|------------|--------|
| `tests/tools/test_bash.py` | bash | Analyse des commandes, permissions, allowlist/denylist | `tests/tools/test_bash.py` |
| `tests/tools/test_windows_shell.py` | windows_shell | Analyse des commandes Windows, permissions | `tests/tools/test_windows_shell.py` |
| `tests/tools/test_edit.py` | edit | Permission d'édition, modification de fichiers | `tests/tools/test_edit.py` |
| `tests/tools/test_read_file.py` | read_file | Permission de lecture, accès aux fichiers | `tests/tools/test_read_file.py` |
| `tests/tools/test_write_file.py` | write_file | Permission d'écriture, création de fichiers | `tests/tools/test_write_file.py` |
| `tests/tools/test_grep.py` | grep | Permission de recherche dans les fichiers | `tests/tools/test_grep.py` |
| `tests/tools/test_mcp.py` | MCP tools | Intégration des outils MCP, permissions | `tests/tools/test_mcp.py` |
| `tests/tools/test_websearch.py` | web_search | Permission de recherche web | `tests/tools/test_websearch.py` |
| `tests/tools/test_webfetch.py` | web_fetch | Permission de récupération URL | `tests/tools/test_webfetch.py` |

---

## ## Points à améliorer

### Couverture manquante identifiée

| Edge case | Test existant | Statut | Recommandation |
|-----------|---------------|--------|----------------|
| Chemins avec ".." | ❌ Non | Non testé | Ajouter des tests dans `test_bash.py` ou `test_read_file.py` |
| Liens symboliques | ❌ Non | Non testé | Ajouter des tests pour les liens vers /etc/passwd |
| Substitutions $(...) | ❌ Non | Non testé | Ajouter des tests pour les command substitutions |
| Commandes non analysables | ❌ Non | Non testé | Ajouter des tests pour les function_definition |
| Motifs sensibles + ALWAYS | ❌ Non | Non testé | Vérifier que les motifs sensibles l'emportent |
| Conflits allowlist/denylist | ❌ Non | Non testé | Vérifier que denylist l'emporte |
| Denylist standalone | ❌ Non | Non testé | Tester `python` vs `python script.py` |

---

