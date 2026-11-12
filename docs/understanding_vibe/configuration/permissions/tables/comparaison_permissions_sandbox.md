# Comparaison Permissions Sandbox

*Fichier source: 05-securite-et-sandbox.md*

## **❌ Mistral Vibe n'utilise PAS de sandbox technique.**

La distinction est claire :

| **Permissions** | **Sandbox** |
|----------------|-------------|
| Demander l'autorisation à l'utilisateur avant d'exécuter des actions sensibles | Limiter techniquement ce que le processus peut faire |
| Implémenté via `ToolPermission`, `PermissionStore`, `resolve_permission()` | Implémenté via seccomp, namespaces, chroot, conteneurs |
| **Présent** dans Mistral Vibe | **Absent** dans Mistral Vibe |
| Niveau **application** | Niveau **système d'exploitation** |
| Peut être contourné par une mauvaise configuration | Ne peut pas être contourné (sauf bug du kernel) |

---

