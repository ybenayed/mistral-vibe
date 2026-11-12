# Aspects Comportement

*Fichier source: 02-deroulement-et-scenarios.md*

## ---

## Comportement spécial en cas de refus

| Aspect | Comportement | Source |
|--------|--------------|--------|
| **Message renvoyé au LLM** | Oui : `ToolResultEvent` avec `error`, `decision=SKIP`, `approval_type`, `approval_source` | `_loop.py:L2855-2890` |
| **Compteur** | Oui : `stats.tool_calls_rejected += 1` | `_loop.py:L2868` |
| **Arrêt de la boucle** | ❌ Non : La boucle continue, seul l'outil est skipé | `_loop.py:L3027-3070` |
| **Journalisation** | ✅ Oui : `logger.info("Tool call denied tool=%s tool_call_id=%s outcome=denied")` | `_loop.py:L2863-2865` |
| **Session log** | ⚠️ Probablement : `ToolResultEvent` est généré, mais stockage explicite dans le session log non vérifié | `_loop.py:L2873-2890` |

---

