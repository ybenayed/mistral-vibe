# Fichiers Modules

*Fichier source: 04-fichiers-et-modules.md*

## ## Fichiers principaux et leurs rôles

### 📁 Bibliothèque centrale des permissions

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/permissions.py` | **Bibliothèque centrale** pour les motifs de chemins et matching | `PathGrantScope`, `PermissionScope`, `RequiredPermission`, `path_grant_pattern()`, `path_pattern_matches()`, `path_grant_pattern_matches()` | `vibe/permissions.py:L1-100` |

---

## ---

### 📁 Modèles de données pour les permissions

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/tools/models.py` | **Modèles Pydantic** pour les permissions des outils | `ToolPermission` (ALWAYS/NVER/ASK), `ToolPermissionError`, `PermissionContext`, `ApprovedRule`, `RequiredPermission` | `vibe/core/tools/models.py:L1-38` |

---

## ---

### 📁 Stockage et gestion des permissions

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/tools/permissions.py` | **Storage des permissions de session** | `PermissionStore`, méthodes `covers()`, `add_rule()`, `set_tool_permission()`, `get_tool_permission()`, `reset()` | `vibe/core/tools/permissions.py:L16-56` |

---

## ---

### 📁 Classe de base pour tous les outils

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/tools/base.py` | **Classe abstraite BaseTool** | Méthode abstraite `resolve_permission(args) -> PermissionContext | None`, `BaseToolConfig`, `InvokeContext`, `ToolError`, `CancellableToolResult`, `ToolInfo` | `vibe/core/tools/base.py:L1-487` |

---

## ---

### 📁 Gestionnaire des outils

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/tools/manager.py` | **Gestion centralisée** des outils (builtin, plugins, MCP, connectors) | `ToolManager`, `integrate_mcp()`, `integrate_connectors()`, `get_tool_config()`, `get()`, `available_tools`, `registered_tools` | `vibe/core/tools/manager.py:L1-795` |

---

## ---

### 📁 Fonctions utilitaires pour les outils

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/tools/utils.py` | **Fonctions utilitaires** pour la résolution des permissions | `resolve_file_tool_permission()`, `resolve_path_permission()`, `is_path_within_workdir()`, `matches_sensitive_pattern()`, `ambient_workspace()` | `vibe/core/tools/utils.py:L1-250` |

---

## ### 🛠 Outils builtins (implémentations concrètes)

#### Outils de fichier

| Chemin | Rôle | Permission par défaut | Méthode `resolve_permission()` | Source |
|--------|------|----------------------|--------------------------------|--------|
| `vibe/core/tools/builtins/read_file.py` | Lecture de fichiers | Non définie explicitement (dépend de config) | Appelle `resolve_file_tool_permission()` | `vibe/core/tools/builtins/read_file.py:L100-115` |
| `vibe/core/tools/builtins/write_file.py` | Écriture de fichiers | Non définie explicitement (dépend de config) | Appelle `resolve_file_tool_permission()` | `vibe/core/tools/builtins/write_file.py:L95-109` |
| `vibe/core/tools/builtins/edit.py` | Édition de fichiers | Non définie explicitement (dépend de config) | Appelle `resolve_file_tool_permission()` | `vibe/core/tools/builtins/edit.py:L88-96` |
| `vibe/core/tools/builtins/grep.py` | Recherche dans les fichiers | Non définie explicitement (dépend de config) | Appelle `resolve_file_tool_permission()` | `vibe/core/tools/builtins/grep.py:L191-199` |

---

## ---

#### Outils shell

| Chemin | Rôle | Permission par défaut | Méthode `resolve_permission()` | Source |
|--------|------|----------------------|--------------------------------|--------|
| `vibe/core/tools/builtins/bash.py` | Exécution shell POSIX | Non définie explicitement (dépend de config) | Analyse syntaxique complète avec tree-sitter | `vibe/core/tools/builtins/bash.py:L684-739` |
| `vibe/core/tools/builtins/git_bash.py` | Exécution git dans bash | Non définie explicitement (dépend de config) | Spécifique à git | `vibe/core/tools/builtins/git_bash.py:L211-250` |
| `vibe/core/tools/builtins/experimental_bash.py` | Bash expérimental | Non définie explicitement (dépend de config) | Analyse avancée | `vibe/core/tools/builtins/experimental_bash.py:L1834-1900` |
| `vibe/core/tools/builtins/windows_shell.py` | Exécution shell Windows | Non définie explicitement (dépend de config) | Analyse pour PowerShell/cmd | `vibe/core/tools/builtins/windows_shell.py:L914-1050` |

---

## ---

#### Outils réseau

| Chemin | Rôle | Permission par défaut | Méthode `resolve_permission()` | Source |
|--------|------|----------------------|--------------------------------|--------|
| `vibe/core/tools/builtins/web_fetch.py` | Récupération URL | Non définie explicitement (dépend de config) | Vérifie l'origin de l'URL | `vibe/core/tools/builtins/web_fetch.py:L105-130` |
| `vibe/core/tools/builtins/web_search.py` | Recherche web | Non définie explicitement (dépend de config) | À vérifier | `vibe/core/tools/builtins/web_search.py` |

