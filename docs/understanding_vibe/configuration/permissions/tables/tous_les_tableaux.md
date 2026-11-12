# Tous les tableaux

## ## Fichiers principaux et leurs rôles

### 📁 Bibliothèque centrale des permissions (04-fichiers-et-modules.md:55)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/permissions.py` | **Bibliothèque centrale** pour les motifs de chemins et matching | `PathGrantScope`, `PermissionScope`, `RequiredPermission`, `path_grant_pattern()`, `path_pattern_matches()`, `path_grant_pattern_matches()` | `vibe/permissions.py:L1-100` |

---

## ---

### 📁 Modèles de données pour les permissions (04-fichiers-et-modules.md:68)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/tools/models.py` | **Modèles Pydantic** pour les permissions des outils | `ToolPermission` (ALWAYS/NVER/ASK), `ToolPermissionError`, `PermissionContext`, `ApprovedRule`, `RequiredPermission` | `vibe/core/tools/models.py:L1-38` |

---

## ---

### 📁 Stockage et gestion des permissions (04-fichiers-et-modules.md:81)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/tools/permissions.py` | **Storage des permissions de session** | `PermissionStore`, méthodes `covers()`, `add_rule()`, `set_tool_permission()`, `get_tool_permission()`, `reset()` | `vibe/core/tools/permissions.py:L16-56` |

---

## ---

### 📁 Classe de base pour tous les outils (04-fichiers-et-modules.md:95)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/tools/base.py` | **Classe abstraite BaseTool** | Méthode abstraite `resolve_permission(args) -> PermissionContext | None`, `BaseToolConfig`, `InvokeContext`, `ToolError`, `CancellableToolResult`, `ToolInfo` | `vibe/core/tools/base.py:L1-487` |

---

## ---

### 📁 Gestionnaire des outils (04-fichiers-et-modules.md:109)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/tools/manager.py` | **Gestion centralisée** des outils (builtin, plugins, MCP, connectors) | `ToolManager`, `integrate_mcp()`, `integrate_connectors()`, `get_tool_config()`, `get()`, `available_tools`, `registered_tools` | `vibe/core/tools/manager.py:L1-795` |

---

## ---

### 📁 Fonctions utilitaires pour les outils (04-fichiers-et-modules.md:124)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/tools/utils.py` | **Fonctions utilitaires** pour la résolution des permissions | `resolve_file_tool_permission()`, `resolve_path_permission()`, `is_path_within_workdir()`, `matches_sensitive_pattern()`, `ambient_workspace()` | `vibe/core/tools/utils.py:L1-250` |

---

## ### 🛠 Outils builtins (implémentations concrètes)

#### Outils de fichier (04-fichiers-et-modules.md:142)

| Chemin | Rôle | Permission par défaut | Méthode `resolve_permission()` | Source |
|--------|------|----------------------|--------------------------------|--------|
| `vibe/core/tools/builtins/read_file.py` | Lecture de fichiers | Non définie explicitement (dépend de config) | Appelle `resolve_file_tool_permission()` | `vibe/core/tools/builtins/read_file.py:L100-115` |
| `vibe/core/tools/builtins/write_file.py` | Écriture de fichiers | Non définie explicitement (dépend de config) | Appelle `resolve_file_tool_permission()` | `vibe/core/tools/builtins/write_file.py:L95-109` |
| `vibe/core/tools/builtins/edit.py` | Édition de fichiers | Non définie explicitement (dépend de config) | Appelle `resolve_file_tool_permission()` | `vibe/core/tools/builtins/edit.py:L88-96` |
| `vibe/core/tools/builtins/grep.py` | Recherche dans les fichiers | Non définie explicitement (dépend de config) | Appelle `resolve_file_tool_permission()` | `vibe/core/tools/builtins/grep.py:L191-199` |

---

## ---

#### Outils shell (04-fichiers-et-modules.md:155)

| Chemin | Rôle | Permission par défaut | Méthode `resolve_permission()` | Source |
|--------|------|----------------------|--------------------------------|--------|
| `vibe/core/tools/builtins/bash.py` | Exécution shell POSIX | Non définie explicitement (dépend de config) | Analyse syntaxique complète avec tree-sitter | `vibe/core/tools/builtins/bash.py:L684-739` |
| `vibe/core/tools/builtins/git_bash.py` | Exécution git dans bash | Non définie explicitement (dépend de config) | Spécifique à git | `vibe/core/tools/builtins/git_bash.py:L211-250` |
| `vibe/core/tools/builtins/experimental_bash.py` | Bash expérimental | Non définie explicitement (dépend de config) | Analyse avancée | `vibe/core/tools/builtins/experimental_bash.py:L1834-1900` |
| `vibe/core/tools/builtins/windows_shell.py` | Exécution shell Windows | Non définie explicitement (dépend de config) | Analyse pour PowerShell/cmd | `vibe/core/tools/builtins/windows_shell.py:L914-1050` |

