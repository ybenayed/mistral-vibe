# Adr

*Fichier source: 07-adr-et-contrat-des-outils.md*

## ---

## Liste complète des ADR liés aux permissions, outils ou sécurité

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

## ---

## Synthèse des liens entre ADR et permissions

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