---

## ---

#### Autres outils

| Chemin | Rôle | Permission par défaut | Méthode `resolve_permission()` | Source |
|--------|------|----------------------|--------------------------------|--------|
| `vibe/core/tools/builtins/skill.py` | Gestion des skills | Non définie explicitement (dépend de config) | Implémentation spécifique | `vibe/core/tools/builtins/skill.py:L172-180` |
| `vibe/core/tools/builtins/task.py` | Gestion des tâches | Non définie explicitement (dépend de config) | Implémentation spécifique | `vibe/core/tools/builtins/task.py:L77-85` |
| `vibe/core/tools/builtins/ask_user_question.py` | Questions utilisateur | Non définie explicitement (dépend de config) | Implémentation spécifique | `vibe/core/tools/builtins/ask_user_question.py` |

---

## ---

### 📁 Analyse des commandes shell

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/tools/builtins/_shell_command_policy.py` | **Politiques de commandes shell** | `analyze_shell_command_policy()`, `git_repository_requires_approval()`, `git_repository_identity()`, `has_option_guardrails()`, `path_candidates()` | `vibe/core/tools/builtins/_shell_command_policy.py:L1-150` |

---

## ---

### 📁 Boucle de l'agent (Agent Loop)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/agent_loop/_loop.py` | **Boucle principale** de l'agent | `AgentLoop`, `_should_execute_tool()`, `_ask_approval()`, `resolve_approval_request()`, `set_tool_permission()`, `approve_always()` | `vibe/core/agent_loop/_loop.py:L1-163212` |

---

## - `ApprovalSource` (CONFIG, SMART, USER, BYPASS, NEVER) (L254-260)
- `ToolDecision` (verdict, approval_type, feedback, approval_source) (L267-270)

---

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/agent_loop/_request_broker.py` | **Gestion des requêtes d'interaction** | `InteractionRequestBroker`, `request_approval()`, `request_user_input()`, `resolve_approval()`, `resolve_user_input()` | `vibe/core/agent_loop/_request_broker.py:L1-100` |

---

## ---

### 📁 App Server

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/app_server/_turns.py` | **Gestion des tours et callbacks** | `_handle_approval_request()`, `_open_callback()`, `_request_user_input()` | `vibe/app_server/_turns.py:L885-900` |

---

## - `_open_callback(event, detail, title)` (L901-920) : Affiche le callback à l'utilisateur
- `action_reject()` dans `approval_app.py` (L253) : Gère le refus (Esc ou n)

---

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/app_server/session.py` | **Gestion des sessions** | `respond_to_callback()`, `deny_callback()` | `vibe/app_server/session.py:L713-735` |

---

## ---

### 📁 Configuration

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/config/vibe_schema.py` | **Schéma de configuration global** | `VibeConfigSchema`, `tools: dict`, `bypass_tool_permissions: bool` | `vibe/core/config/vibe_schema.py:L414-440, L630` |

---

## - `tools: Annotated[dict[str, dict[str, Any]], WithDeepMerge(), BeforeValidator(_normalize_tool_configs)]` : Configuration par outil
- `bypass_tool_permissions: Annotated[bool, WithReplaceMerge()] = False` : Contourne toutes les vérifications de permission

---

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/config/models.py` | **Modèles de configuration** | `BaseToolConfig` (hérité par tous les outils) | `vibe/core/config/models.py:L1-100` |

---

## **Détails :**
- `BaseToolConfig` : Contient `permission: ToolPermission`, `allowlist: list[str]`, `denylist: list[str]`, `sensitive_patterns: list[str]`

---

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/trusted_folders.py` | **Gestion des dossiers de confiance** | `TrustedFoldersManager`, `WorkspaceTrustStatus`, `WorkspaceTrustDecision`, `trusted_folders_manager` (singleton) | `vibe/core/trusted_folders.py:L1-345` |

---

## ---

### 📁 Interface utilisateur (Textual TUI)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/cli/textual_ui/widgets/approval_app.py` | **Widget d'approbation** | `ApprovalApp`, `ApprovalGranted`, `ApprovalGrantedAlwaysTool`, `ApprovalGrantedAlwaysPermanent`, `ApprovalRejected`, `action_reject()` | `vibe/cli/textual_ui/widgets/approval_app.py:L1-320` |

---

## - `ApprovalGrantedAlwaysPermanent` → Approuve définitivement
  - `ApprovalRejected` → Refuse

---

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/cli/textual_ui/app.py` | **Application principale Textual** | Handlers des messages d'approbation | `vibe/cli/textual_ui/app.py:L2126-2150` |

---

## ---

### 📁 Types et modèles publics

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/types.py` | **Types publics** | `ApprovalResponse` (YES, NO), `ToolExecutionResponse` (SKIP, EXECUTE), `ApprovalSource` (CONFIG, SMART, USER, BYPASS, NEVER) | `vibe/core/types.py:L278-280` |

---

## ---

### 📁 Workspace

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/workspace.py` | **Gestion du workspace** | `Workspace`, `for_session()`, `allows()` | `vibe/core/workspace.py:L1-100` |

---