---

## ---

#### Outils réseau (04-fichiers-et-modules.md:178)

| Chemin | Rôle | Permission par défaut | Méthode `resolve_permission()` | Source |
|--------|------|----------------------|--------------------------------|--------|
| `vibe/core/tools/builtins/web_fetch.py` | Récupération URL | Non définie explicitement (dépend de config) | Vérifie l'origin de l'URL | `vibe/core/tools/builtins/web_fetch.py:L105-130` |
| `vibe/core/tools/builtins/web_search.py` | Recherche web | Non définie explicitement (dépend de config) | À vérifier | `vibe/core/tools/builtins/web_search.py` |

---

## ---

#### Autres outils (04-fichiers-et-modules.md:194)

| Chemin | Rôle | Permission par défaut | Méthode `resolve_permission()` | Source |
|--------|------|----------------------|--------------------------------|--------|
| `vibe/core/tools/builtins/skill.py` | Gestion des skills | Non définie explicitement (dépend de config) | Implémentation spécifique | `vibe/core/tools/builtins/skill.py:L172-180` |
| `vibe/core/tools/builtins/task.py` | Gestion des tâches | Non définie explicitement (dépend de config) | Implémentation spécifique | `vibe/core/tools/builtins/task.py:L77-85` |
| `vibe/core/tools/builtins/ask_user_question.py` | Questions utilisateur | Non définie explicitement (dépend de config) | Implémentation spécifique | `vibe/core/tools/builtins/ask_user_question.py` |

---

## ---

### 📁 Analyse des commandes shell (04-fichiers-et-modules.md:204)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/tools/builtins/_shell_command_policy.py` | **Politiques de commandes shell** | `analyze_shell_command_policy()`, `git_repository_requires_approval()`, `git_repository_identity()`, `has_option_guardrails()`, `path_candidates()` | `vibe/core/tools/builtins/_shell_command_policy.py:L1-150` |

---

## ---

### 📁 Boucle de l'agent (Agent Loop) (04-fichiers-et-modules.md:231)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/agent_loop/_loop.py` | **Boucle principale** de l'agent | `AgentLoop`, `_should_execute_tool()`, `_ask_approval()`, `resolve_approval_request()`, `set_tool_permission()`, `approve_always()` | `vibe/core/agent_loop/_loop.py:L1-163212` |

---

## - `ApprovalSource` (CONFIG, SMART, USER, BYPASS, NEVER) (L254-260)
- `ToolDecision` (verdict, approval_type, feedback, approval_source) (L267-270)

--- (04-fichiers-et-modules.md:253)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/agent_loop/_request_broker.py` | **Gestion des requêtes d'interaction** | `InteractionRequestBroker`, `request_approval()`, `request_user_input()`, `resolve_approval()`, `resolve_user_input()` | `vibe/core/agent_loop/_request_broker.py:L1-100` |

---

## ---

### 📁 App Server (04-fichiers-et-modules.md:265)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/app_server/_turns.py` | **Gestion des tours et callbacks** | `_handle_approval_request()`, `_open_callback()`, `_request_user_input()` | `vibe/app_server/_turns.py:L885-900` |

---

## - `_open_callback(event, detail, title)` (L901-920) : Affiche le callback à l'utilisateur
- `action_reject()` dans `approval_app.py` (L253) : Gère le refus (Esc ou n)

--- (04-fichiers-et-modules.md:276)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/app_server/session.py` | **Gestion des sessions** | `respond_to_callback()`, `deny_callback()` | `vibe/app_server/session.py:L713-735` |

---

## ---

### 📁 Configuration (04-fichiers-et-modules.md:288)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/config/vibe_schema.py` | **Schéma de configuration global** | `VibeConfigSchema`, `tools: dict`, `bypass_tool_permissions: bool` | `vibe/core/config/vibe_schema.py:L414-440, L630` |

---

## - `tools: Annotated[dict[str, dict[str, Any]], WithDeepMerge(), BeforeValidator(_normalize_tool_configs)]` : Configuration par outil
- `bypass_tool_permissions: Annotated[bool, WithReplaceMerge()] = False` : Contourne toutes les vérifications de permission

