# Chapitre 5 -- Vibenet : account abstraction native (EIP-8130) et sponsoring de gas

`vibenet` documente le devnet de Base pour l account abstraction native au
niveau protocole (EIP-8130) : des comptes portables entre chaines EVM,
supportant plusieurs types de signataires (secp256k1, P-256, WebAuthn), la
rotation de cle sans changement d adresse, des "acteurs" a cle de session
avec portee limitee, des politiques on-chain, et le sponsoring de gas
natif via ERC-8168. L outillage vit dans un module `eip8130` de viem, sur
une branche de fork -- pas encore publie sur npm au moment de la redaction.

Le fichier documente precisement les points d integration reseau : chain id
`84538453`, RPC d execution public `rpc.vibes.base.org` (compatible 0x79,
le type de transaction AA), un proxy RPC navigateur
`api.vibes.base.org/api/vibenet/account/rpc`, un payer heberge pour le
sponsoring ERC-8168, un faucet (`POST .../faucet/drip`) et son endpoint de
statut, et une verification de sante de chaine. Un avertissement explicite
previent d un piege : l hote correct est `api.vibes.base.org`, pas
`vibes.base.org` -- ce dernier redirige (302) vers la page HTML de
presentation, que le transport HTTP de viem tente ensuite de parser comme
du JSON, produisant une erreur trompeuse (`Unrecognized token '<'`) qui
ressemble a un bug de code plutot qu a une mauvaise URL.

Comme le module `eip8130` n est pas encore disponible via `npm install
viem`, la skill fournit un script d installation dedie
(`scripts/setup-viem-8130.sh`) qui clone la branche de fork
(`chunter-cb/viem` `feat/eip-8130-production`), la construit avec pnpm,
puis l installe dans le projet cible avec le flag `--install-links`
obligatoire -- sans ce flag, npm cree un lien symbolique vers un chemin
hors du dossier du projet, ce qui casse Turbopack et Next.js. Le fichier
precise que cette complexite est temporaire : une fois la PR upstream
`wevm/viem#5004` fusionnee et publiee sur npm, l installation se reduira a
un simple `npm install viem@latest`, sans changement d import ni d API.
