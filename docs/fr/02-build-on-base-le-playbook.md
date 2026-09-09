# Chapitre 2 -- build-on-base : le playbook et le routage par tache

`skills/build-on-base/SKILL.md` est la skill la plus large du depot : elle
consolide en un seul point d entree tout ce qu un agent doit savoir pour
developper sur Base -- reseau, contrats, Builder Codes, Base Account SDK,
enregistrement d agents, noeud, et migrations depuis OnchainKit ou
MiniKit/Farcaster.

La section "Default Stack" fixe des choix par defaut explicites plutot que
de laisser l agent deviner : Base Mainnet (chain id 8453) ou Base Sepolia
testnet (84532) pour le reseau, Foundry (`forge create` + verification
BaseScan) pour les contrats, le SDK Base Account (`@base-org/account`) pour
l authentification wallet, Base Pay (USDC, sans gas, reglement en moins de 2
secondes) pour les paiements, wagmi + viem pour les transactions, et les
Builder Codes (attribution ERC-8021 via `ox/erc8021`) pour le suivi.

La section "Safety Guardrails" liste des regles de securite concretes et
non negociables : ne jamais commiter de cle privee (utiliser
`cast wallet import` pour les keystores Foundry), ne jamais exposer de cle
API RPC ou des identifiants CDP cote client (toujours passer par un
backend), ne jamais sauter la verification serveur d un paiement (toujours
appeler `getPaymentStatus()` cote serveur et verifier expediteur, montant,
destinataire, avec un suivi des identifiants de transaction deja traites
pour empecher les attaques par rejeu), et ne jamais envoyer de transaction
sans l attribution Builder Codes -- une omission qui, precise le texte,
echoue silencieusement, sans erreur ni avertissement visible.

La skill fonctionne comme un routeur : une table "Task Routing" associe
chaque type de tache (config reseau, deploiement de contrat, noeud Base,
Builder Codes, Base Account SDK, enregistrement d agent, migration
OnchainKit, migration MiniKit vers Farcaster, conversion Mini App vers
application classique) au fichier `references/...md` correspondant, et la
"Operating Procedure" impose explicitement de classifier la tache, lire la
reference pertinente avant d implementer, confirmer le framework choisi avec
l utilisateur quand plusieurs options existent, puis livrer diffs, commandes
d installation et etapes manuelles (variables d environnement, cles API,
enregistrement du wallet).