--- (04-fichiers-et-modules.md:298)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/config/models.py` | **Modèles de configuration** | `BaseToolConfig` (hérité par tous les outils) | `vibe/core/config/models.py:L1-100` |

---

## **Détails :**
- `BaseToolConfig` : Contient `permission: ToolPermission`, `allowlist: list[str]`, `denylist: list[str]`, `sensitive_patterns: list[str]`

--- (04-fichiers-et-modules.md:307)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/trusted_folders.py` | **Gestion des dossiers de confiance** | `TrustedFoldersManager`, `WorkspaceTrustStatus`, `WorkspaceTrustDecision`, `trusted_folders_manager` (singleton) | `vibe/core/trusted_folders.py:L1-345` |

---

## ---

### 📁 Interface utilisateur (Textual TUI) (04-fichiers-et-modules.md:320)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/cli/textual_ui/widgets/approval_app.py` | **Widget d'approbation** | `ApprovalApp`, `ApprovalGranted`, `ApprovalGrantedAlwaysTool`, `ApprovalGrantedAlwaysPermanent`, `ApprovalRejected`, `action_reject()` | `vibe/cli/textual_ui/widgets/approval_app.py:L1-320` |

---

## - `ApprovalGrantedAlwaysPermanent` → Approuve définitivement
  - `ApprovalRejected` → Refuse

--- (04-fichiers-et-modules.md:343)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/cli/textual_ui/app.py` | **Application principale Textual** | Handlers des messages d'approbation | `vibe/cli/textual_ui/app.py:L2126-2150` |

---

## ---

### 📁 Types et modèles publics (04-fichiers-et-modules.md:358)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/types.py` | **Types publics** | `ApprovalResponse` (YES, NO), `ToolExecutionResponse` (SKIP, EXECUTE), `ApprovalSource` (CONFIG, SMART, USER, BYPASS, NEVER) | `vibe/core/types.py:L278-280` |

---

## ---

### 📁 Workspace (04-fichiers-et-modules.md:371)

| Chemin | Rôle | Composants clés | Source |
|--------|------|-----------------|--------|
| `vibe/core/workspace.py` | **Gestion du workspace** | `Workspace`, `for_session()`, `allows()` | `vibe/core/workspace.py:L1-100` |

---

## ## Couverture des tests

### Tests unitaires et d'intégration (08-tests-et-qualite.md:9)

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

### Tests des outils builtins (08-tests-et-qualite.md:19)

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

### Couverture manquante identifiée (08-tests-et-qualite.md:128)

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

## ---

## Liste complète des ADR liés aux permissions, outils ou sécurité (07-adr-et-contrat-des-outils.md:7)

