# Scenarios Permissions


Scénarios de permissions par situation


| Situation | Outil | Résultat | Code responsable | Source |
| --- | --- | --- | --- | --- |
| **Lecture dans le workspace** | `read_file` | `ALWAYS` (si dans workspace) ou `ASK` (si outside) | `resolve_file_tool_permission()` vérifie `is_path_within_workdir()` | `vibe/core/tools/utils.py:L183-249` |
| **Écriture dans le workspace** | `write_file` | `ALWAYS` (si dans workspace) ou `ASK` (si outside) | `resolve_file_tool_permission()` vérifie `is_path_within_workdir()` | `vibe/core/tools/utils.py:L183-249` |
| **Accès hors workspace** | `read_file`, `write_file`, `bash` | `ASK` avec `RequiredPermission(scope=OUTSIDE_DIRECTORY)` | Ajoute la permission requise | `vibe/core/tools/utils.py:L225-238` |
| **Fichier sensible (.env)** | `read_file`, `bash` | `ASK` avec `RequiredPermission(scope=FILE_PATTERN)` | Détecte les motifs sensibles | `vibe/core/tools/utils.py:L210-218` |
| **Commande bash allowlistée** | `bash` | `ALWAYS` (si dans allowlist et pas dans denylist) | `_is_unconditionally_allowed()` vérifie les listes | `vibe/core/tools/builtins/bash.py:L720-722` |
| **Commande bash denylistée** | `bash` | `ASK` avec permissions requises ou `NEVER` | Filtre par denylist | `vibe/core/tools/builtins/bash.py:L690-705` |
| **Commande avec sudo** | `bash` | `ASK` avec `RequiredPermission` pour la commande | `needs_exact_command_scope()` | `vibe/core/tools/builtins/bash.py:L730-739` |
| **Permission déjà accordée pour la session** | Tous | `ALWAYS` | `PermissionStore.covers()` retourne True | `vibe/core/agent_loop/_loop.py:L3053-3063` |
| **Permission permanente (ALWAYS)** | Tous | `ALWAYS` | Config de l'outil | `vibe/core/tools/manager.py:L750-775` |
| **Permission permanente (NEVER)** | Tous | `NEVER` | Config de l'outil | `vibe/core/tools/manager.py:L750-775` |
| **Outil fourni par un plugin** | Plugin tools | Même que les outils built-in | Intégration via ToolManager | `vibe/core/tools/manager.py:L200-250` |
| **Outil fourni par MCP** | MCP tools | Même que les outils built-in | `ToolManager.integrate_mcp()` | `vibe/core/tools/manager.py:L560-580` |
| **Outil fourni par un connector** | Connector tools | Même que les outils built-in | `ToolManager.integrate_connectors()` | `vibe/core/tools/manager.py:L582-600` |


# Comportement Refus


Comportement quand une action est refusée

