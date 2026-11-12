# Permissions Vs Sandbox


Comparaison entre les permissions et le sandbox


| Permissions | Sandbox |
| --- | --- |
| Demander l'autorisation à l'utilisateur avant d'exécuter des actions sensibles | Limiter techniquement ce que le processus peut faire |
| Implémenté via ToolPermission, PermissionStore, resolve_permission() | Implémenté via seccomp, namespaces, chroot, conteneurs |
| Présent dans Mistral Vibe | Absent dans Mistral Vibe |
| Niveau application | Niveau système d'exploitation |
| Peut être contourné par une mauvaise configuration | Ne peut pas être contourné (sauf bug du kernel) |


# Systeme Permissions


Le système de permissions de Mistral Vibe est uniquement basé sur


### Liste:


- La **demande d'autorisation** avant les actions sensibles

- La **détection de motifs dangereux** (denylist, fichiers sensibles, etc.)

- La **validation des chemins** (workspace boundaries)

- L'**analyse syntaxique** des commandes


# Protection Contre


Que protègent les permissions ?