| N° | Titre | Décision | Lien avec les permissions | Source |
|---|-------|----------|---------------------------|--------|
| **0001** | Architecture Principles | Architecture hexagonale : core ↔ edges, optimisation pour startup rapide et changements locaux | **Indirect** : Les permissions sont un *port* (frontière) entre le core et les effets de bord. La séparation permet d'isoler la logique de permission dans le core | `docs/adr/0001-architecture-principles.md` |
| **0002** | Core Engine And Delivery Surfaces | `vibe/core` = moteur (agent loop, **tools**, LLM, config, sessions), `vibe/app_server` = harness, delivery surfaces (CLI, ACP, programmatic) consomment le core | **Direct** : Les **tools** font partie du core. Les permissions sont gérées dans le même espace | `docs/adr/0002-core-engine-and-delivery-surfaces.md:L8-12` |
| **0003** | Event Driven Agent Loop | Boucle d'agent basée sur des **événements typés** (streaming async). Les événements incluent les approvals, tool calls, tool results | **Indirect** : Les *approvals* (demandes de permission) sont des événements typés dans le système | `docs/adr/0003-event-driven-agent-loop.md:L8-10` |
| **0004** | **Typed Permissioned Tools** | **Contrat des outils** : Les outils sont des ports typés vers les effets de bord. **La politique de permission fait partie intégrante du contrat de l'outil**. Analyse sémantique des commandes shell (récursive, normalisation des chemins). Un effet public unique représente le tool call complet | **Central et direct** : **Définition complète du tool contract** pour les permissions | `docs/adr/0004-typed-permissioned-tools.md` |
| **0005** | Layered Configuration | Configuration en couches (CLI > env > fichiers projet > defaults). Les paramètres de **permission** sont des *server-applied settings* | **Direct** : `tools: dict`, `bypass_tool_permissions` sont configurés via ce système | `docs/adr/0005-layered-configuration.md:L15-20` |
| **0007** | Extension Mechanisms | **Mécanismes d'extension** : skills, agents, subagents, hooks, **MCP servers**, **connectors**. Les extensions fournissent des outils qui doivent respecter le même contrat | **Direct** : Les outils **MCP** et **connectors** doivent respecter le même contrat de permission que les outils built-in | `docs/adr/0007-extension-mechanisms.md:L8-12` |
| **0008** | Feature Instrumentation | Téléométrie pour les *features* (funnels, adoption, status flows) | **Indirect** : Les événements de permission (ex: `approval_requested`, `approval_denied`) peuvent être instrumentés pour la télémétrie | `docs/adr/0008-feature-instrumentation.md` |
| **0009** | **App Server Boundary** | L'app-server est la **seule frontière** entre les delivery surfaces et le core. **Le serveur est autoritaire** pour : outils, permissions, effets, résultats visibles par le modèle. **Règles de sécurité** : le serveur applique la politique outils/FS/réseau/MCP/connector ; les projections publiques ne peuvent pas accorder de permission | **Direct et critique** : **Le serveur applique les permissions** (pas le client). Toute mutation passe par l'app-server | `docs/adr/0009-app-server-boundary.md:L25-30,L150-160` |
| **0010** | Textual Content Rendering | Rendu du contenu dans l'UI Textual (styles, markup) | **Indirect** : L'UI affiche les demandes de permission mais ne décide pas | `docs/adr/0010-textual-content-rendering.md` |
| **0011** | App Server Session Backends | Backends de session (Legacy vs Unified Harness). Les opérations sur les sessions passent par des *ports* typés | **Indirect** : Les backends de session **héritent** de la politique de permission du core via l'app-server | `docs/adr/0011-unified-harness-backend.md:L40-45` |
| **0014** | Backend Contract Compatibility | Compatibilité avec les backends Mistral (self-hosted). Changements de contrat wire doivent être *additifs et tolérants* | **Indirect (sécurité)** : La politique de permission doit rester compatible avec les versions antérieures | `docs/adr/0014-backend-contract-compatibility.md:L10-20` |
| **0015** | **Outbound TLS Trust Policy** | Politique de confiance TLS pour les connexions sortantes (`enable_system_trust_store`). Utilise Certifi ou system trust store | **Direct (sécurité)** : Sécurité des connexions réseau (impacte les outils comme `web_fetch`) | `docs/adr/0015-outbound-tls-trust-policy.md` |

---

## - Les outils MCP/connector peuvent fournir des outils qui doivent **respecter le même contrat**
   - Un backend dont le protocole source porte intentionnellement des faits d'outils sans présentation Vibe peut traduire un ensemble fermé d'outils built-in vers ces catégories sémantiques existantes

### Ce que chaque outil doit respecter (Tool Contract) (07-adr-et-contrat-des-outils.md:61)

| Composant | Obligation | Implémentation | Source |
|-----------|------------|----------------|--------|
| **Hériter de BaseTool** | ✅ Obligatoire | `class MonOutil(BaseTool[...]):` | `vibe/core/tools/base.py:L100-150` |
| **Déclarer les types** | ✅ Obligatoire | Typage Pydantic pour args, result, config, state | `vibe/core/tools/base.py:L100-150` |
| **Implémenter resolve_permission** | ✅ Obligatoire | `def resolve_permission(self, args) -> PermissionContext | None:` | `vibe/core/tools/base.py:L448-450` |
| **Respecter ToolPermission** | ✅ Obligatoire | Vérifier et honorer la permission de la config | `vibe/core/tools/base.py:L448-450` |
| **Lever ToolPermissionError** | ⚠️ Recommandé | `raise ToolPermissionError("raison")` pour les refus | ADR 0004:L40-41, `vibe/core/tools/models.py:L10` |
| **Ne pas exécuter si refusé** | ✅ Obligatoire | Bloquer l'exécution si permission refusée | `vibe/core/agent_loop/_loop.py:L3027-3070` |

---

## | **Lever ToolPermissionError** | ⚠️ Recommandé | `raise ToolPermissionError("raison")` pour les refus | ADR 0004:L40-41, `vibe/core/tools/models.py:L10` |
| **Ne pas exécuter si refusé** | ✅ Obligatoire | Bloquer l'exécution si permission refusée | `vibe/core/agent_loop/_loop.py:L3027-3070` |

