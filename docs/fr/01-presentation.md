# Chapitre 1 -- Presentation de base/skills

Ce depot n est pas une bibliotheque logicielle classique : c est une
collection d "Agent Skills" (au format de agentskills.io), c est a dire des
paquets d instructions en Markdown destines a etre charges par un assistant
IA (comme Claude) pour lui apprendre a construire sur Base -- deployer des
contrats, integrer un wallet, faire tourner un noeud, etc. Le depot ne
contient donc presque pas de code applicatif : il contient des `SKILL.md`
(le point d entree que l agent lit en premier) et des dossiers `references/`
(des fichiers charges a la demande, seulement quand la tache le justifie).

Le README distingue trois skills recommandees, installables individuellement
via `npx skills add base/skills --skill <nom>` (le CLI Skills de Vercel) :
`build-on-base` (le "playbook" complet de developpement Base -- reseau,
contrats, auth wallet, paiements, attribution, migrations), `base-mcp`
(donne a l assistant un wallet via le serveur MCP `mcp.base.org` : envoi,
swap, signature, appels groupes, plugins tiers) et `vibenet` (construire sur
le devnet Vibenet de Base, avec l account abstraction native EIP-8130 et le
sponsoring de gas ERC-8168).

Le principe commun aux trois skills est le "progressive reference loading" :
chaque `SKILL.md` est concu pour etre court et charge integralement des le
debut de la conversation, tandis que les fichiers `references/*.md` plus
detailles ne sont lus qu au moment ou la tache precise le demande -- ce qui
evite de saturer le contexte de l agent avec de la documentation non
pertinente pour la question posee.
