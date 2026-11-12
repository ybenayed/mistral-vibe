# Composants Contrat

*Fichier source: 07-adr-et-contrat-des-outils.md*

## - Les outils MCP/connector peuvent fournir des outils qui doivent **respecter le même contrat**
   - Un backend dont le protocole source porte intentionnellement des faits d'outils sans présentation Vibe peut traduire un ensemble fermé d'outils built-in vers ces catégories sémantiques existantes

### Ce que chaque outil doit respecter (Tool Contract)

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

### Quels composants doivent appliquer le contrat ?

| Composant | Rôle | Application du contrat | Source |
|-----------|------|-----------------------|--------|
| **Agent Loop** | Exécute les outils et gère la boucle LLM | **Applique les permissions** avant d'exécuter un outil via `_should_execute_tool()`. Bloque l'exécution si `ToolPermissionError` est levée ou si la décision est `SKIP` | `vibe/core/agent_loop/_loop.py:L3027-3070` |
| **UI (Textual/ACP)** | Affiche les demandes de permission (callbacks) | **Ne décide pas** : transmet les réponses utilisateur à l'app-server. N'applique aucune logique de permission | `vibe/cli/textual_ui/widgets/approval_app.py:L1-320` |
| **Session Log** | Journalise les appels d'outils | **Enregistre** les tool calls y compris les refus via `ToolResultEvent` | `vibe/core/agent_loop/_loop.py:L2855-2900` |
| **App Server** | **Serveur autoritaire** pour les permissions | **Applique et fait respecter** le contrat : valide les outils, résout les permissions, projette les effets publics, gère les callbacks. Centralise la logique pour tous les clients | `docs/adr/0009-app-server-boundary.md:L150-160` |
| **ACP** | Protocole client | **Transmet** les callbacks de permission sans contournement. Ne modifie pas la logique de permission | `vibe/app_server/session.py:L829-930` |

---