### Quels composants doivent appliquer le contrat ? (07-adr-et-contrat-des-outils.md:72)

| Composant | Rôle | Application du contrat | Source |
|-----------|------|-----------------------|--------|
| **Agent Loop** | Exécute les outils et gère la boucle LLM | **Applique les permissions** avant d'exécuter un outil via `_should_execute_tool()`. Bloque l'exécution si `ToolPermissionError` est levée ou si la décision est `SKIP` | `vibe/core/agent_loop/_loop.py:L3027-3070` |
| **UI (Textual/ACP)** | Affiche les demandes de permission (callbacks) | **Ne décide pas** : transmet les réponses utilisateur à l'app-server. N'applique aucune logique de permission | `vibe/cli/textual_ui/widgets/approval_app.py:L1-320` |
| **Session Log** | Journalise les appels d'outils | **Enregistre** les tool calls y compris les refus via `ToolResultEvent` | `vibe/core/agent_loop/_loop.py:L2855-2900` |
| **App Server** | **Serveur autoritaire** pour les permissions | **Applique et fait respecter** le contrat : valide les outils, résout les permissions, projette les effets publics, gère les callbacks. Centralise la logique pour tous les clients | `docs/adr/0009-app-server-boundary.md:L150-160` |
| **ACP** | Protocole client | **Transmet** les callbacks de permission sans contournement. Ne modifie pas la logique de permission | `vibe/app_server/session.py:L829-930` |

---

## ---

## Synthèse des liens entre ADR et permissions (07-adr-et-contrat-des-outils.md:107)

| ADR | Lien avec les permissions | Niveau |
|-----|---------------------------|--------|
| 0001 | Architecture permet d'isoler les permissions comme un port | Indirect |
| 0002 | Les outils font partie du core qui gère les permissions | Direct |
| 0003 | Les approvals sont des événements typés dans la boucle | Indirect |
| **0004** | **Définition complète du tool contract et des permissions** | **Central** |
| **0005** | **Configuration des permissions via le système de layers** | **Direct** |
| 0007 | Les outils extensions doivent respecter le même contrat | Direct |
| 0008 | Instrumentation des événements de permission | Indirect |
| **0009** | **L'app-server est l'autorité centrale pour les permissions** | **Direct** |
| 0010 | UI affiche mais ne décide pas des permissions | Indirect |
| 0011 | Backends héritent de la politique de permission | Indirect |
| 0014 | Compatibilité des permissions entre versions | Indirect |
| **0015** | **Sécurité TLS pour les outils réseau** | **Direct** |

---

## **❌ Mistral Vibe n'utilise PAS de sandbox technique.**

La distinction est claire : (05-securite-et-sandbox.md:284)

| **Permissions** | **Sandbox** |
|----------------|-------------|
| Demander l'autorisation à l'utilisateur avant d'exécuter des actions sensibles | Limiter techniquement ce que le processus peut faire |
| Implémenté via `ToolPermission`, `PermissionStore`, `resolve_permission()` | Implémenté via seccomp, namespaces, chroot, conteneurs |
| **Présent** dans Mistral Vibe | **Absent** dans Mistral Vibe |
| Niveau **application** | Niveau **système d'exploitation** |
| Peut être contourné par une mauvaise configuration | Ne peut pas être contourné (sauf bug du kernel) |

---

## ---

## Scénarios de décision de permission (02-deroulement-et-scenarios.md:56)

| Situation | Outil | Résultat | Code responsable | Source |
|-----------|-------|----------|------------------|--------|
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

---

## ---

## Comportement spécial en cas de refus (02-deroulement-et-scenarios.md:203)

| Aspect | Comportement | Source |
|--------|--------------|--------|
| **Message renvoyé au LLM** | Oui : `ToolResultEvent` avec `error`, `decision=SKIP`, `approval_type`, `approval_source` | `_loop.py:L2855-2890` |
| **Compteur** | Oui : `stats.tool_calls_rejected += 1` | `_loop.py:L2868` |
| **Arrêt de la boucle** | ❌ Non : La boucle continue, seul l'outil est skipé | `_loop.py:L3027-3070` |
| **Journalisation** | ✅ Oui : `logger.info("Tool call denied tool=%s tool_call_id=%s outcome=denied")` | `_loop.py:L2863-2865` |
| **Session log** | ⚠️ Probablement : `ToolResultEvent` est généré, mais stockage explicite dans le session log non vérifié | `_loop.py:L2873-2890` |

---

## ---

## Résumé des edge cases (06-edge-cases.md:275)

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

